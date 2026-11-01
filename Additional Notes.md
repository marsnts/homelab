### Setting up Cloudflared (Aborted)

If you don't have a static IP and do not want to touch your router for port forwarding, setting up cloudflared is used to secure a bridge to expose your site to the internet without exposing your home IP address.

Download and install cloudflare daemon:
```bash
sudo mkdir -p --mode=0755 /usr/share/keyrings
curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | sudo tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null
```
Add cloudflare's apt repo to your apt repository:
```bash
echo "deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared any main" | sudo tee /etc/apt/sources.list.d/cloudflared.list
```
Update repositories and install cloudflared:
```bash
sudo apt-get update && sudo apt-get install cloudflared
```
Verify the installation:
```bash
cloudflared --version
```

Authenticate cloudflared:
```bash
cloudflared tunnel login
```
This will output a URL. Paste this to your browser, log in, and authorize your domain name.

Create a tunnel:
```bash
cloudflared tunnel create home-website
```
	replace "home-website" to your desired tunnel name
It will output a tunnel Tunnel ID (UUID) and the path to the credentials JSON file. Save or note it down. 

Configure traffic routing by creating a local configuration file:
```bash
mkdir ~/.cloudflared
nano ~/.cloudflared/config.yml
```
Paste the following template and replace all placeholder with your actual tunnel ID, file path, and domain:
```bash
url: http://localhost:80
tunnel: YOUR_TUNNEL_UUID
credentials-file: /home/YOUR_USERNAME/.cloudflared/YOUR_TUNNEL_UUID.json

ingress:
  - hostname: yourdomain.com
    service: http://localhost:80
  - service: http_status:404

```
Route your DNS, replace placeholder with your actual domain name and tunnel name:
```bash
cloudflared tunnel route ip add <IP/CIDR> <UUID or NAME>
```

Run the tunnel as a background service to ensure that website stays up when your machine reboots:
```bash
sudo cloudflared --config ~/.cloudflared/config.yml service install
```
Start and enable the service:
```bash
sudo systemctl start cloudflared
sudo systemctl enable cloudflared
```
Confirm that the route has been successfully established:
```bash
cloudflared tunnel route ip show
```

Run the tunnel:
```bash
cloudflare tunnel run <UUID or NAME>
```
Check the tunnel to get information:
```bash
cloudflared tunnel info <UUID or NAME>
```
---

### Additional Notes
```
sudo systemctl enable ssh --now
sudo nginx -t
sudo systemctl enable nginx --now
sudo systemctl status nginx
sudo systemctl status tailscaled
sudo tailscale funnel --bg http://localhost:80
curl -v https://marsnts.tarsier-map.ts.net
curl -I https://marsnts.tarsier-map.ts.net
```