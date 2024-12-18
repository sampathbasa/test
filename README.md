```
FROM python:3.10

# Install Rust toolchain and build tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    build-essential \
    && curl https://sh.rustup.rs -sSf | sh -s -- -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Add Rust binaries to PATH
ENV PATH="/root/.cargo/bin:$PATH"

# Install Python dependencies
RUN /bin/bash -c "source $HOME/.cargo/env && pip install --upgrade pip && pip install -r ./python_api/packages/requirements.txt"


# Install Rust toolchain and build tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    build-essential \
    && curl https://sh.rustup.rs -sSf | sh -s -- -y \
    && export PATH="$HOME/.cargo/bin:$PATH" \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Add Rust binaries to PATH
ENV PATH="/root/.cargo/bin:$PATH"













-------------------------------------------
version: "3.3"
services:
    nginx-dev:
          image: nginx:latest
          container_name: nginx-dev
          volumes: 
            - ./default.dev.conf:/etc/nginx/conf.d/default.dev.conf
            - ./ssl:/etc/nginx/ssl
          restart: always
          ports:
            - "80:80"
            - "443:443"
          networks:
            - nissan
    
volumes:
  ci-dev:  

networks:
  ci-dev:
    external: true



server {
    listen 80;
    server_name domainname;
    return 301 https://domain name$request_uri;
}

# HTTPS server block for secure connections
server {
    listen 443 ssl;
    ssl_certificate     /etc/nginx/ssl/fullchain.pem;
    ssl_certificate_key /etc/nginx/ssl/privkey.pem;
    server_name .com;
    server_tokens off;

    # Security Headers
    add_header X-Frame-Options "DENY" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-Xss-Protection "1; mode=block" always;

    # Limit client upload size
    client_max_body_size 20000M;

    # Timeout settings for proxy
    proxy_connect_timeout 600s;
    proxy_send_timeout 600s;
    proxy_read_timeout 600s;
    send_timeout 600s;

    # Proxy for Invoice Extraction API
    location ~ /api/v1/ {
        proxy_pass http://service:8001;
        proxy_redirect off;
        proxy_set_header HOST $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $server_name;
    }

    # Proxy for other API routes
    location ~ /api/v1/ {
        proxy_pass http://:8000;
        proxy_redirect off;
        proxy_set_header HOST $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $server_name;
    }

    # Proxy for the frontend
    location / {
        proxy_pass http://service:80;
        proxy_set_header HOST $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}




server {
    listen 80;
    location / {
      root   /usr/share/nginx/html;
      index  index.html index.htm;
      try_files $uri $uri/ /index.html;
    } 
    error_page 404 /index.html;
    location = / {
      root /usr/share/nginx/html;
      internal;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
      root   /usr/share/nginx/html;
    }
  }








# Generate a new private key
openssl genrsa -out your_domain.key 2048

# Generate a new CSR using this key
openssl req -new -key your_domain.key -out your_domain.csr
--------------------------------------------------


openssl rsa -noout -modulus -in /path/to/your/private.key | openssl md5
openssl x509 -noout -modulus -in /path/to/your/certificate.crt | openssl md5
------------------------------


server {
    listen 443 ssl;
    server_name your_domain.com;

    ssl_certificate     /path/to/your/certificate.crt;
    ssl_certificate_key /path/to/your/private.key;
    
    # Strong SSL Security Settings
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    
    # Other recommended settings
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;

    # HSTS (uncomment if you're sure)
    # add_header Strict-Transport-Security "max-age=63072000" always;

    location / {
        proxy_pass http://your_backend_service;
    }
}

# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name your_domain.com;
    return 301 https://$host$request_uri;
}


--------------------------------------------------------------------------------------------------------------------
useradd -r -s /sbin/nologin nginx
cat /etc/nginx/nginx.conf
user nginx;


sudo yum update -y
sudo amazon-linux-extras install nginx1.12
sudo systemctl start nginx sudo systemctl enable nginx
sudo systemctl status nginx
sudo nano /etc/nginx/conf.d/mywebsite.conf
sudo nginx -t
sudo systemctl reload nginx


sudo ls -l /proc/1/exe
sudo ls -l /proc/1/exe
sudo ls -lah /lib/systemd/system/nginx.service
sudo ls /lib/systemd/system/nginx.service



sudo rm -rf /usr/lib/systemd/system/nginx.service
sudo dnf remove nginx
sudo yum remove nginx
sudo userdel -r nginx


sudo rm -rf /etc/nginx
sudo rm -rf /etc/init.d/nginx
sudo rm -rf /var/log/nginx
sudo rm -rf /var/cache/nginx/
sudo rm -rf /usr/sbin/nginx


sudo rm -rf /etc/nginx
sudo rm -rf /var/log/nginx
sudo rm -rf /usr/sbin/nginx
sudo rm -rf /run/nginx.pid
sudo find / -name "nginx" -exec rm -rf {} +

sudo amazon-linux-extras enable nginx1
sudo yum clean all
sudo yum install nginx -y

sudo systemctl start nginx
sudo systemctl enable nginx

sudo journalctl -xe
sudo systemctl status nginx

sudo find / -type l -name "nginx"

rpm -ql nginx | grep conf

```
amazon-linux-extras list | grep nginx
amazon-linux-extras enable nginx1
sudo yum clean metadata
sudo yum -y install nginx
nginx -v
