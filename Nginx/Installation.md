# Подготовка
### Устанавливаем необходимые зависимости для сборки  
Практически всегда для работы программы необходимы определенные ресурсы. Потребность пакета ресурсах, находящихся в других пакетах называют зависимостью этого пакета от другого. Установим необходимые пакеты (зависимости):  
```
sudo apt install dpkg-dev build-essential gnupg2 git gcc cmake libpcre3 libpcre3-dev zlib1g zlib1g-dev openssl libssl-dev curl unzip -y
```
### Добавляем в систему GPG ключ репозитория nginx
```
sudo -s
``` 
```
curl -L https://nginx.org/keys/nginx_signing.key | apt-key add -
```