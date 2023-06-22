# Решение возможных проблем

#### unicorn.sock failed (13: Permission denied)

```log
2023/04/25 10:17:21 [crit] 149898#0: *1 connect() to 
unix:/opt/xx/tmp/sockets/unicorn.sock failed 
(13: Permission denied) while connecting to upstream, 
client: xx.xx.xx.xx, 
server: xx.xx.io, 
request: "GET /api/xx/v1/xx HTTP/1.0", 
upstream: "http://unix:/opt/xx/tmp/sockets/unicorn.sock:/api/xx/v1/xx", 
host: "xx.xx.io"
```

Для проверки что дело в SElinux его можно отключить

```bash
sudo setenforce 0
```

Если вам помогло, то дело в том что вас в файле **xx.service** идет вызов без промежуточных скриптов.\
Так как все запускается от процесса **init**, а он сильно ограничен в правах, потому что **init** это процесс который имеет доступ ко всему, поэтому небезопасно так просто давать ему испольнять команды если их каким-то образом взломают.

Отключение **SElinux** это временное решение, чтобы проверить что проблема в **SELinux**, работать на постоянной основе оно не должно. А так же при перезагрузке виртуалки настройка вернется, так как она должна быть всегда.

Корректное решение же заключается в том что нужен промежуточный скрипт.

Соотвественно если в вашем xx.service сейчас такой вызов

```
ExecStart=/usr/local/bin/bundle exec unicorn -c config/unicorn.rb
```

его следует поменять на такой

```
ExecStart=/var/opt/xx/current/start-web.sh
```

ну и соответсвенно завести такой файл со следующим содержимым

```
#!/bin/bash

set -euxo pipefail

/usr/local/bin/bundle exec unicorn -c /var/opt/xx/current/config/unicorn.rb
```















