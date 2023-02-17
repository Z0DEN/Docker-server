# Конфиг сайта
## [`Инструкция по установке`](https://github.com/Z0DEN/Docker-server/blob/f391ae5fe7253c09cb99b5916a186bb8307ed612/Nginx/Setup.md)

# Без SSL/TLS защиты
```
server {
listen 80;
listen [::]:80;

server_name cloudblesk.site www.cloudblesk.site;
root /home/main/cloudblesk.site/www/cloudblesk.site/html;
index index.html index.php index.xml;
}
```
# SSL/TLS
```
server {
    listen 80;
    listen [::]:80;

    server_name cloudblesk.site www.cloudblesk.site;
    return 301 https://cloudblesk.site$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name www.cloudblesk.site;
    return 301 https://cloudblesk.site$request_uri;

    ssl_certificate /etc/letsencrypt/live/cloudblesk.site/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/cloudblesk.site/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/cloudblesk.site/chain.pem;

    include /home/main/repo-to-clone/nginx/snippets/ssl-params.conf;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name cloudblesk.site;
    root /home/main/cloudblesk.site/www/cloudblesk.site/html;
    index index.html index.php index.xml;

    ssl_certificate /etc/letsencrypt/live/cloudblesk.site/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/cloudblesk.site/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/cloudblesk.site/chain.pem;

    include /home/main/repo-to-clone/nginx/snippets/ssl-params.conf;
}
```