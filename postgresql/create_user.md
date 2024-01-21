## 🐘 PostgreSQL

### Создание пользователя
Подключаемся
```sh
psql -U postgres -h localhost
```

cоздаем пользователя
```sql
CREATE USER username;
```

даем права
```sql
ALTER USER username CREATEDB;
```

создаем бд
```sql
CREATE DATABASE databasename;
```

меняем пароль
```sql
ALTER USER username WITH PASSWORD 'password';
```

можете проверить
```sh
psql -U username -h localhost
```