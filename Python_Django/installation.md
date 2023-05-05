## Установим `Python` последней версии.
```
sudo apt update
```
```
sudo apt install python3-pip python3-dev python3-venv libpq-dev postgresql postgresql-contrib
```
ALTER DATABASE Django_project OWNER TO Django_user;
## Настроим `PostgreSQL`:
```
sudo -u postgres psql
```
```
CREATE DATABASE django_project;
```
```
CREATE USER django_user WITH PASSWORD 'password';
```
```
ALTER ROLE django_user SET client_encoding TO 'utf8';
```
```
ALTER ROLE django_user SET default_transaction_isolation TO 'read committed';
```
```
ALTER ROLE django_user SET timezone TO 'UTC';
```
```
GRANT ALL PRIVILEGES ON DATABASE django_project TO django_user;
```
```
\q
```
### Tеперь настройка Postgres завершена, и Django может подключаться к базе данных и управлять своей информацией в базе данных.
## Обновим `pip`
```
sudo -H pip3 install --upgrade pip
```
## Установим пакет для создания виртуальных сред. (Если версия `Python` < `3.0`)
```
sudo -H pip3 install virtualenv
```
## Создадим каталог для файлов `.py`
```
sudo mkdir Django
```
## Создадим виртуальную среду для нашего каталога

### Для этого перейдем в него
```
cd Django
```
### И создадим виртуальную среду `Python`, где `Django` - название проекта
### Если версия `Python` < `3.0`:
```
sudo virtualenv Django
```
### Если >= `3.0`:
```
sudo python -m venv Django
```

### Таким образом установим локальную версию Python и локальную версию pip.

## Но прежде чем устанавливать требования Python для вашего проекта, вам необходимо активировать виртуальную среду:
```
source Django/bin/activate
```
### Обратите внимание на то, что ваше приглашение командной строки теперь носит префикс вашей среды.
<img src="https://github.com/Z0DEN/images/blob/6126b76fe2c87a6be33f0f3926f41108f524d18c/Django/Django-req.png" width="65%" height="65%"/>

## Установим значение `include-system-site-packages` на `true`:
```
cd Django
```
```
sudo nano pyvenv.cfg
```

## Установим `Django` `Gunicorn` и адаптер `Psycopg`
```
python -m pip install django gunicorn psycopg2-binary
```
## Добавим необходимый `PATH` в `bashrc`:
```
echo 'PATH=$PATH:~/.local/bin' | tee -a ~/.bashrc
```
```
source ~/.bashrc
```
## Теперь у вас есть все программное обеспечение, необходимое для запуска проекта Django.
-------

# Создание и настройка нового проекта Django
### Установив компоненты Python, теперь вы можете создавать фактические файлы проекта Django. Поскольку у вас уже есть каталог проекта, скажите Django, чтобы он установил файлы здесь. Он создаст каталог второго уровня с фактическим кодом, который является нормальным, и поместит в этот каталог сценарий управления. Это важно, потому что вы определяете каталог явно, вместо того, чтобы позволить Django принимать решения относительно вашего текущего каталога:
```
django-admin startproject PROJECT_NAME
```

## 

### В случае проблем может сработать команда:
```
ALTER DATABASE Django_project OWNER TO Django_user;
```

## Изменим настройки проекта
### Найдем папку `settings.py`
```
nano settings.py
```
```
import os
```
```
ALLOWED_HOSTS = ['your_server_domain_or_IP', 'second_domain_or_IP', 'localhost']
```
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'django_project',
        'USER': 'django_user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```
```
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
```
## Находим файл `manage.py`
```
./manage.py makemigrations
```
```
./manage.py migrate
```
## Создадим пользователя адмнистратора
```
./manage.py createsuperuser
```
