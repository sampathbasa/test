```
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
