# Установка
### По умолчанию `Memcached` доступен в базовых репозиториях Debian 11
```
sudo apt install memcached libmemcached-tools
```
### Проверяем статус `Memcached`:
```
sudo service memcached status
```

<img src="https://github.com/Z0DEN/images/blob/8aaae550e409fc059f80099d8b2d09e4ced307d0/Memcached/memcached.png" width="65%" height="65%"/>

### Изменим конфигурацию `Memcached`
```
sudo nano /etc/memcached.conf
```
⚡ Заменим`-l 127.0.0.1` фактическим IP-адресом сервера:

<img src="https://github.com/Z0DEN/images/blob/af057037c61e247e84121f125ffc73c3c0108668/Memcached/memcached-conf.png" width="65%" height="65%"/>

⬇⬇⬇⬇⬇⬇

<img src="https://github.com/Z0DEN/images/blob/af057037c61e247e84121f125ffc73c3c0108668/Memcached/memcached-conf-after.png" width="65%" height="65%"/>

### Сохраняем файл
**`CTRL`** + **`O`**  
**`ENTER`**  
**`CTRL`** + **`X`**

### Перезапускаем `Memcached`
```
sudo service memcached restart
```
### Установим расширение `Memcached`, чтобы использовать его в качестве сиситемы кэширования приложений `PHP`, таких как `Wordpress`
```
sudo apt install php-memcached
```