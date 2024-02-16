## 🐘 PostgreSQL

### Возможные ошибки

#### Настройка кодировки

Ошибка у вас может проявиться как при разворачивание дампа бд

```sh
root@vm2601525:~# pg_restore -Fc -d "postgresql://xx:G88Ev6364w5HQ4PK@127.0.0.1:5432/xx" d
b.dump
pg_restore: while PROCESSING TOC:
pg_restore: from TOC entry 4222; 0 24729 TABLE DATA events xx
pg_restore: error: COPY failed for table "events": ERROR:  character with byte sequence 0xd0 0x93 in encoding "UTF8" has no equivalent in encoding "LATIN1"
CONTEXT:  COPY events, line 1
pg_restore: from TOC entry 4216; 0 16404 TABLE DATA parties xx
pg_restore: error: COPY failed for table "parties": ERROR:  character with byte sequence 0xd0 0x93 in encoding "UTF8" has no equivalent in encoding "LATIN1"
CONTEXT:  COPY parties, line 4
pg_restore: warning: errors ignored on restore: 2
```

[stackoverflow#14525505](https://stackoverflow.com/questions/14525505/postgres-issue-encoding-utf8-has-no-equivalent-in-encoding-latin1)

так и при попытке создать бд в нужной кодировке

```sql
postgres=# CREATE DATABASE databasename OWNER xx ENCODING = 'UTF8';
ERROR:  encoding "UTF8" does not match locale "en_US"
DETAIL:  The chosen LC_CTYPE setting requires encoding "LATIN1".
```

[evileg#2](https://evileg.com/ru/post/2/)

решается пересозданием шаблона который используется для создания баз данных

```sql
UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';
DROP DATABASE Template1;
CREATE DATABASE template1 WITH owner=postgres ENCODING = 'UTF-8' lc_collate = 'en_US.utf8' lc_ctype = 'en_US.utf8' template template0;
UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1';
```
