## 💎 Ruby

### Настройка puma

Что бы не запускать puma явно с передачей параметров
```sh
bundle exec puma -b unix:///opt/xx_backend/current/tmp/puma.sock
```

а запускать лакончино
```sh
bundle exec puma -C config/puma.rb
```

заодно используя указанные настройки

соотвественно поправим сам файл `config/puma.rb`

над строкой
```c
# Specifies the `pidfile` that Puma will use.
pidfile ENV.fetch("PIDFILE") { "tmp/pids/server.pid" }
```

добавляем
```c
APP_PATH = '/opt/xx_backend/current'
bind "unix://#{APP_PATH}/tmp/puma.sock"
```

Передеплоиваем и правим `/usr/lib/systemd/system/xx-web.service`
```sh
ExecStart=/home/deployer/.rbenv/bin/rbenv exec bundle exec puma -C config/xx.rb
```

и перезагружаем
```sh
sudo systemctl daemon-reload
sudo systemctl restart partymatch-web.service
```