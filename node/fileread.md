## 🍀 Node

### Чтение файла

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