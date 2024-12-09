```
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



sudo cp /usr/share/nginx/nginx.conf.default /etc/nginx/nginx.conf

sudo yum remove nginx -y
sudo yum install nginx -y

ls /etc/nginx/nginx.conf



sudo nano /etc/nginx/nginx.conf

user nginx;
worker_processes auto;

error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    tcp_nopush      on;
    tcp_nodelay     on;
    keepalive_timeout  65;
    types_hash_max_size 2048;

    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        location / {
        }

        error_page 404 /404.html;

        location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;

        location = /50x.html {
        }
    }
}

