## 🤖 Nginx

### Установка nginx

#### Ubuntu

```sh
sudo apt-get update
sudo apt-get install nginx
```

Теперь можно проверить в браузере

![Alt text](images/image.png)

#### Если не открывается

То скорее всего у вас закрыт 80 порт
тем более если вы используете облако/хостинг значит в его настройках
можете еще предварительно проверить с самого сервера командой `curl localhost`

```sh
curl localhost

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```