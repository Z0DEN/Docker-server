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
nano cloudblesk.site/www/html/index.html
```
### Вписываем в него следующее:
```
<!DOCTYPE html>
<html lang="ru">
<head>
<title>cloudblesk.site</title>
<meta charset="utf-8">
</head>
<body>
<h1>cloudblesk.site</h1>
</body>
</html>
```
### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Создадим конфигурационный файл сайта
```
nano cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf
``` 
### Вписываем в него следующее:
```
server {
listen 80;
listen [::]:80;

server_name example.site www.example.site;
root /cloudblesk.site/www/cloudblesk.site/html;
index index.html index.xml;
}
```
⚡ Затем обязательно выполняем:  
**`CTRL`** + **`\`**  
```
cloudblesk.site
``` 
**`ENTER`**  
**`Вписываем свой домен`**   
**`ENTER`**

### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Создадим символьную ссылку для включения конфига:
```
ln -s cloudblesk.site/sites-available/cloudblesk.site/cloudblesk.site.conf ~/cloudblesk.site/sites-enabled/
```
### Проверяем конфиг nginx
```
sudo nginx -t
```
# Файлы конфига `Nginx`

# nginx.conf
nano(настройка)
# default.conf
mv  
nano(настройка)