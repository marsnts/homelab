
Many ISP are operating on CGNAT (Carrier Grade NAT) to place consumers on a WAN network that share a single public IPv4 addresses due to IPv4 shortages. To bypass this, Tailscale is used to route traffic securely to a private Tailnet without a need of port forwarding, DDNS, and a dedicated public IP address.

Installing a Tailscale client on the ubuntu server:
```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

Run Tailscale:
```bash
sudo tailscale up
```

Visit the unique URL in the output, log in, and authorize the server to join the Tailnet.

Find the server's IP address using:
```bash
tailscale ip -4
```
	Keep the IP address, it will be used in configuring the nginx

Configure NGINX to restrict traffic to Tailscale. Edit the or create a configuration file:
```bash
sudo nano /etc/nginx/sites-available/tailscale-apps
```
Insert the following server block, replacing the Tailscale IP with the IP previously outputted:
```
server {
    # CRITICAL: Only bind to your internal Tailscale IP address
    listen YOUR_TAILSCALE_IP:80 default_server;
    listen 80;
    
    server_name homelab-server.tailnet.ts.net; # Your MagicDNS domain

    # SSL Certificates (Generated natively via 'tailscale cert')
    ssl_certificate /etc/nginx/certs/homelab.crt;
    ssl_certificate_key /etc/nginx/certs/homelab.key;

    # Universal Reverse Proxy Block
    location / {
	    proxy_pass http://127.0.0.1:8123; # Ensure this matches your actual port
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # WebSockets support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

```
Enable the configuration and link them with:
```bash
sudo ln -s /etc/nginx/sites-available/tailscale-apps /etc/nginx/sites-enabled/
```

NGINX splits configuration management into two directories to make it easy to toggle sites on and off without deleting them.
	`/etc/nginx/site-available/` holds all virtual host configurations, whether they are currently running or not.
	`/etc/nginx/sites-enabled/` holds all virtual host configurations and serve them using nginx.

Test and restart nginx:
```bash
sudo nginx -t
sudo systemctl restart nginx
```

To guarantee that applications within the server aren't accidentally exposed to local home network, use `ufw` to restrict port access allowing only standard SSH access over Tailscale only:
```bash
sudo ufw allow in on tailscale0 to any port 22 proto tcp
```
Allow web traffic (HTTP/HTTPS) Tailscale only:
```bash
sudo ufw allow in on tailscale0 to any port 80 proto tcp
sudo ufw allow in on tailscale0 to any port 443 proto tcp
```
Enable firewall if not yet enabled:
```bash
sudo ufw enable
```
Verify active rules:
```bash
sudo ufw status verbose
```


For enhanced security, Implement SSL certificates to additionally ensure that nginx reloads seamlessly when they renew.

Find first the exact Tailscale magicDNS full name:
```bash
tailscale status
```
	Look for the ubuntu server on the list it will look like machine-name.tailnet.ts.net

Create a directory for nginx's certs:
```bash
sudo mkdir -p /etc/nginx/certs
```
Use Tailscale binary to fetch a valid "Let's Encrypt" certificate directly from their servers:
```
sudo tailscale cert --cert-file /etc/nginx/certs/homelab.crt --key-file /etc/nginx/certs/homelab.key machine-name.tailnet.ts.net
```
	Replace machine-name.tailnet.ts.net with the tailscale magicDNS previously outputted.

Set secure permissions so only root and nginx read the private key:
```bash
sudo chmod 600 /etc/nginx/certs/homelab.key
sudo chmod 644 /etc/nginx/certs/homelab.crt
```

Tailscale certificate expire every 90 days. While Tailscale handles background renewal of certificates automatically, nginx, on the other hand, must be reloaded to read the updated files.

Thus, creating a native systemd path watcher or timer is reliable than a cron job:
```bash
sudo nano /etc/systemd/system/tailscale-cert-reload.service
```
Paste the following configuration:
```
[Unit]
Description=Reload NGINX after Tailscale Certificate Renewal
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/tailscale cert --cert-file /etc/nginx/certs/homelab.crt --key-file /etc/nginx/certs/homelab.key machine-name.tailnet.ts.net
ExecStartPost=/usr/sbin/systemctl reload nginx

[Install]
WantedBy=multi-user.target
```
Create a matching systemd timer file to run this check automatically:
```bash
sudo nano /etc/systemd/system/tailscale-cert-reload.timer
```
Paste the following configuration:
```
[Unit]
Description=Weekly check for Tailscale Cert Renewal

[Timer]
OnCalendar=Sun *-*-* 00:00:00
Persistent=true

[Install]
WantedBy=timers.target
```
Enable and start the new timer:
```bash
sudo systemctl daemon-reload
sudo systemctl enable --now tailscale-cert-reload.timer
```

Verify if the renewal schedule is working and the nginx is listening purely on Tailscale:
```bash
systemctl list-timers --all | grep tailscale
sudo ss -tulpn | grep nginx
```


To route the webpage in an open public channel, Authorize it in the Tailscale account setting found on the [Tailscale Admin Console](https://console.tailscale.com/admin/acls/visual/general-access-rules).

Go the the Access Control tab and add a `nodeAttrs` block to allow Funnel on the Tailnet:
```json
"nodeAttrs": [
    {
        "target": ["autogroup:admin"],
        "attr":   ["funnel"],
    },
],
```

Point the nginx to localhost. Tailscale background service handles incoming public traffic and reroutes it internally. Because of this, nginx needs to listen on 172.0.0.1 (localhost) so Tailscale can handle traffic locally

Update nginx configuration of `/etc/nginx/sites-available/homelab-services` to:
```nginx
server {
    # Listen on localhost; Tailscale Funnel will forward public traffic here
    listen 127.0.0.1:8080;
    
    server_name machine-name.tailnet.ts.net;

    # Your web files or reverse proxy setup
    location / {
        root /var/www/html; # Path to your website files
        index index.html;
    }
}
```

Test and restart nginx:
```bash
sudo nginx -t
sudo systemctl restart nginx
```

Turn on the funnel to pull public traffic from the internet and route it directly into your local nginx port:
```bash
sudo tailscale funnel 443
```

Tailscale will output a public URL which will be the standard MagicDNS address: `https://ts.net`

Allow HTTPS Traffic to pass through
```bash
sudo tailscale serve --bg --terminate-tls=false https:443 text://localhost:443
```
Turn on the tailscale funnel:
```bash
sudo tailscale funnel 443 on
sudo tailscale funnel --bg http://localhost:80
```
Verify it's status:
```bash
sudo tailscale serve status
```
If funnel needs to be restarted:
```bash
sudo tailscale funnel --bg http://localhost:80 off
sudo tailscale funnel --bg http://localhost:80
sudo tailscale serve status
```
