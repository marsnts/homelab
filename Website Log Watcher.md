
This website log watcher is built to achieve a live interface with real-time notifications whenever someone access the public website through Tailscale tunnel. 

This will be separated into three parts of the architecture:
1. The Log Watcher (Backend)
	A tiny node.js script that runs on the ubuntu server. It basically streams all Nginx access log using `tail -f /var/log/nginx/access.log`.
2. Real-time bridge:
	The backend then hosts a WebSocket server. Whenever a new line appears in the nginx log, it parses it and broadcasts it instantly.
3. The Interface (Frontend):
	A simple HTML Dashboard that connects to the WebSocket. It updates a live view counter and triggers a visual notification on the screen whenever someone accesses the website.


### The Log Watcher

Creating a folder for the application and install websocket
```bash
cd /var/www/
mkdir tailscale-monitor
cd tailscale-monitor
sudo apt install npm -y
npm init -y
npm install ws
```
Create a file named `server.js`. It tracks real-time traffic and calculates total unique views:
`server.js`
```js
const WebSocket = require('ws');
const { spawn } = require('child_process');

// Start WebSocket server on port 8080
const wss = new WebSocket.Server({ port: 8080 });
let totalViews = 0;

// Keep track of connected clients
wss.on('connection', (ws) => {
    console.log('Frontend dashboard connected.');
    // Send initial state to newly connected dashboard
    ws.send(JSON.stringify({ type: 'init', totalViews }));
});

// Tail the Nginx access log in real-time
const tail = spawn('tail', ['-f', '/var/log/nginx/access.log']);

tail.stdout.on('data', (data) => {
    const lines = data.toString().split('\n');
    
    lines.forEach(line => {
        if (!line.trim()) return;

        // Common Log Format regex to extract IP, Timestamp, Request, and Status Code
        const match = line.match(/^(\S+) \S+ \S+ \[(.*?)\] "(\S+ \S+ \S+)" (\d+)/);
        
        if (match) {
            totalViews++;
            
            const logData = {
                type: 'hit',
                ip: match[1],
                timestamp: match[2],
                request: match[3],
                status: match[4],
                totalViews: totalViews
            };

            // Broadcast the hit instantly to all active frontend connections
            wss.clients.forEach(client => {
                if (client.readyState === WebSocket.OPEN) {
                    client.send(JSON.stringify(logData));
                }
            });
        }
    });
});

tail.stderr.on('data', (data) => {
    console.error(`Tail error: ${data}`);
});

console.log('Log watcher backend running on ws://localhost:8080');

```
Run this backend script with administrative permissions so it can read the Nginx log file:
```bash
sudo node server.js
```

### Dashboard Interface

Create an `index.html` file. It can be opened on the local machine using VS Code.
###### `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailscale Live Traffic Monitor</title>
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent-color: #3b82f6;
            --success-color: #10b981;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 2rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: background-color 0.1s ease;
        }

        /* Visual Alert Flash Effect */
        body.flash {
            background-color: #1e3a8a;
        }

        .container {
            max-width: 800px;
            width: 100%;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
        }

        .status-badge {
            padding: 0.5rem 1rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 600;
            background-color: #ef4444;
            color: #ffffff;
        }

        .status-badge.connected {
            background-color: var(--success-color);
        }

        .counter-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 2rem;
            text-align: center;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
            margin-bottom: 2rem;
            border: 1px solid #334155;
        }

        .counter-card h2 {
            margin: 0;
            font-size: 1.25rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .counter-value {
            font-size: 4rem;
            font-weight: 800;
            margin: 0.5rem 0 0 0;
            color: var(--accent-color);
        }

        .log-container {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid #334155;
        }

        .log-container h3 {
            margin-top: 0;
            margin-bottom: 1rem;
            color: var(--text-main);
        }

        .log-feed {
            max-height: 300px;
            overflow-y: auto;
            font-family: monospace;
            font-size: 0.9rem;
            display: flex;
            flex-direction: column-reverse;
            gap: 0.5rem;
        }

        .log-entry {
            padding: 0.5rem;
            background-color: var(--bg-color);
            border-left: 4px solid var(--accent-color);
            border-radius: 0 4px 4px 0;
            animation: slideIn 0.2s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Tailscale Funnel Traffic</h1>
            <div id="status" class="status-badge">Disconnected</div>
        </header>

        <div class="counter-card">
            <h2>Total Live Views</h2>
            <div id="counter" class="counter-value">0</div>
        </div>

        <div class="log-container">
            <h3>Live Activity Stream</h3>
            <div id="logFeed" class="log-feed">
                <div style="color: var(--text-muted)">Awaiting connection...</div>
            </div>
        </div>
    </div>

    <script>
        // REPLACE WITH YOUR UBUNTU SERVER'S IP OR TAILSCALE IP IF ACCESSED REMOTELY
        const SERVER_IP = 'localhost'; 
        const wsUrl = `ws://${SERVER_IP}:8080`;
        
        const counterEl = document.getElementById('counter');
        const statusEl = document.getElementById('status');
        const logFeedEl = document.getElementById('logFeed');

        // Simple synthetically generated audio ping context to avoid missing external audio file errors
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function playNotificationSound() {
            if (audioCtx.state === 'suspended') return; // Browser security fallback
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(587.33, audioCtx.currentTime); // D5 note
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.15);
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.15);
        }

        function triggerVisualNotification() {
            document.body.classList.add('flash');
            setTimeout(() => {
                document.body.classList.remove('flash');
            }, 100);
        }

        function connectWebSocket() {
            const ws = new WebSocket(wsUrl);

            ws.onopen = () => {
                statusEl.textContent = 'Connected';
                statusEl.classList.add('connected');
                logFeedEl.innerHTML = '<div style="color: var(--text-muted)">Connected. Listening for live traffic...</div>';
            };

            ws.onmessage = (event) => {
                const data = JSON.parse(event.data);

                if (data.type === 'init') {
                    counterEl.textContent = data.totalViews;
                } 
                
                if (data.type === 'hit') {
                    // Update counter
                    counterEl.textContent = data.totalViews;

                    // Trigger sound and screen flash
                    playNotificationSound();
                    triggerVisualNotification();

                    // Append real-time activity log log
                    const logEntry = document.createElement('div');
                    logEntry.className = 'log-entry';
                    logEntry.innerHTML = `<strong>[${data.timestamp}]</strong> ${data.ip} &mdash; <span style="color: #60a5fa">${data.request}</span> &mdash; Status: <strong>${data.status}</strong>`;
                    
                    // Clear placeholder on first message
                    if (logFeedEl.children[0] && logFeedEl.children[0].style.color) {
                        logFeedEl.innerHTML = '';
                    }
                    
                    logFeedEl.appendChild(logEntry);
                }
            };

            ws.onclose = () => {
                statusEl.textContent = 'Disconnected';
                statusEl.classList.remove('connected');
                // Proactively try to reconnect every 5 seconds
                setTimeout(connectWebSocket, 5000);
            };

            ws.onerror = (err) => {
                console.error('WebSocket Error:', err);
                ws.close();
            };
        }

        // Initialize audio engine on first click due to browser autoplay restrictions
        window.addEventListener('click', () => {
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        });

        connectWebSocket();
    </script>
</body>
</html>
```


### Making it Public
I wanted this website to be added to my portfolio. Thus publishing this publicly is my goal. However, because it contains sensitive information like visitor's public IP addresses and request logs, I wanted to create it with a secure HTTP basic authentication with nginx. 

#### Generating a Secure Password Hash
`htpasswd` is used to create an encrypted username and password file. But first, Apache utility tools needed to be installed:
```bash
sudo apt update
sudo apt install apache2-utils -y
```
Create the password file, replace `username`:
```bash
sudo htpasswd -c /etc/nginx/.htpasswd username
```
Type and confirm a strong password when prompted

#### Configuring Nginx to Serve the Dashboard and Protect it

Updating the Nginx server block configuration file to protect the directory and reverse-proxy the WebSocket Traffic.
```bash
sudo nano /etc/nginx/sites-available/tailscale-apps
```
Update the Nginx server block:
```nginx
server {
    listen 80; # Or your specific Tailscale port setup
    server_name your-tailscale-funnel-domain.ts.net;

    # Protect and serve the Frontend Dashboard
    location / {
        root /var/www/tailscale-monitor;
        index index.html;
        
        # Enforce the login prompt
        auth_basic "Restricted Live Dashboard";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }

    # Protect and reverse-proxy the WebSocket connection
    location /ws/ {
        # Enforce the exact same login prompt for the WebSocket connection
        auth_basic "Restricted Live Dashboard";
        auth_basic_user_file /etc/nginx/.htpasswd;

        proxy_pass http://127.0.0;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
    }
}
```
Test the configuration and restart it:
```bash
sudo nginx -t
sudo systemctl restart nginx
```

#### Updating the Frontend to use the Nginx Proxy

Nginx is now securely proxying the websocket under the same domain name, port 8080 isn't needed to be exposed to the internet.

Change `index.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailscale Live Traffic Monitor</title>
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent-color: #3b82f6;
            --success-color: #10b981;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 2rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: background-color 0.1s ease;
        }

        /* Visual Alert Flash Effect */
        body.flash {
            background-color: #1e3a8a;
        }

        .container {
            max-width: 800px;
            width: 100%;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
        }

        .status-badge {
            padding: 0.5rem 1rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 600;
            background-color: #xef4444;
            color: #ffffff;
        }

        .status-badge.connected {
            background-color: var(--success-color);
        }

        .counter-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 2rem;
            text-align: center;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
            margin-bottom: 2rem;
            border: 1px solid #334155;
        }

        .counter-card h2 {
            margin: 0;
            font-size: 1.25rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .counter-value {
            font-size: 4rem;
            font-weight: 800;
            margin: 0.5rem 0 0 0;
            color: var(--accent-color);
        }

        .log-container {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid #334155;
        }

        .log-container h3 {
            margin-top: 0;
            margin-bottom: 1rem;
            color: var(--text-main);
        }

        .log-feed {
            max-height: 300px;
            overflow-y: auto;
            font-family: monospace;
            font-size: 0.9rem;
            display: flex;
            flex-direction: column-reverse;
            gap: 0.5rem;
        }

        .log-entry {
            padding: 0.5rem;
            background-color: var(--bg-color);
            border-left: 4px solid var(--accent-color);
            border-radius: 0 4px 4px 0;
            animation: slideIn 0.2s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Tailscale Funnel Traffic</h1>
            <div id="status" class="status-badge">Disconnected</div>
        </header>

        <div class="counter-card">
            <h2>Total Live Views</h2>
            <div id="counter" class="counter-value">0</div>
        </div>

        <div class="log-container">
            <h3>Live Activity Stream</h3>
            <div id="logFeed" class="log-feed">
                <div style="color: var(--text-muted)">Awaiting connection...</div>
            </div>
        </div>
    </div>

    <script>
        // Automatically infers your public Tailscale Funnel domain and uses the secure /ws/ path
        const protocol = window.location.protocol === 'https:' ? 'wss:' : 'ws:'; const wsUrl = `${protocol}//${window.location.host}/ws/`;
        
        const counterEl = document.getElementById('counter');
        const statusEl = document.getElementById('status');
        const logFeedEl = document.getElementById('logFeed');

        // Simple synthetically generated audio ping context to avoid missing external audio file errors
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function playNotificationSound() {
            if (audioCtx.state === 'suspended') return; // Browser security fallback
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(587.33, audioCtx.currentTime); // D5 note
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.15);
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.15);
        }

        function triggerVisualNotification() {
            document.body.classList.add('flash');
            setTimeout(() => {
                document.body.classList.remove('flash');
            }, 100);
        }

        function connectWebSocket() {
            const ws = new WebSocket(wsUrl);

            ws.onopen = () => {
                statusEl.textContent = 'Connected';
                statusEl.classList.add('connected');
                logFeedEl.innerHTML = '<div style="color: var(--text-muted)">Connected. Listening for live traffic...</div>';
            };

            ws.onmessage = (event) => {
                const data = JSON.parse(event.data);

                if (data.type === 'init') {
                    counterEl.textContent = data.totalViews;
                } 
                
                if (data.type === 'hit') {
                    // Update counter
                    counterEl.textContent = data.totalViews;

                    // Trigger sound and screen flash
                    playNotificationSound();
                    triggerVisualNotification();

                    // Append real-time activity log log
                    const logEntry = document.createElement('div');
                    logEntry.className = 'log-entry';
                    logEntry.innerHTML = `<strong>[${data.timestamp}]</strong> ${data.ip} &mdash; <span style="color: #60a5fa">${data.request}</span> &mdash; Status: <strong>${data.status}</strong>`;
                    
                    // Clear placeholder on first message
                    if (logFeedEl.children[0] && logFeedEl.children[0].style.color) {
                        logFeedEl.innerHTML = '';
                    }
                    
                    logFeedEl.appendChild(logEntry);
                }
            };

            ws.onclose = () => {
                statusEl.textContent = 'Disconnected';
                statusEl.classList.remove('connected');
                // Proactively try to reconnect every 5 seconds
                setTimeout(connectWebSocket, 5000);
            };

            ws.onerror = (err) => {
                console.error('WebSocket Error:', err);
                ws.close();
            };
        }

        // Initialize audio engine on first click due to browser autoplay restrictions
        window.addEventListener('click', () => {
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        });

        connectWebSocket();
    </script>
</body>
</html>
```


### Reconfiguring Nginx and Tailscale

Since static-site is currently listening on port 80, a second site with the same setup cannot listen on the same port. Thus using an internal port for nginx to let tailscale route custom subdomains to them

##### Updating Nginx to Separate Sites by Ports
Edit the configuration file `/etc/nginx/sites-available/tailscale-apps`
```bash
sudo nano /etc/nginx/sites-available/tailscale-apps
```
Edit server block:
```nginx
# App 1 (Marsnts) - Accessible on standard HTTP port 80
server {
    listen 100.104.219.65:443 ssl;
    server_name marsnts.tarsier-map.ts.net;

	    # SSL Certificates (Generated natively via 'tailscale cert')
    ssl_certificate /etc/nginx/certs/homelab.crt;
    ssl_certificate_key /etc/nginx/certs/homelab.key;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

# App 2 (Logs) - Accessible on port 8080
server {
    listen 100.104.219.65:8080 ssl;
    server_name marsnts.tarsier-map.ts.net;

    # SSL Certificates (Generated natively via 'tailscale cert')
    ssl_certificate /etc/nginx/certs/homelab.crt;
    ssl_certificate_key /etc/nginx/certs/homelab.key;

   # Protect and serve the Frontend Dashboard
    location / {
        root /var/www/tailscale-monitor;
        index index.html;

        # Enforce the login prompt
        auth_basic "Restricted Live Dashboard";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }

    # Protect and reverse-proxy the WebSocket connection
    location /ws/ {
        # Enforce the exact same login prompt for the WebSocket connection
        auth_basic "Restricted Live Dashboard";
        auth_basic_user_file /etc/nginx/.htpasswd;

        proxy_pass http://127.0.0.1:3002;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
    }
}
```

##### Allow Traffic on port 8080 on UFW 
Check if port 8080 is allowed by the UFW:
```bash
sudo ufw status
```
If 8080 is not present, allow it:
```bash
sudo ufw allow 8080/tcp
```
Verify if nginx is actually listening on port 8080:
```bash
sudo ss -tulpn | grep :8080
```
If it returns nothing, nginx is not listening on port 8080, check nginx config errors and restart nginx.

##### Ensure that App on port 3002 is running
If frontend dashboard service on port 3002 is dead, nginx might drop connections. Verify if backend service is running locally:
```bash
curl -I http://127.0.0.1:3002
```



### How does Tailscale Tunnel and Nginx Routes 2 different apps in 2 different ports?

Routing traffic through a tailscale tunnel paired with an Nginx reverse proxy allows to securely expose multiple internal web applications running on different ports without opening any additional ports on the physical router or firewall.

Tailscale manages the secure transport layer while nginx handles the application routing layer.

1. High Level Architecture:
	When a client requests one oif the application, the traffic flows in three specific stages:
		`client` -> `Tailscale Interface (tailnet)` -> `nginx (listening ports)` - > `target web app`
2. Tailscale Tunnel
	When Tailscale is installed it assign a static private IP within the 100.64.0.0 block known as tailnet IP. When a client types the Tailscale IP or the MagicDNS name, Tailscale encrypts the data and drops it directly onto the server's virtual network interface.
3. Reverse Proxy - Nginx Routing
	Once Tailscale delivers the network packet to the machine, nginx handles them and act as a traffic controller. It listens directly on the tailscale interface `tailnet0` or on all interfaces `0.0.0.0`.
	Then Nginx route two / multiple web apps on two different ports using two methods:
		Port Based Routing
			In this setup nginx listens to two distinct external port and funnels traffic to the corresponding internal ports where the apps is currently running.
		Domain/Subdomain Routing:
			If using Tailscale MagicDNS or custom local domains, nginx is used to read incoming HTTP host header. This allows standard web ports like 80 or 443 for both apps.
4. Application Layer
	Then the web application `Node.js app on Port 3000` and `Python API on port 4000` received the forwarded request from the nginx via local loopback address `127.0.0.1`


###### Port Based Routing
```nginx
# PORT BASED ROUTING
# /etc/nginx/sites-available/multi-apps.conf

# Routing for Web App 1
server {
    listen 8081; # Entry port for App 1
    server_name my-server;

    location / {
        proxy_pass http://127.0.0.1:3000; # Internal port for App 1
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

# Routing for Web App 2
server {
    listen 8082; # Entry port for App 2
    server_name my-server;

    location / {
        proxy_pass http://127.0.0.1:4000; # Internal port for App 2
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```
Clients accesses the `http://100.x.x.x:8081` for web app 1 and `http://100.x.x.x:8082` for web app 2.
###### Subdomain / Domain Based Routing
```nginx
# Routing based on Subdomains (Requires DNS records pointing to your Tailscale IP)
server {
    listen 80;
    server_name app1.my-domain.ts.net;

    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}

server {
    listen 80;
    server_name app2.my-domain.ts.net;

    location / {
        proxy_pass http://127.0.0.1:4000;
    }
}
```
The client enters the standard URL without a port number. Nginx inspects the text domain name requested by the browser and forwards the request internally to port 3000 or 4000 accordingly.






```
server {
    listen 80;
    server_name _;

    root /var/www/static-resume;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
