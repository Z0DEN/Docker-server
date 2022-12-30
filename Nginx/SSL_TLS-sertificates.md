# Добавление SSL/TLS сертификатов на сайт.
### Генерация SSL ключ
```
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```
### Создадим папку для сниппетов
```
cd /home/BlesK/server_to_clone/nginx
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
# Устанавливаем `sertbot`