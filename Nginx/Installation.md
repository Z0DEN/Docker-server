# Подготовка
## Все конфигурации можно найти здесь:

### Обновим репозитории Linux
```
sudo apt-get update
```
### Устанавливаем необходимые зависимости для сборки  
⚡ Практически всегда для работы программы необходимы определенные ресурсы. Потребность пакета ресурсах, находящихся в других пакетах называют зависимостью этого пакета от другого. Установим необходимые пакеты (зависимости):  
```
sudo apt install dpkg-dev build-essential gnupg2 git gcc cmake libpcre3 libpcre3-dev zlib1g zlib1g-dev openssl libssl-dev curl unzip -y
```
### Добавляем в систему GPG ключ репозитория nginx
⚡ Импортируем официальный ключ, используемый `apt` для проверки подлинности пакетов:
```
sudo mkdir /usr/local/nginx
```
```
cd /usr/local/nginx
sudo wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
```
### Добавим репозиторий Nginx  
⚡ Откроем  файл `/etc/apt/sources.list` в редакторе линукс
```
sudo nano /etc/apt/sources.list.d/nginx.list
```
### Редактируем список репозиториев
⚡ Добавляем в него записи:
```
deb http://nginx.org/packages/mainline/debian/ bullseye nginx
deb-src http://nginx.org/packages/mainline/debian/ bullseye nginx
```
### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Обновляем репозитории
```
sudo apt update -y
```
### Скачиваем исходники Nginx
```
cd /usr/local/nginx
sudo apt-get source nginx
```
### Ставим зависимости для сборки
```
sudo apt build-dep nginx -y
```
### Скачиваем модуль Brotli
```
sudo git clone --recursive https://github.com/google/ngx_brotli.git
```
### Обновляем правила сборки
```
cd /usr/local/nginx/nginx-*/
sudo nano debian/rules
```
### Найдем блоки:
**`config.env.nginx`**  
**`config.env.nginx_debug`**

<img src="https://github.com/Z0DEN/images/blob/07970df939b2923d3783818bab483c012dd1184b/Nginx-installing/blocks.png" width="65%" height="65%"/>

### Добавим новый ключ после каждого `./configure`
```
--add-module=/usr/local/nginx/ngx_brotli
```

<img src="https://github.com/Z0DEN/images/blob/11fc3a569d8eca4d81c677c75940ab36848396b5/Nginx-installing/new-keys.png" width="65%" height="65%"/>

### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Компилируем и собираем Nginx
```
sudo dpkg-buildpackage -b -uc -us
```
### Проверяем **`.deb`** файлы
```
ls /usr/local/nginx/*.deb
```

<img src="https://github.com/Z0DEN/images/blob/59a586935767566e897ddc5d63f2df90670c680c/Nginx-installing/deb-files-check.png" width="65%" height="65%"/>

### Устанавливаем Nginx из deb-файлов
```
sudo dpkg -i /usr/local/nginx/*.deb
```
# Настроим Nginx
### Настроим минимальный конфиг для Nginx
```
sudo nano /etc/nginx/nginx.conf
```
```
user www-data;
worker_processes auto;
pid /var/run/nginx.pid;

events {
worker_connections 1024;
}

include /home/main/cloudblesk.site/sites-enabled/*.stream;

http {

# Virtual Hosts

include /home/main/cloudblesk.site/sites-enabled/cloudblesk.site.conf;

# Configs

include /home/main/repo-to-clone/nginx/config/*.conf;
include /usr/share/nginx/modules/*.conf;

# Basic

sendfile on;
tcp_nopush on;
tcp_nodelay on;
types_hash_max_size 2048;
server_tokens off;
ignore_invalid_headers on;

# Decrease default timeouts to drop slow clients

keepalive_timeout 40s;
send_timeout 20s;
client_header_timeout 20s;
client_body_timeout 20s;
reset_timedout_connection on;

# Hash sizes

server_names_hash_bucket_size 64;

# Mime types

default_type  application/octet-stream;
include /etc/nginx/mime.types;

# Logs

log_format main '$remote_addr - $remote_user [$time_local] "$request" $status $bytes_sent "$http_referer" "$http_user_agent" "$gzip_ratio"';
access_log /var/log/nginx/access.log main;
error_log /var/log/nginx/error.log warn;

# Limits

limit_req_zone  $binary_remote_addr  zone=dos_attack:20m   rate=30r/m;

# Gzip

gzip on;
gzip_disable "msie6";
gzip_vary off;
gzip_proxied any;
gzip_comp_level 5;
gzip_min_length 1000;
gzip_buffers 16 8k;
gzip_http_version 1.1;
gzip_types
application/atom+xml
application/javascript
application/json
application/ld+json
application/manifest+json
application/rss+xml
application/vnd.geo+json
application/vnd.ms-fontobject
application/x-font-ttf
application/x-web-app-manifest+json
application/xhtml+xml
application/xml
font/opentype
image/bmp
image/svg+xml
image/x-icon
text/cache-manifest
text/css
text/plain
text/vcard
text/vnd.rim.location.xloc
text/vtt
text/x-component
text/x-cross-domain-policy;

# Brotli

brotli on;
brotli_comp_level 6;
brotli_types
text/xml
image/svg+xml
application/x-font-ttf
image/vnd.microsoft.icon
application/x-font-opentype
application/json
font/eot
application/vnd.ms-fontobject
application/javascript
font/otf
application/xml
application/xhtml+xml
text/javascript
application/x-javascript
text/$;
}
```
# Переходим к [`Setup`](https://github.com/Z0DEN/Docker-server/blob/faad2e27e4ddd944b8751736b5d02a551d01b6f9/Nginx/Setup.md)

### Проверяем конфиг nginx
```
sudo nginx -t
```
<img src="https://github.com/Z0DEN/images/blob/5a752b0da2abf777c7ece91905c1c051def8117b/Nginx-installing/nginx-t.png" width="65%" height="65%"/>

### Запускаем Nginx
```
sudo service nginx start
```
```
sudo service nginx status
```
### Проверяем Brotli
```
curl -H 'Accept-Encoding: br' -I http://localhost
```
<img src="https://github.com/Z0DEN/images/blob/2759023c6e7f7e89684ea7a8f129f37a6c584ada/Nginx-installing/check_brotli.png" width="65%" height="65%"/>
