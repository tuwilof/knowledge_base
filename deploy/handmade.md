## 🚀 Deploy

### Ручной деплой

Для деплоя Ruby приложения
установим на сервер на Ubuntu вручную
по инстуркциям по ссылкам ниже
* [Nginx](../nginx/install.md)
* [Git](../git/install.md)
* [Rbenv](../ruby/install.md)

#### Настройка Rails
Установим гем bundler
```
gem install bundler
```

Предположим что вы уже используете систему контроля версий Git,
и у вас уже есть удаленный репозиторий где размещен код проекта.
Поэтому теперь зайдем на сервер и вытяним код на тачку проекта
для этого подойте каталог `/opt`:

```sh
root@vm2540275:~# cd /opt
root@vm2540275:/opt# git clone git@gitlab.com:xx/xx_backend.git
```

прежде чем устанавливать гемы, могут понадобиться зависимости
например для корректной установки гема `psych` надо установить
```sh
sudo apt-get install libyaml-dev
```

а для гема `pg` 
```sh
sudo apt-get install libpq-dev
```

для гема `unf_ext`
```sh
sudo apt-get install g++
```

перейдем туда и установим гемы
```sh
root@vm2540275:/opt# cd xx_backend
root@vm2540275:/opt/xx_backend# bundle
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
sudo apt-get install curl
```

и tmux
```
sudo apt-get install tmux
```

и через него
```
tmux attach || tmux new
```

Можете проверить
```sh
RAILS_ENV=production bundle e puma -b unix:///opt/xx_backend/tmp/sockets/xx.sock
```

```sh
curl -v --unix-socket /opt/xx_backend/tmp/sockets/xx.sock 'http://api.xx.ru/notifications'
```

и можете проверять логи тут
```sh
less -R log/production.log
```

#### Настройка Nginx

Правим файл
```sh
vim /etc/nginx/sites-available/default
```

```
upstream my_app {
  server unix:///opt/xx_backend/tmp/sockets/xx.sock;
}

server {
        listen 80 default_server;
        listen [::]:80 default_server;

        server_name _;

        location / {
          proxy_pass http://my_app;
        }
```

и перезагружаем nginx

```sh
sudo service nginx restart
```

првоеряем в браузере заглушка пропала

и проверяем локально curl
```sh
curl -v http://185.188.182.36/ 'https://api.xx.ru/notifications'
```