## 🍀 Node

### JSON

```js
const fs = require('fs');

let filename = 'log/test.log';

fs.readFile(filename, 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }

    const lines = data.split('\n');
    lines.forEach((line, index) => {
        if (index === lines.length - 1) {
            console.log('Это последняя строка файла, останавливаем парсинг строк, что бы не упасть');
        } else {
            let jsonObject = JSON.parse(line);
            console.log(typeof jsonObject);
            for (let key in jsonObject) {
                if (jsonObject.hasOwnProperty(key)) {
                    console.log(`ч: ${key}, Значение: ${jsonObject[key]}`);
                }
            }
        }
    });
});


```