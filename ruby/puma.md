## 💎 Ruby

### Настройка puma

Что бы не запускать puma явно с передачей параметров
```sh
bundle exec puma -b unix:///opt/xx_backend/current/tmp/xx.sock
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
APP_PATH = '/opt/xx_backend/current/'
bind "unix://#{APP_PATH}/tmp/puma.sock"
```
