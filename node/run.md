## 🍀 Node

### Запуск

#### В консоли

```sh
➜  knowledge_base git:(master) ✗ node
Welcome to Node.js v21.7.3.
Type ".help" for more information.
> 1 + 1
2
>
```

#### Файла

test.js
```js
console.log(1+1)
```

```sh
➜  ~ node test
2
```

или просто

```sh
➜  ~ node test
2
```

#### Node modules

После установки

```sh
npm install --save markdown-toc
```

можете вызывать так, например
```sh
node_modules/.bin/markdown-toc
node_modules/.bin/markdown-toc -i subscription.md
```