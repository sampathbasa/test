```
sudo rm -rf /etc/nginx
sudo rm -rf /var/log/nginx
sudo rm -rf /usr/sbin/nginx
sudo rm -rf /run/nginx.pid
sudo find / -name "nginx" -exec rm -rf {} +
