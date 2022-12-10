# Подготовка

### Обновляем пакеты -  
➥ ca-certificates (цифровой документ заверения ssl сертификатов)  
➥ curl (client URL - программа командной строки, позволяющая взаимодействовать с серверами по протоколам имеющих синтаксис URL)  
➥ gnupg (GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)  
➥ lsb-release (Linux Standard Base release - команда для получения информации о дистрибутиве)  

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

### Создаем папку для хранения ключей

```
sudo mkdir -p /etc/apt/keyrings
```

### Добавляем официальный GPG-ключ Docker  
➥ GPG-ключ (также GnuPG и GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
### Устанавливаем репозиторий

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Обновляем пакеты

```
sudo apt-get update
```

### Ошибка при запуске **apt-get update**?  
➥ Возможно, [umask](https://en.wikipedia.org/wiki/Umask) по умолчанию настроен неправильно, что препятствует обнаружению файла открытого ключа репозитория. Попробуйте предоставить разрешение на чтение для файла открытого ключа Docker перед обновлением индекса пакета:

```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Затем попробуйте команду снова

```
sudo apt-get update
```
# Устанавливаем Docker

### Устанавливаем последнюю версию Docker

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```