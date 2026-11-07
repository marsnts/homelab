
This website log monitoring is built to achieve a live interface with real-time notifications whenever someone access the public website through Tailscale tunnel. 

It does the following:
	1. Host a static website (static-site).
	2. Host a log viewer that monitors static-site.
	3. Avoid exposing server's public IP or opening inbound router ports.
	4. Centralize HTTP/HTTPS routing and access logging through Nginx.
	5. Restrict access to the log viewer to authorized administrators

For the log viewer, GoAccess is used to parse Nginx access logs and provide dashboard with visitor statistics, requested urls, referrers, browsers, operating systemns, and HTTP status codes.

The static-site used `tailscale funnel` for public access while the log-monitoring-site used `tailscale serve` to only allow clients within the Tailnet to freely access the log-monitoring-site.


