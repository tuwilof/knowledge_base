## 💎 Ruby

### Про Ruby on Rails

#### Создание нового проекта

Перейдите в нужный каталог для создания
проверьте что установленна корректная версия

```sh
ruby -v
```

по необходимости установите нужную версию

```sh
rbenv versions
rbenv local 3.1.3
ruby -v
```

у Ruby On Rails есть дополнительные настройки при создании проекта

```sh
rails -h
```

пример набора для создание бэкенда

```sh
rails new backend_xx --api -d postgresql -MCSJT --skip-webpack-install --skip-action-mailbox --skip-action-text --skip-active-job --skip-active-storage --skip-spring --skip-listen --skip-system-test --skip-bootsnap
```