## 🐘 PostgreSQL

### Установка PostgreSQL на Ubuntu

Набираем команду и соглашаемся на предложения

```sh
sudo apt-get update
sudo apt-get install -y postgresql
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

создаем пользователя по инструкции [🐘 PostgreSQL > Создание пользователя](create_user.md)

Если используете PostGIS то еще
нужно установить для Ubuntu 20.04
```sh
sudo apt-get install -y postgis postgresql-12-postgis-3
```

подключиться по инструкции [🐘 PostgreSQL > Подключение к БД](connect.md)

выполнить
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