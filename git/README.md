# Git

## Возможно ли иметь разную конфигурацию Git для разных проектов?

https://github.com/direnv/direnv

Каждый `.envrc` должен содержать что-то вроде этого:

```sh
export GIT_CONFIG_GLOBAL=$(pwd)/.gitconfig
```
И `.gitconfig` это обычный gitconfig с желаемыми значениями.

Это то, что у меня есть в пользовательских `.gitconfig` файлах:

```
[include]
    path = ~/.gitconfig

[user]
    email = my.name@company.com
    signingKey = XXXXXXXXXXXXXXXX
```

Перезаписывается только здесь user.email, остальная конфигурация взята из конфигурации по умолчанию `~/.gitconfig`.

https://stackoverflow.com/questions/8801729/is-it-possible-to-have-different-git-configuration-for-different-projects