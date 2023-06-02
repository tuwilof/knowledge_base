# Решение возможных проблем

#### Не удается создать запись в БД

Предположим при попытке создать в базе данных запись с помощью команды `.create!(`, вы сталкиваетесь с ошибкой

```bash
Traceback (most recent call last):
        1: from (irb):29
ActiveRecord::NotNullViolation (PG::NotNullViolation: ERROR:  null value in column "id" of relation "xx" violates not-null constraint)
DETAIL:  Failing row contains (null, xx, xx, 2023-06-01 08:13:16.922629+00, 2023-06-01 08:13:16.922629+00).
: INSERT INTO "xx" ("name", "type", "created_at", "updated_at") VALUES ('xx', 'xx', '2023-06-01 08:13:16.922629', '2023-06-01 08:13:16.922629') RETURNING "id"
```

В целом проблема не редкая

{% embed url="https://github.com/zdennis/activerecord-import/issues/138?ysclid=licsm5jlv3616900093" %}

В моем случае я обнаружил что в проблемной базе была разница

```sql
xx=> \d xx
                   Table "xx"
   Column   |           Type           | Collation | Nullable | Default
------------+--------------------------+-----------+----------+---------
 id         | uuid                     |           | not null |
 name       | character varying        |           | not null |
 type       | character varying        |           | not null |
 created_at | timestamp with time zone |           | not null |
 updated_at | timestamp with time zone |           | not null |
Indexes:
    "xx" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "xx" CONSTRAINT "xx" FOREIGN KEY (xx) REFERENCES xx(id) ON DELETE CASCADE                                                             

```

&#x20;по сравнению с корректной

```sql
xx=> \d xx
                                Таблица "xx"
  Столбец   |           Тип            | Правило сортировки | Допустимость NULL |    По умолчанию    
------------+--------------------------+--------------------+-------------------+--------------------
 id         | uuid                     |                    | not null          | uuid_generate_v4()
 name       | character varying        |                    | not null          | 
 type       | character varying        |                    | not null          | 
 created_at | timestamp with time zone |                    | not null          | 
 updated_at | timestamp with time zone |                    | not null          | 
Индексы:
    "xx" PRIMARY KEY, btree (id)
Ссылки извне:
    TABLE "xx" CONSTRAINT "xx" FOREIGN KEY (xx) REFERENCES xx(id) ON DELETE CASCADE
```

{% embed url="https://stackoverflow.com/questions/39378089/how-do-i-set-a-default-value-for-a-uuid-primary-key-column-in-postgres" %}

Такая команда в `rails console` по итогу советов выше помогла

```ruby
  tables = ActiveRecord::Base.connection.tables - %w(schema_migrations)

  tables.each do |table_name|
    begin
      ActiveRecord::Base.connection.execute("ALTER TABLE #{table_name} ALTER COLUMN id SET DEFAULT uuid_generate_v4();")
    rescue => e
      p " Error -- #{e}"
    end
  end
```

