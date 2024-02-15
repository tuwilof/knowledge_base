## 💎 Ruby

### Ручной запуск puma без nginx

Воспользуйтесь инструкциями:
* [🕊️ cURL > Установка](../curl/install.md)
* [💻 Tmux > Как установить tmux на Ubuntu](../tmux/install.md)
* [💻 Tmux > Как открыть новое или предыдущее окно](../tmux/comand.md#как-открыть-новое-или-предыдущее-окно)

проверьте запуск
```sh
RAILS_ENV=production bundle e puma -b unix:///opt/xx_backend/current/tmp/puma.sock
```

запросы
```sh
curl -v --unix-socket /opt/xx_backend/current/tmp/puma.sock 'http://api.xx.ru/notifications'
```

логи
```sh
less -R log/production.log
```
