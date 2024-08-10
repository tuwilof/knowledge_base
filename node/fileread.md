## 🍀 Node

### Чтение файла

#### Основное

```js
const fs = require('fs');

let filename = 'log/test.log';

fs.readFile(filename, 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }

  const lines = data.split('\n');

  lines.forEach(line => {
    debugger
    console.log(line);
    // Здесь вы можете добавить свою логику для проверки каждой строки
  });
});
```

#### Конец файла

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
            //...
        }
    });
});
```