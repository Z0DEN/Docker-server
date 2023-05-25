# Настройка `Django`
## Настройка поддержки `HTTP/2`
### Установим библиотеку `Daphne`
```
pip install daphne
```
```
cd /home/main/cloudblesk.site/cloud
```
```
sudo nano asgi.py
```
```
import os
from django.core.asgi import get_asgi_application
from daphne import server

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

application = get_asgi_application()

server.run(application, port=8000, interface='127.0.0.1', ssl_keyfile='/etc/letsencrypt/live/cloudblesk.site/privkey.pem', ssl_certfile='/etc/letsencrypt/live/cloudblesk.site/cert.pem')
```
## Создание `Django` приложения
```
python manage.py startapp <APP_NAME>
```
### Настроим общий `urls.py`
```
from django.contrib import admin
from django.urls import path
from django.urls import include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('<APP_NAME>', include('<APP_NAME>.urls')),
]
```
### Настроим `urls.py` приложения <APP_NAME>
```
from django.urls import include
from django.urls import path
from . import views

urlpatterns = [
    path('<FUNCTION_NAME>', views.<FUNCTION_NAME>, name='<FUNCTION_NAME>'),
]
```
## Запустим сервер `Django`
### Без сокета:
```
daphne -b 0.0.0.0 -p 8000 cloud.asgi:application
```
### С сокетом:
```
sudo mkdir /run/daphne
```
```
sudo chown main:main /run/daphne
```
```
daphne -b 0.0.0.0 -p 8000 -u /run/daphne/daphne.sock cloud.asgi:application
```
## Установим Supervisor
### Supervisor - это системный инструмент, который позволяет управлять процессами в фоне, а также автоматически запускать или перезапускать их при необходимости.

```
sudo apt-get update
sudo apt-get install supervisor
```

### Создадим конфигурационный файл для Django приложения
```
sudo nano /etc/supervisor/conf.d/django_app.conf
```
```
[program:my-django-app]

directory=/home/main/cloudblesk.site/cloud/

command=/home/main/.local/bin/daphne --access-log /var/log/daphne/access.log --proxy-headers cloud.asgi:application -b 127.0.0.1 -p 8000

autostart=true
autorestart=true

stderr_logfile=/var/log/my-django-app.err.log
stdout_logfile=/var/log/my-django-app.out.log

user=main
```

### Создадим папки для логов
```
sudo mkdir -p /var/log/daphne
```
```
sudo chmod 777 /var/log/daphne
```

### Перезапустим Supervisor
```
sudo service supervisor restart
```
Проверим его работу
```
sudo supervisorctl status
```
## Использование `uWSGI`
### Установка
```
sudo apt-get install uwsgi
```
```
sudo pip3 install uwsgi
```
### Добавление конфига `uWSGI`
```
sudo nano /etc/uwsgi/apps-available/cloud.ini
```
```
[uwsgi]
chdir = /home/main/cloudblesk.site/cloud
module = cloud.asgi:application
master = true
processes = 4
socket = /run/uwsgi/your_project.sock
chmod-socket = 660
vacuum = true
touch-reload
```
```
sudo ln -s /etc/uwsgi/apps-available/cloud.ini /etc/uwsgi/apps-enabled/cloud.ini
```
```
sudo service uwsgi start
```
### Создадим директорию для хранения `unix-сокета`
```
sudo mkdir -p /run/uwsgi
sudo chown www-data:www-data /run/uwsgi
```
### Добавляем `location` в конфиг сайта
```
    location / {
        include uwsgi_params;
        uwsgi_pass unix:/run/uwsgi/your_project.sock;
    }
```
## Траблшутинг
```
pip install attrs
```
```
pip install twisted
```
```
pip install twisted[http2]
```
