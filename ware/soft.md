## 🍽️ Tools

### Программное обеспечение

#### KeePassXC

* Менеджер паролей
* Open Source
* бесплатно

https://keepassxc.org/

#### Яндекс Браузер

https://browser.yandex.ru/

* бесплатно
* отечественное
* перевод видео на ютубе

#### Яндекс Диск

https://360.yandex.ru/disk/download/

* семейная подписка, до 7 аккаунтов +2Тб памяти
* WebDav из коробки

#### Telegram

https://desktop.telegram.org/

#### ThunderBird

https://www.thunderbird.net/ru/

* много плагинов
* кросплатформенность

#### UnnaturalScrollWheels

Что бы инверсировать срок мыши на маке

https://github.com/ther0n/UnnaturalScrollWheels

#### UTM

https://mac.getutm.app/

Например что бы поднять виртуалку для проверки Ansible

образ Ubuntu можно скачать здесь
https://releases.ubuntu.com/20.04/?C=S;O=D

для корректно работы, при создании важно выбрать именно Эмулировать

так же при установке ресурсов меньше минимальных для Ubuntu тоже будут проблемы установки, да и в целом на минималных все будет довольно медленно, лучше быть внимательным и ставить по минимуму

подробная статья с настройкой
https://losst.pro/ustanovka-ubuntu-server-20-04

далее можно будет подключиться по ssh

сначала надо выяснить IP

наберите в вм
```sh
ip -4 addr
```

будет что то типо
```sh
dima@afishium:~$ ip -4 addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: enp0s1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 192.168.64.4/24 brd 192.168.64.255 scope global dynamic enp0s1
       valid_lft 2316sec preferred_lft 2316sec
```

и соотвественно дальше поэ тому адресу можете подключаться

```sh
➜  ~ ssh dima@192.168.64.4
dima@192.168.64.4's password:
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-200-generic x86_64)
```

https://github.com/utmapp/UTM/discussions/2465#discussioncomment-3868749

#### lt localtunnel

https://github.com/localtunnel/localtunnel

https://youtu.be/z11SoJAmV0U?si=op8OtxCIaW37n1wZ&t=173

