# Конфиг сайта
## [`Инструкция по установке`](https://github.com/Z0DEN/Docker-server/blob/f391ae5fe7253c09cb99b5916a186bb8307ed612/Nginx/Setup.md)
```
server {
listen 80;
listen [::]:80;

server_name cloudblesk.site www.cloudblesk.site;
root /home/BlesK/cloudblesk.site/www/cloudblesk.site/html;
index index.html index.php index.xml;
}
```