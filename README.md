# n8n

How to install n8n server in GCP

1. Create a virtual machine in GCP, a cheap setup is:
   E2 micro
   Ubuntu
   30GB
   Allow hhtp, hhtps and XXXX

2. Login to your new VN using SSH

3. Create the required directories:
   mkdir -p nginx/conf.d certbot/www certbot/conf

4. Install nano
  sudo apt update
  sudo apt install nano

5. Create and save the Nginx configuration file ./nginx/cond.f/n8n.conf  n8n-murbano.ddns.net

server {
    listen 80;
    server_name your-domain.com;

    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }

    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name your-domain.com;

    ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem;

    location / {
        proxy_pass http://n8n:5678;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}


6. Install Docker and docker compose

7. 
8. 
