## 🤖 Nginx

### Проксирование

Устанавлиаем nginx если еще не устанлвен по инструкци [🤖 Nginx > Установка nginx](./install.md)

правим командой

```sh
sudo vim /etc/nginx/sites-available/default
```

важно если используете 443 то надо и сертификаты тоже использовать при проксирование
как в инструкции [🤖 Nginx > Настройка SSL](./ssl.md)

```
server {
        listen 443 ssl;

        ssl_certificate /etc/ssl/xx.crt;
        ssl_certificate_key /etc/ssl/xx.key;

        server_name api.xx.ru;

        proxy_set_header Host $host;

        location / {
                proxy_pass http://11.22.33.44;
        }
}
```

перезагружаем nginx

```sh
sudo service nginx restart
```

проверяем сервис и логи

```sh
root@vm2601525:~# ls -la /var/log/nginx/
total 20
drwxr-xr-x  2 root     adm     4096 Feb 13 23:31 .
drwxrwxr-x 10 root     syslog  4096 Feb 13 23:31 ..
-rw-r-----  1 www-data adm    10798 Feb 13 23:54 access.log
-rw-r-----  1 www-data adm        0 Feb 13 23:31 error.log
root@vm2601525:~# less -R /var/log/nginx/access.log 
```

если правки предварительные то можете локально поправить
```sh
sudo vim /etc/hosts 
```

```
55.66.77.88 api.xx.ru
```