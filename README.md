```
# Proxy requests to the application server
    location / {
        proxy_pass http://0.0.0.0:3000/;  # Ensure this points to your application's correct address and port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
