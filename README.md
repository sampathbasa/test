```
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
