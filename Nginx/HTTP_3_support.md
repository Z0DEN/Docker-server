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
## Установка библиотек `SSL` для поддержки сборки `Nginx` с HTTP/3.
### Будем использовать `LibreSSL`
```
sudo wget https://ftp.openbsd.org/pub/OpenBSD/LibreSSL/libressl-3.7.0.tar.gz
```
```
sudo tar -vxf libressl-3.7.0.tar.gz
```
```
cd libressl-3.7.0/
```
```
sudo mkdir build
```
```
cd build
```
```
sudo cmake ../
```
```
sudo make -j 8
```
## Добавление `QUIC` в исходники

