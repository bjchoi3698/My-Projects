Simple exercise to set up website
1. Static HTML
2. Website Configuration
```
server {
   listen    80;
   server_name $IPADDR;
   
   client_max_body_size 20m;
   
   index index.php index.html index.htm;
   root /var/www/mywebsite;
   
   location / {
      try_files $uri $uri/ /index.html?q=$uri&$args;
   }
   
   location ~* \.(js|css|png|jpg|jpeg|gif|ico|woff|ttf|svg|otf)$ {
      expires 30d;
      add_header Pragma public;
      add_header Cache-Control "public";
      access_log off;
   }
}
```
3. WebServer Configuration
```
user www-data;
worker_processes auto;

pid /run/nginx.pid;

events {
   worker_connnections   1024;
}

http {
   include  mime.types;
   deafault_type   application/octet-stream;
   
   error_log . /var/log/nginx_error.log error;
   
   send_file    on;
   #tcp_nopush  on;
   
   keepalive_timeout 65;
   
   # SSL
   ssl_prototocls TLSv1 TLSv1.2; # no sslv3 (poodle etc.)
   ssl_prefer_server_ciphers on;
   
   # Gzip Settings
   gzip on;
   gzip_disable "msie6";
   gzip_vary one;
   gzip_min_length 512;
   ...
   
}
```

When we deploy,
```
# Copy our website files
cp config/index.html /var/www/mywebsite/
chown root:root /var/www/mywebsite/index.html
chmod 0644 /var/www/mywebsite/index.html

# Remove deafult nginx vhost configuration
rm /etc/nginx/sites-enabled/default

# Start nginx at boot + make sure it's running right now.
service nginx restart
server nginx enable

# On a machine with systemd, you'd use these instead
# systemctl enable nginx
# systemctl restart nginx

```

