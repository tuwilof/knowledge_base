# Метрики

Примеры на Ruby

```ruby
    ActiveRecord::Base.connection.tables.each do |table_name|
      xx(table)
    end
```

#### Количество записей в таблицах

Небольшие объемы

```ruby
sql = 'SELECT COUNT(*) FROM ?'

res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name]).delete("'"))
res.pluck('count').last
```

Большие объемы

```ruby
sql = <<-SQL.squish
 SELECT CASE relpages*pg_relation_size(?)
   WHEN 0 THEN 0
   ELSE (reltuples/relpages*pg_relation_size(?)/8192)::bigint END
 FROM pg_class where relname = ?;
SQL

res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name, table_name, table_name]))
res.pluck('case').last.to_i
```

#### Размеры таблиц

```ruby
sql = 'SELECT pg_total_relation_size(?)'
res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name]))
res.pluck('pg_total_relation_size').last.to_i
```

#### Идентификатор последней записи

{% hint style="info" %}
На случай когда число приблизится к отметки 2\_147\_483\_647 записи перестанут добавляться
{% endhint %}

Соотвественно для случаев когда использует UUID можно настроить их пропуск TABLES\_WITHOUT\_NUMERIC\_ID

```ruby
return 0 if TABLES_WITHOUT_NUMERIC_ID.include?(table_name)

sql = 'SELECT MAX(id) FROM ?'
res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name]).delete("'"))
res.pluck('max').last.to_i
```

#### Период хранения данных в таблицах

Полезно когда хочется уменьшить размер периодическими очистками после анализа

```ruby
def long(table_name)
  return 0 if TABLES_WITHOUT_CREATED_AT.include?(table_name)

  sql = 'SELECT created_at FROM ? ORDER BY created_at ASC LIMIT 1'
  res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name]).delete("'"))
  res.pluck('created_at').last.to_i
end

def recently(table_name)
  return 0 if TABLES_WITHOUT_CREATED_AT.include?(table_name)

  sql = 'SELECT created_at FROM ? ORDER BY created_at DESC LIMIT 1'
  res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, table_name]).delete("'"))
  res.pluck('created_at').last.to_i
end

recently(table) - long(table)
```

Но на старых версиях Ruby так не получится и вместо

```ruby
res.pluck('created_at').last.to_i
```

&#x20;надо делать так

```ruby
Time.new(res.pluck('created_at').last).to_i
```

точнее с учетом негативных кейсов так

```ruby
res.pluck('created_at').last.nil? ? res.pluck('created_at').last.to_i : Time.new(res.pluck('created_at').last).to_i
```

#### Размер базы данных

```ruby
sql = 'SELECT pg_database_size(?)'
database = ActiveRecord::Base.connection.current_database
res = ActiveRecord::Base.connection.execute(ActiveRecord::Base.sanitize_sql_array([sql, database]))
res.pluck('pg_database_size').last.to_i
```
