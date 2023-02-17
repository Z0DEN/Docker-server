# Подготовка

### 1. Обновляем пакеты  
⚡ ca-certificates (цифровой документ заверения ssl сертификатов)  
⚡ curl (client URL - программа командной строки, позволяющая взаимодействовать с серверами по протоколам имеющих синтаксис URL)  
⚡ gnupg (GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)  
⚡ lsb-release (Linux Standard Base release - команда для получения информации о дистрибутиве)  

```
sudo apt-get update
```

```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

### 2. Создаем папку для хранения ключей

```
sudo mkdir -p /etc/apt/keyrings
```

### 3. Добавляем официальный GPG-ключ Docker  
⚡ GPG-ключ (также GnuPG и GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### 4. Устанавливаем репозиторий

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 5. Обновляем пакеты

```
sudo apt-get update
```

### Ошибка при запуске `apt-get update`?  
⚡ Возможно, [umask](https://en.wikipedia.org/wiki/Umask) по умолчанию настроен неправильно, что препятствует обнаружению файла открытого ключа репозитория. Попробуйте предоставить разрешение на чтение для файла открытого ключа Docker перед обновлением индекса пакета:

```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Затем попробуем команду снова

```
sudo apt-get update
```

# Устанавливаем Docker

### 1. Устанавливаем последнюю версию Docker-Engine

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Добавим пользователя в группу Docker (необязательно)  
⚡ Выполните этот шаг, если хотите избежать ввода `sudo` при каждом запуске Docker.  
⚡ **Копируем команду, незабывая вместо [USER] вписать своё имя пользовавтеля** 

```
sudo usermod -aG docker [USER]
```

### Чтобы применить новое членство в группе, выйдите из сервера и снова войдите в него или введите следующую команду:  
⚡ **Снова не забываем подставить своё имя пользовавтеля**

```
su - [USER]
```
### Убедимся, что пользователь добавлен в группу `docker`, введя:
```
groups
```
<img src="https://github.com/Z0DEN/images/blob/62307f633191d5b0a0e9dc9f52f23ddfbd292a06/Docker-installing/groups.png" width="65%" height="65%"/>

### 2. Проверим успешность установки, а также актуальность версии Docker  
⚡ **[Последняя версия Docker](https://docs.docker.com/engine/release-notes/)**  

```
docker -v
``` 
# Установка Docker-compose
### 1. Поскольку мы же добавляли ранее [репозитории Docker](#Создаем-папку-для-хранения-ключей) просто скачаем пакет командой

```
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### 2. Проверим успешность установки, а также актуальность версии Docker-compose  
⚡ **[Последняя версия Docker-compose](https://docs.docker.com/compose/release-notes/)**

```
docker-compose -v
```
