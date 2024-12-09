```
# Backend server block
server {
    listen 443 ssl;
    server_name your_backend_domain.com; # Use your backend domain or IP address

    ssl_certificate /path/to/backend_cert.pem; # SSL certificate for backend
    ssl_certificate_key /path/to/backend_key.pem;

    location / {
        proxy_pass http:/0; # Forward requests to backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
    }
}
