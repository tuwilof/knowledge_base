## 🐘 PostgreSQL

### Создание пользователя

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