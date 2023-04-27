# 1. Установка `Mariadb`
```
sudo apt install mariadb-server mariadb-client
```
# 2. Установка [`php`](https://github.com/Z0DEN/Docker-server/blob/main/PHP/Install.md)
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

1. sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
2. wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
3. sudo apt-get update
4. sudo apt-get -y install postgresql