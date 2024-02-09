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

