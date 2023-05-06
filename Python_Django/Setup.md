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