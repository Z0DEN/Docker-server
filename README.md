# Сервис облачного хранилища на фреймворке Django (README ФАЙЛ ДАВНО НЕ АКТУАЛЕН, ГОТОВЫЙ КОД ПРОЕКТА А ТАКЖЕ ПРЕЗЕНТАЦИЮ МОЖНО ПОСМОТРЕТЬ ПО ССЫЛКАМ НИЖЕ)
репозитории проекта: [main server](https://github.com/Z0DEN/myproject), [node server](https://github.com/Z0DEN/node_backend) 
[pdf презентация](https://github.com/Z0DEN/Docker-server/blob/main/cloud.pdf)
## Задачи/мини цели:
## ⚡ Использовать фреймворк Django для серверной реализации фукнций доступных по API(обезопасить доступ при помощи json web token)
## ⚡ Добится легкой масштабируемости и развертки при помощи Docker(внутри контейнеров запускать supervisor с процессами: nginx, redis, django)
## ⚡ Изначально в качестве базы данных планировалось использовать MySQL, в последствии перешел на PostgreSQL
## ⚡ Для обработки запросов и шифрования ssl/tls использовать веб-сервер Nginx
## ⚡ Для оптимизации запросов хранить токены в ОЗУ(Redis)

## Операционная система - Linux antiX (amd64) на Debian 11
## Установка необходимых пакетов:
```
sudo apt-get update && sudo apt-get install -y $(jq -r '.packages | keys | .[]' ~/repo-to-clone/requirements.JSON)
```
# Порядок выполнения
## Docker
### 1. [installation](https://github.com/Z0DEN/Docker-server/blob/7415bd16205cb48d3fb8d2251f67af9a511abe7e/Docker/Installation.md#L1)
## Nginx
### 1. [installation](https://github.com/Z0DEN/Docker-server/blob/7415bd16205cb48d3fb8d2251f67af9a511abe7e/Nginx/Installation.md#L14)
### 2. [setup](https://github.com/Z0DEN/Docker-server/blob/7415bd16205cb48d3fb8d2251f67af9a511abe7e/Nginx/Setup.md)
### 3. [SSL/TLS-sertificate](https://github.com/Z0DEN/Docker-server/blob/main/Nginx/SSL_TLS-sertificates.md)
### Mysql
### 1. [installation](https://github.com/Z0DEN/Docker-server/blob/main/MariaDB/Install.md)
## PHP
### 1. [installation](https://github.com/Z0DEN/Docker-server/blob/main/PHP/Install.md)
# Конфиги
## Docker
## Nginx
### ⚡ [nginx.conf(main_config)](https://github.com/Z0DEN/Docker-server/blob/daeb39d3690642f73307d3f726a1a2554e436ad3/Nginx/configs/nginx.conf(main_config).md)  
### ⚡ [default.conf(additional_config)](https://github.com/Z0DEN/Docker-server/blob/daeb39d3690642f73307d3f726a1a2554e436ad3/Nginx/configs/default.conf(additional_config).md)  
### ⚡ [site-configuration](https://github.com/Z0DEN/Docker-server/blob/daeb39d3690642f73307d3f726a1a2554e436ad3/Nginx/configs/site-configuration.md)  
### ⚡ [index.html](https://github.com/Z0DEN/Docker-server/blob/daeb39d3690642f73307d3f726a1a2554e436ad3/Nginx/configs/site-configuration.md)
### ⚡ [SSL/TLS-sertificate](https://github.com/Z0DEN/Docker-server/blob/main/Nginx/SSL_TLS-sertificates.md)
## MysqL
