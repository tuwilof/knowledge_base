## Deploy

### Ручной деплой

Для деплоя Ruby приложения на Ubuntu
установим на сервер вручную
по инстуркциям по ссылкам ниже
* [Nginx](../nginx/install.md)
* [Git](../git/install.md)
* [Rbenv](../ruby/install.md)

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

перейдем туда и установим гемы
```sh
root@vm2540275:/opt# cd xx_backend
root@vm2540275:/opt/xx_backend# bundle
```