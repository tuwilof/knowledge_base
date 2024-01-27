## 🚀 Deploy

**📔 Оглавление**
* [Ручной деплой Ruby on Rails](#ручной-деплой-ruby-on-rails)
* [Настройка Rails](#настройка-rails)
* [Настройка Nginx](#настройка-nginx)
* [Делаем запуск через Systemd](#делаем-запуск-через-systemd)
* [Повторный деплой](#повторный-деплой)


### Ручной деплой Ruby on Rails

Для деплоя Ruby on Rails приложения
установим на сервер на Ubuntu вручную
по инстуркциям по ссылкам ниже
* [Nginx](../nginx/install.md)
* [Git](../git/install.md)

и создаете на сервере нового пользователя deployer по инструкции [🚀 Deploy > Создаем на сервере нового пользователя deployer](deployer.md)


#### Настройка Rails

Устанавливаем под новым пользователем по инструкции [💎 Ruby > Установка rbenv](../ruby/install.md)

Предположим что вы уже используете систему контроля версий Git,
и у вас уже есть удаленный репозиторий где размещен код проекта.
Поэтому теперь зайдем на сервер и вытяним код на тачку проекта
для этого подойте каталог `/opt`
а так же лучше сразу сделать подпапку, подпапки:
```sh
deployer@ubuntu:~$ cd /opt
deployer@ubuntu:/opt$ mkdir xx_backend
deployer@ubuntu:/opt$ sudo chown deployer xx_backend
deployer@ubuntu:/opt$ cd xx_backend
deployer@ubuntu:/opt/xx_backend$ mkdir releases
deployer@ubuntu:/opt/xx_backend$ cd releases
deployer@ubuntu:/opt/xx_backend/releases$ git clone --branch master https://gitlab.com/xx/xx_backend.git /opt/xx_backend/releases/202401130203
```

и сразу делаем ссылку для приложения
```sh
ln -s /opt/xx_backend/releases/202401130203 /opt/xx_backend/current
```

прежде чем устанавливать гемы, могут понадобиться зависимости
например для корректной установки гема `psych` надо установить
```sh
sudo apt-get install -y libyaml-dev
```

а для гема `pg` 
```sh
sudo apt-get install -y libpq-dev
```

для гема `unf_ext`
```sh
sudo apt-get install -y g++
```

перейдем туда и установим гемы
```sh
deployer@ubuntu:/opt$ cd xx_backend/current
deployer@ubuntu:/opt/xx_backend/current$ bundle
```

Если необходимо PostgreSQL
установим на сервер на Ubuntu вручную
по инстуркциям по ссылке ниже:
* [PostgreSQL](../postgresql/install.md)

Меняем данные для подключения к бд `config/database.yml`
```yaml
production:
  <<: *default
  host: localhost
  database: xx
  username: xx
  password: xx
```

запускаем консоль проекта
```sh
RAILS_ENV=production bundle e rails c
```

выполняем миграции
```sh
RAILS_ENV=production bundle e rails db:migrate
```

надо создать
```sh
vim config/master.key 
```

и прописать там содержимое локального файла из `.gitignore`
```sh
cat config/master.key 
```

Установить curl
```sh
sudo apt-get install -y curl
```

и tmux по инструкции [💻 Tmux > Как установить tmux на Ubuntu](../tmux/install.md)

и через него
```
tmux attach || tmux new
```

Можете проверить
```sh
mkdir /opt/xx_backend/current/tmp
RAILS_ENV=production bundle e puma -b unix:///opt/xx_backend/current/tmp/puma.sock
```

```sh
curl -v --unix-socket /opt/xx_backend/current/tmp/puma.sock 'http://api.xx.ru/notifications'
```

и можете проверять логи тут
```sh
less -R log/production.log
```


#### Настройка Nginx

Правим файл
```sh
sudo vim /etc/nginx/sites-available/default
```

```lua
upstream xx_backend {
        server unix:///opt/xx_backend/current/tmp/puma.sock;
}

server {
        listen 80;

        server_name api.xx.ru;

        proxy_set_header Host $host;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                #try_files $uri $uri/ =404;
                proxy_pass http://xx_backend;
        }
}
```

и перезагружаем nginx

```sh
sudo service nginx restart
```

првоеряем в браузере заглушка пропала

и проверяем локально curl
```sh
curl -v http://11.22.33.44/notifications -H 'Host: my_app'
```


#### Делаем запуск через Systemd

Делаем запуск по инструкци [🔧 Systemd > Как настроить запуск через systemctl](../systemd/start.md)


#### Повторный деплой

После того как запушили в git
заходим на сервер под юзером deployer
```sh
sudo su deployer
bash
```

клонируем в новый каталог
```sh
git clone --branch master https://gitlab.com/xx/xx_backend.git /opt/xx_backend/releases/202401170118
```

переходим туда и ставим гемы
```sh
cd /opt/xx_backend/current
bundle
```

надо создать ключ для секретов
```sh
vim config/master.key 
```

прописать там содержимое локального файла из `.gitignore`
```sh
cat config/master.key 
```

меняем ссылку
```sh
rm /opt/xx_backend/current
ln -s /opt/xx_backend/releases/202401170118 /opt/xx_backend/current
```

перезагружаем nginx
```sh
sudo service nginx restart
```

и сам проект
```sh
sudo systemctl restart xx.target
```

проверям логи для сервиса `xx-web.service` по инструкции [📔 Journalctl > Чтение](../journalctl/read.md)
