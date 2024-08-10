## 🍀 Node

### JSON

```js
let jsonObject = JSON.parse(line);
console.log(typeof jsonObject);
for (let key in jsonObject) {
  if (jsonObject.hasOwnProperty(key)) {
    console.log(`ч: ${key}, Значение: ${jsonObject[key]}`);
  }
}
```