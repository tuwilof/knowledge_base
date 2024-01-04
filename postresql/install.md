## PostgreSQL

### Установка PostgreSQL на Ubuntu

Набираем команду и соглашаемся на предложения

```sh
sudo apt-get install postgresql
```

набираем

```sh
sudo -u postgres psql template1
```

```sql
ALTER USER postgres with encrypted password 'postgres';
```

```sh
sudo vi /etc/postgresql/9.3/main/pg_hba.conf
```

меняем на
```
local   all         postgres                          trust
```

осталось
```sh
sudo /etc/init.d/postgresql restart
```

Создаем пользователя
```sh
sudo -u postgres createuser xx
```

подключаемся
```sh
psql -U postgres -h localhost
```

и даем права
```sql
ALTER USER xx CREATEDB;
```