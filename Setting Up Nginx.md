
Nginx should be installed before doing this part.

Create an index.html template inside the /var/www/static-resume/ directory.
	replace "static-resume" to the name of the folder

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Self-Hosted Site</title>
</head>
<body>
    <h1>Hello, world!</h1>
    <p>This static site is self-hosted.</p>
</body>
</html>
```

Configure nginx by creating a new site configuration file:

```bash
sudo nano /etc/nginx/sites-available/static-resume
```

Insert the following basic server block layout:
```
server {
    listen 80;
    server_name marsnts.com www.marsnts.com;

    root /var/www/static-resume;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
	Replace "marsnts" with the actual server name or domain name, and "static-resume" with the actual project folder / path
	
Enable the site configuration file and restart nginx:
```bash
sudo ln -s /etc/nginx/sites-available/static-resume /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

If default nginx site is still showing whenever you access localhost, delete the default nginx config:
```bash
sudo rm /etc/nginx/sites-enabled/default
```
	Note that the default config is still available at /etc/nginx/sites-available whenever needed