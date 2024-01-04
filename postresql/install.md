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

создаем бд
```sql
CREATE DATABASE xx;
```

меняем пароль
```sql
ALTER USER xx WITH PASSWORD 'xx';
```

можете проверить
```sh
psql -U xx -h localhost
```

Если используете PostGIS то еще
нужно установить для Ubuntu 20.04
```sh
sudo apt-get install postgis postgresql-12-postgis-3
```

и подключиться
```sh
root@vm2540275:/opt/partymatch_backend# psql -U postgres -h localhost
```

и выполнить
```sql
CREATE EXTENSION postgis;
```

в теории потом должно помочь, но тут что то не так
```sql
GRANT ALL PRIVILEGES ON DATABASE xx TO xx;
GRANT USAGE ON SCHEMA public TO xx;
```

https://stackoverflow.com/questions/61157620/create-extension-postgis-fails
https://stackoverflow.com/questions/22483555/postgresql-give-all-permissions-to-a-user-on-a-postgresql-database

если хотите пока забить то так
```sql
ALTER USER "xx" with SUPERUSER CREATEDB;
```