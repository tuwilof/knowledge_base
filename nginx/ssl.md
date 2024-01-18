## 🤖 Nginx

### Настройка SSL

#### Ручная по уже имеющимеся сертификату

Предположим у вас уже есть сертификат

ну сначала надо настроить 443 порт и что бы у вас работали запросы при его отключении

```sh
➜  ~ telnet 11.22.33.44 80 
Trying 11.22.33.44...
Connected to yy.zz.dd.ru.
Escape character is '^]'.
^CConnection closed by foreign host.
```

```sh
➜  ~ telnet 11.22.33.44 443
Trying 11.22.33.44...
telnet: connect to address 11.22.33.44: Connection refused
telnet: Unable to connect to remote host
```

проверим юзается ли порт
```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo apt-get install net-tools
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      552/systemd-resolve 
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      690/nginx: master p 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      675/sshd: /usr/sbin 
tcp6       0      0 :::80                   :::*                    LISTEN      690/nginx: master p 
tcp6       0      0 :::22                   :::*                    LISTEN      675/sshd: /usr/sbin 
udp        0      0 127.0.0.53:53           0.0.0.0:*                           552/systemd-resolve 
udp        0      0 10.0.0.14:68            0.0.0.0:*                           550/systemd-network 
```

правим файл что бы было так

```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo vim /etc/nginx/sites-available/default
```

```c
upstream xx_backend {
        server unix:///opt/xx_backend/current/tmp/puma.sock;
}

server {
        listen 80;
        listen 443;

        server_name api.xx.ru;

        proxy_set_header Host $host;

        location / {
                proxy_pass http://xx_backend;
        }
}
```

перезагружаем
```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo service nginx restart
```

и проверяем
```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ sudo netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1371/nginx: master  
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      717/sshd: /usr/sbin 
tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN      1371/nginx: master  
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      617/systemd-resolve 
tcp6       0      0 :::80                   :::*                    LISTEN      1371/nginx: master  
tcp6       0      0 :::22                   :::*                    LISTEN      717/sshd: /usr/sbin 
udp        0      0 127.0.0.53:53           0.0.0.0:*                           617/systemd-resolve 
udp        0      0 10.0.0.14:68            0.0.0.0:*                           615/systemd-network 
```

```sh
➜  ~ telnet 11.22.33.44 443
Trying 11.22.33.44...
Connected to 179.yy.zz.ru.
Escape character is '^]'.
^CConnection closed by foreign host.
➜  ~ 
```

а теперь првоеряем curl с настройкой без ssl
незабудьте запустить приложение если еще не настроен автозапуск

https://help.reg.ru/support/ssl-sertifikaty/3-etap-ustanovka-ssl-sertifikata/kak-nastroit-ssl-sertifikat-na-nginx

то есь вам надо два файла с сертификатами собрать и закинуть на сервер
your_domain.crt
your_domain.key

```sh
scp your_domain.crt ubuntu@11.22.33.44:~
scp your_domain.key ubuntu@11.22.33.44:~
```

переносим в папку `/etc/ssl/`
```sh
sudo cp your_domain.crt /etc/ssl/
sudo cp your_domain.key /etc/ssl/
```

снова правим
```sh
sudo vim /etc/nginx/sites-available/default
```

```lua
server {
        listen 443 ssl;

        ssl_certificate /etc/ssl/xx.crt;
        ssl_certificate_key /etc/ssl/xx.key;

        server_name api.xx.ru;

        proxy_set_header Host $host;

        location / {
                proxy_pass http://xx_backend;
        }
}
```

перезагружаем
```sh
sudo service nginx restart
```

и если хотите проверить локально то правим на нужный IP в `/etc/hosts`