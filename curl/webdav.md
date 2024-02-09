## 🕊️ cURL

### Работа с WebDAV

Команда загрузки файла
```sh
curl -u user:pass -X PUT https://webdav.yandex.ru/test.txt -d @test.txt -i
```

команда скачивания файла
```sh
curl -u user:pass https://webdav.yandex.ru/test.txt --output test2.txt
```
