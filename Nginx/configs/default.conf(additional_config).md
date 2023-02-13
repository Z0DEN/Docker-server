# Дополнительный конфиг `Nginx`
## [`Инструкция по установке`](https://github.com/Z0DEN/Docker-server/blob/f391ae5fe7253c09cb99b5916a186bb8307ed612/Nginx/Installation.md#L100-L213)
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