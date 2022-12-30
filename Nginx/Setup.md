# Вебсайт
## `cloudblesk.site - домен моего сайта, его меняете на свой.`
# Расположение
### Клонируем репозиторий Github или сами создаём папку для сайта:

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
### Создаём index.html файл сайта

```
sudo nano /home/BlesK/cloudblesk.site/www/cloudblesk.site/html/index.html
```
### Вписываем в него следующее:
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

### Создадим конфигурационный файл сайта
```
sudo nano /home/BlesK/cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf
``` 
### Вписываем в него следующее:
```
server {
listen 80;
listen [::]:80;

server_name cloudblesk.site www.cloudblesk.site;
root /home/BlesK/cloudblesk.site/www/cloudblesk.site/html;
index index.html index.php index.xml;
}
```

### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Создадим символьную ссылку для включения конфига:
```
sudo ln -s /home/BlesK/cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf /home/BlesK/cloudblesk.site/sites-enabled/
```
### Проверяем конфиг nginx
```
sudo nginx -t
```
# Файл конфига `default.conf`
```
mkdir server_to_clone
```
```
sudo mv /etc/nginx/conf.d/default.conf /home/BlesK/server_to_clone/nginx/config/
nano server_to_clone/nginx/config/default.conf
```

### Настроим `default.conf`:
```
server {
listen       80;
server_name  localhost;

#access_log  /var/log/nginx/host.access.log  main;

location / {
root   home/BlesK/cloudblesk.site/www/cloudblesk.site/html;
index  index.html index.php index.htm;
}

#error_page  404              /404.html;

# redirect server error pages to the static page /50x.html
#
error_page   500 502 503 504  /50x.html;
location = /50x.html {
root    home/BlesK/cloudblesk.site/www/cloudblesk.site/error_pages/*;
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