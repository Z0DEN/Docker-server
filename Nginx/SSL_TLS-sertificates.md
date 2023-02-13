# Добавление SSL/TLS сертификатов на сайт.
### Генерация SSL ключ
```
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```
### Создадим папку для сниппетов
```
cd /home/main/repo-to-clone/nginx
mkdir snippets
```
### Создаем сниппет для SSL
```
nano ssl-params.conf
```
```
ssl_session_timeout 1d;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;

ssl_dhparam /etc/ssl/certs/dhparam.pem;

ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
ssl_prefer_server_ciphers off;

add_header Strict-Transport-Security "max-age=63072000" always;
```
# Устанавливаем `certbot`
```
sudo apt-get install certbot python3-certbot-nginx
```
### Выпускаем сертификат
```
sudo certbot certonly --nginx
```
### настроим конфиг сайта
```
nano cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf
```
### Стираем всё
**`CTRL`** + **`del`**  
или  
**`CTRL`** + **`k`**
### Вписываем новый конфиг
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

include /home/BlesK/server_to_clone/nginx/snippets/ssl-params.conf;
}

server {
listen 443 ssl http2;
listen [::]:443 ssl http2;

server_name cloudblesk.site;
root /home/BlesK/cloudblesk.site/www/cloudblesk.site/html;
index index.html index.php index.xml;

ssl_certificate /etc/letsencrypt/live/cloudblesk.site/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/cloudblesk.site/privkey.pem;
ssl_trusted_certificate /etc/letsencrypt/live/cloudblesk.site/chain.pem;

include /home/BlesK/server_to_clone/nginx/snippets/ssl-params.conf;
}
```


addilyn.ns.cloudflare.com
phil.ns.cloudflare.com
