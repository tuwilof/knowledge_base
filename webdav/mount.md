## 🌩 WebDAV

### Примонтировать WebDAV

Источник
https://blog.xenot.ru/connect-yadisk-ubuntu-webdav-davfs2.fuck

```sh
sudo apt install -y davfs2
mkdir /mnt/yandex.disk
mount -t davfs https://webdav.yandex.ru /mnt/yandex.disk/
cd /mnt/yandex.disk/
ls -la
df -h /mnt/yandex.disk/
```

отменить
```sh
umount /mnt/yandex.disk/
```

https://manpages.ubuntu.com/manpages/bionic/man8/umount.8.html

### Автоматическое монтирование после перезагрузки виртуальной машины

Добавьте строки в конце файла

```sh
sudo vim /etc/davfs2/secrets
```

```
https://webdav.yandex.ru user pass
```

```sh
sudo vim /etc/fstab
```

```
https://webdav.yandex.ru   /mnt/yandex.disk   davfs   rw,users,_netdev    0   0
```

проверьте после перезагрузки

```sh
cd /mnt/yandex.disk/
ls -la
df -h /mnt/yandex.disk/
```
