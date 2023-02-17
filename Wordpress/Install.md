# Установка `WordPress`
## Создадим и настроим базу данных для сайта при помощи mariadb:
### 1. Настроим доступ к базе для пользователей:
```
CREATE DATABASE wp_database;
```
```
GRANT ALL ON wp_database.* TO 'wp_user'@'localhost' IDENTIFIED BY 'YOUR_PASSWORD' WITH GRANT OPTION;
```
## **`YOUR_PASSWORD` - пароль к базе данных**

## Устанавливаем `WordPress`:
### 1. Переходим в директорию с сайтом:
```
cd /home/main/cloudblesk.site/www/cloudblesk.site/html
```
### 2. Скачиваем архив
```
sudo wget https://ru.wordpress.org/latest-ru_RU.zip
```
### 3. Распаковываем:
```
sudo unzip latest-ru_RU.zip
```
### 4. Скопируем файлы конфигурации:
```
sudo cp wp-config-sample.php wp-config.php
```
### 5. Отредактируем файл конфигурации:
```
sudo nano wp-config.php
```
### 6. Вписываем имя пользователя `[wp_user]` и пароль `[YOUR_PASSWORD]`

<img src="https://github.com/Z0DEN/images/blob/fc890ea51a134a472c217c1915d27b2ef24a29de/wordpress/wp-config.png" width="65%" height="65%"/>

### 7. Выдадим права на папку пользователю `www-data`:
```
sudo chown www-data:www-data -R ./wordpress/
```
### Проверяем:
```
ls -la
```
<img src="https://github.com/Z0DEN/images/blob/9bc7409145c176c1451da2154b1af48354483956/wordpress/www-data-check.png" width="65%" height="65%"/>

## Создадим виртуальный хост для нашего сайта:
### 1. Перейдем в директорию `sites-available`
```
cd /home/main/cloudblesk.site/sites-available/cloudblesk.site
```
### 2. Создадим конфиг для нашего сайта:
```
sudo nano wp.conf
```
### Вставляем:
```
server {
    server_name world-itech.ru;
    root /home/main/cloudblesk.site/www/cloudblesk.site/html/wordpress;
    index index.php;

    location ~* ^.+\.(ogg|ogv|svg|svgz|eot|otf|woff|mp4|ttf|rss|atom|jpg|jpeg|gif|png|ico|zip|thz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf|)$ {
        access_log off;
        log_not_found off;
    }

    location / {
        try_files $uri #uri/ /index.php?$args;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        include snippents/fastcgi-php.conf;
        fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```