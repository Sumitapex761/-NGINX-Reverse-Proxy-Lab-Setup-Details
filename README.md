# -NGINX-Reverse-Proxy-Lab-Setup-Details

Machine 1 (NGINX): 192.168.80.129

Machine 2 (Apache2 Web Server): 192.168.80.130

Objective: When a client accesses the NGINX machine (192.168.80.129), the request should be forwarded to the Apache2 server (192.168.80.130).


🛠 Step-by-Step Configuration
1. Check existing NGINX configuration
   
tree /etc/nginx/sites-*


2. (Optional) Remove old enabled configurations:

sudo rm /etc/nginx/sites-enabled/*
tree /etc/nginx/sites-*

3. Create a reverse proxy configuration file:

sudo nano /etc/nginx/sites-available/rp.conf

Paste the following content: 
server {
    listen 80;
    location / {
        proxy_pass http://192.168.80.130;
    }
}

4. Enable the reverse proxy by creating a symbolic link:
   
   sudo ln -s /etc/nginx/sites-available/rp.conf /etc/nginx/sites-enabled/

5. Test the NGINX configuration:

sudo nginx -t -c /etc/nginx/nginx.conf


6. Reload NGINX to apply changes:

sudo systemctl reload nginx

🎯 Final Output
Visiting http://192.168.80.129 will route the request to http://192.168.80.130 (Apache2 server).


📁 Final Directory Structure

/etc/nginx
├── nginx.conf
├── sites-available
│   └── rp.conf                 # Reverse proxy config file
└── sites-enabled
    └── rp.conf → ../sites-available/rp.conf   # Symbolic link







