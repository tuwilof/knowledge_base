## 📑 Visual Studio Code

### Настроить запуск в консоли

Предположим вы хотите что бы при наборе команды `code` в терминале открывался проект для этой директории, но у вас ошибка

```sh
➜  ~ code
zsh: command not found: code
```

добавьте в конец вашего файла, например `~/.zshrc`

```sh
export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
```

и можете проверить в консоли корректную работу
```sh
➜  knowledge_base git:(master) ✗ code .
➜  knowledge_base git:(master) ✗
```

Источник: [https://ruslan.rocks/posts/zsh-command-not-found-code]