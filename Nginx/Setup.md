# Вебсайт
## `cloudblesk.site - домен моего сайта, его меняете на свой.`
# Расположение
### 1. Клонируем репозиторий Github или сами создаём папку для сайта:

```
git clone https://github.com/Z0DEN/cloudblesk.site.git
```
### или
```
mkdir cloudblesk.site
cd cloudblesk.site
```
```
mkdir -p sites-available/cloudblesk.site sites-enabled www/html
```
⚡ `sites-available` - для конфига сайтов  
⚡ `sites-enabled`- для символьной ссылки - удобное включение и выключение нужных сайтов  
⚡ `www` - для самого сайта
# Сайт
### 1. Создаём index.html файл сайта

```
sudo nano /home/main/cloudblesk.site/www/cloudblesk.site/html/index.html
```
### 2. Вписываем в него следующее:
```
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
<meta charset="utf-8">
<title>Welcome to cloudblesk.site</title>
</head>
<body>
<h1>Success! cloudblesk.site home page!</h1>
</body>
</html>
```
### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### 3. Создадим конфигурационный файл сайта
```
sudo nano /home/main/cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf
``` 
### 4. Вписываем в него следующее:
```
server {
listen 80;
listen [::]:80;

server_name cloudblesk.site www.cloudblesk.site;
root /home/main/cloudblesk.site/www/cloudblesk.site/html;
index index.html index.php index.xml;
}
```

### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### 5. Создадим символьную ссылку для включения конфига:
```
sudo ln -s /home/main/cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf /home/main/cloudblesk.site/sites-enabled/
```
### 6. Проверяем конфиг nginx
```
sudo nginx -t
```
# Файл конфига `default.conf`
```
mkdir repo-to-clone
```
```
sudo mv /etc/nginx/conf.d/default.conf /home/main/repo-to-clone/nginx/config/
nano repo-to-clone/nginx/config/default.conf
```

### 1. Настроим `default.conf`:
```
server {
listen       80;
server_name  localhost;

#access_log  /var/log/nginx/host.access.log  main;

location / {
root   home/main/cloudblesk.site/www/cloudblesk.site/html;
index  index.html index.php index.htm;
}

#error_page  404              /404.html;

# redirect server error pages to the static page /50x.html
#
error_page   500 502 503 504  /50x.html;
location = /50x.html {
root    home/main/cloudblesk.site/www/cloudblesk.site/error_pages/*;
}
# proxy the PHP scripts to Apache listening on 127.0.0.1:80
#
#location ~ \.php$ {
#    proxy_pass   http://127.0.0.1;
#}

# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
#location ~ \.php$ {
#    root           html;
#    fastcgi_pass   127.0.0.1:9000;
#    fastcgi_index  index.php;
#    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
#    include        fastcgi_params;
#}

# deny access to .htaccess files, if Apache's document root
# concurs with nginx's one
#
#location ~ /\.ht {
#    deny  all;
#}
}
```