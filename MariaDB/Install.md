# 1. Установка `Mariadb`
```
sudo apt install mariadb-server mariadb-client
```
# 2. Установка [`php`](https://github.com/Z0DEN/Docker-server/blob/36ec5d6f81312809a421afcd74b1c36ce780d2f8/PHP/Install.md)
# Решение конфликта `MariaDB` и `MySQL`
```
sudo apt remove --purge mysql-server mysql-client mysql-common
```
```
sudo apt autoremove
```
```
sudo apt install mariadb-server
```