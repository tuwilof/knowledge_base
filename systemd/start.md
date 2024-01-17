## 🔧 Systemd

### Как настроить запуск через systemctl

Создадим два файла xx.target и xx-web.service с такими содержимыми

для xx.target
```sh
[Unit]
Description=Run xx
Requires=xx-web.service

[Install]
WantedBy=multi-user.target

```

для xx-web.service
```sh
[Unit]
Description=xx service
After=syslog.target network.target
PartOf=xx.target

[Service]
WorkingDirectory=/opt/xx_backend/current
User=deployer
StandardOutput=journal
StandardError=journal
ExecStart=/home/deployer/.rbenv/bin/rbenv exec bundle exec puma -b unix:///opt/xx_backend/current/tmp/puma.sock

[Install]
WantedBy=xx.target
```
[https://gist.github.com/arteezy/5d53d99f6ee617fae1f0db0576fdd418]

закидываем их на сервер по пути `/usr/lib/systemd/system/`

в папке `/etc/systemd/system/`
создаем папку `xx-web.service.d`
а в ней создаем файл `override.conf`
с содержимым
```sh
[Service]
Environment=RAILS_ENV=production
```

запускаем и проверяем
```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo systemctl start xx.target
ubuntu@ubuntu-std2-1-1-10gb:~$ systemctl | grep party
  xx-web.service                                                      loaded active running   xx service
  xx.target                                                           loaded active active    Run xx
```