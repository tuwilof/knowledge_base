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

#### Работа с моделями и таблицами

##### Создание моделе и таблицу

Выполните генерацию
```sh
bundle e rails g model User 
```

она создат модель и таблицу
```sh
invoke  active_record
create    db/migrate/20240505204541_create_users.rb
create    app/models/user.rb
```

доработайте миграцию, например
```ruby
class CreateUsers < ActiveRecord::Migration[7.1]
  def change
    enable_extension "postgis"
    create_table :users do |t|
      t.integer   :vk_id
      t.string    :state
      t.boolean   :join_group
      t.boolean   :save_favoutire
      t.boolean   :save_display

      t.timestamps
    end
  end
end
```

##### Работа с точками

Добавьте гем в `Gemfile`
```ruby
gem 'activerecord-postgis-adapter'
```

поменяйте адаптер в `database.yml`
```yaml
  adapter: postgis
```

укажите в миграции
```ruby
t.st_point  :point, geographic: true
```

#### Makefile

##### Создание базы

```sh
db_create:
	bundle exec rake db:create --trace
```

##### Выполнение миграций
```sh
db_migrate:
	bundle exec rake db:migrate
	bundle exec rake db:migrate RAILS_ENV=test
	make annotate
```

##### Аннотации
```sh
annotate:
	bundle exec annotate --models
```