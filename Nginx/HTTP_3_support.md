# Добавление поддержки HTTP/3 в `Nginx`
### Скачиваем `mercurial` для клонирования репозитория `QUIC`
```
sudo apt-get install mercurial
```
### Переходим в папку с исходниками `Nginx`
```
cd /usr/local/nginx
```
### Клонируем репозиторий
```
sudo hg clone -b quic https://hg.nginx.org/nginx-quic
```
### перезаписать содержимое каталога с исходниками `Nginx` файлами из `nginx-quic`
```
sudo rsync -r nginx-quic/ nginx-1.23.4/
```
## Добавление `QUIC` в исходники
```
cd /usr/local/nginx/nginx-1*/
sudo nano debian/rules
```
### нас интересуют 2 секции этого файла: 
1. config.status.nginx: config.env.nginx 
2. config.status.nginx_debug: config.env.nginx_debug
### Перед `--with-cc-opt="$(CFLAGS)"` добавить:
```
--with-http_v3_module --with-stream_quic_module
```
### После `--with-ld-opt="$(LDFLAGS)"` добавить:
```
--with-cc-opt="-I../modules/libressl/include $(CFLAGS)" --with-ld-opt="-L../modules/libressl/build/ssl -L../modules/libressl/build/crypto $(LDFLAGS)"
```
## Возвращаемся в Installation
