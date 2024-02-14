## 🚀 Deploy

### Ручной деплой статики

Для деплоя статики
установим на сервер на Ubuntu вручную, если еще не установленны
по инстуркциям по ссылкам ниже
* [Nginx](../nginx/install.md)
* [Git](../git/install.md)

и создаете на сервере нового пользователя deployer по инструкции [🚀 Deploy > Создаем на сервере нового пользователя deployer](deployer.md)

#### Настройка статики

Предположим что вы уже используете систему контроля версий Git,
и у вас уже есть удаленный репозиторий где размещен код проекта.
Поэтому теперь зайдем на сервер и вытяним код на тачку проекта
для этого подойте каталог `/opt`
а так же лучше сразу сделать подпапку, подпапки:

```sh
root@ubuntu:~$ sudo su deployer
$ bash
deployer@ubuntu:~$ cd /opt
deployer@ubuntu:/opt$ sudo mkdir xx_frontend
deployer@ubuntu:/opt$ sudo chown deployer xx_frontend
deployer@ubuntu:/opt$ cd xx_frontend
deployer@ubuntu:/opt/xx_frontend$ mkdir releases
deployer@ubuntu:/opt/xx_frontend$ cd releases
deployer@ubuntu:/opt/xx_frontend$ git clone --branch master https://gitlab.com/xx/xx_frontend.git /opt/xx_frontend/releases/202401130203
```

и сразу делаем ссылку для приложения
```sh
ln -s /opt/xx_frontend/releases/202401130203 /opt/xx_frontend/current
```


#### Настройка Nginx

Правим файл

для предварительной настройки ssl воспользуйтесь инструкцией [🤖 Nginx > Настройка SSL](../nginx/ssl.md)

```sh
sudo vim /etc/nginx/sites-available/default
```

```lua
server {
        listen 443 ssl;

        ssl_certificate /etc/ssl/xx.crt;
        ssl_certificate_key /etc/ssl/xx.key;

        server_name xx.ru;

        proxy_set_header Host $host;

        location / {
                root /opt/xx_frontend/current/static;
        }
}

server {
        listen 80;

        server_name xx.ru;

        proxy_set_header Host $host;

        location / {
                root /opt/xx_frontend/current/static;
        }
}
```

и перезагружаем nginx

```sh
sudo service nginx restart
```

проверяем в браузере, если домен уже настроили

и проверяем локально curl
```sh
curl -v http://11.22.33.44/notifications -H 'Host: xx.ru'
```
