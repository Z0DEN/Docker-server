# Основной конфиг `Nginx`
## [`Инструкция по установке`](https://github.com/Z0DEN/Docker-server/blob/f391ae5fe7253c09cb99b5916a186bb8307ed612/Nginx/Installation.md#L100-L213)
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

include /home/main/cloudblesk.site/sites-enabled/*;

# Configs

include /home/main/server_to_clone/nginx/config/*.conf;
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