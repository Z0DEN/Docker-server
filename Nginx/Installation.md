# Цель
## Поясняю за Nginx
## Поясняю за Brotli
# Подготовка

### Устанавливаем необходимые зависимости для сборки  
⚡ Практически всегда для работы программы необходимы определенные ресурсы. Потребность пакета ресурсах, находящихся в других пакетах называют зависимостью этого пакета от другого. Установим необходимые пакеты (зависимости):  
```
sudo apt install dpkg-dev build-essential gnupg2 git gcc cmake libpcre3 libpcre3-dev zlib1g zlib1g-dev openssl libssl-dev curl unzip -y
```
### Добавляем в систему GPG ключ репозитория nginx
⚡ Импортируем официальный ключ, используемый `apt` для проверки подлинности пакетов:
```
wget http://nginx.org/keys/nginx_signing.key
apt-key add nginx_signing.key
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
⚡ **CTRL** + **O**  
⚡ **ENTER**  
⚡ **CTRL** + **X**
### Обновляем репозитории
```
sudo apt update -y
```
### Скачиваем исходники Nginx
```
cd /usr/local/src
```

```
apt-get source nginx
```
### Ставим зависимости для сборки
```
apt build-dep nginx -y
```
### Скачиваем модуль Brotli
```
sudo git clone --recursive https://github.com/google/ngx_brotli.git
```
### Обновляем правила сборки
```
cd /usr/local/src/nginx-*/
```

```
sudo nano debian/rules
```
### Найдем блоки:
⚡ `config.env.nginx`  
⚡ `config.env.nginx_debug`  

<img src="https://github.com/Z0DEN/images/blob/14886a35b42aa868de8df230cd91770637c768f5/Nginx-installing/%D0%B1%D0%BB%D0%BE%D0%BA%D0%B8%20%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D0%B0.png" width="65%" height="65%"/>