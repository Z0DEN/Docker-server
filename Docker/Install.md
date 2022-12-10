Обновляем пакеты -
ca-certificates (цифровой документ заверения ssl сертификатов)
curl (client URL - программа командной строки, позволяющая взаимодействовать с серверами по протоколам имеющих синтаксис URL)
gnupg (GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)
lsb-release (Linux Standard Base release - команда для получения информации о дистрибутиве)

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

Создаем папку для хранения ключей

```
sudo mkdir -p /etc/apt/keyrings
```

Добавляем официальный GPG-ключ Docker
GPG-ключ (также GnuPG и GNU Privacy Guard - инструмент шифрования и создания цифровых подписей)

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
