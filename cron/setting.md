## ⏰ Cron

### Настройка запуска

Создайте скрипт из инструкции [📇 Bash > Создание и выполнение скрипта](../bash/script.md)
со следующей командой

```sh
date >> /root/test.txt
```

наберите команду
```sh
crontab -e
```

пропишите
```
* * * * * /root/test.sh
```

проверьте
```sh
sudo journalctl -u cron.service --since "3min ago"
```

```sh
tail -f /root/test.txt
```

источник подробнее [losst.pro#nastrojka-cron](https://losst.pro/nastrojka-cron)
