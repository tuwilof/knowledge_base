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
      t.datetime  :start_date

      t.timestamps
    end
  end
end
```

выполните [аннотации](#аннотации) если исползуете гем

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

##### Проверка аннотации

```sh
check_annotate:
	bundle exec annotate --models --frozen
```

#### Полезные гемы для проверки на CI

##### annotate

###### Добавления гема annotate

Добавьте гем https://github.com/ctran/annotate_models в `Gemfile`

```ruby
gem 'annotate'
```

выполните команду
```sh
bundle
```

###### Добавления аннотаций в конец модели

Добавьте файл `auto_annotate_models.rake` в папку `lib/tasks/` следующего содержимого 

```sh
if Rails.env.development? || Rails.env.test?
  require 'annotate'

  task set_annotation_options: :environment do
    Annotate.set_defaults(
      position: 'after',

      show_indexes: true,
      simple_indexes: true,
      show_foreign_keys: true,
      show_complete_foreign_keys: false,
      with_comment: true
    )
  end

  Annotate.load_tasks
end
```

выполните [аннотации](#аннотации)

###### Проверка актуальности аннотаций на GitLab CI

Добавьте make команду для [проверки аннотаций](#проверка-аннотации)

и еще команду

```sh
check: check_annotate
```

настройте `database.yml`

```yaml
default: &default
  adapter: postgis
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV.fetch('POSTGRES_USER', '') %>
  password: <%= ENV.fetch('POSTGRES_PASSWORD', '') %>
  host: <%= ENV.fetch('POSTGRES_HOST', 'localhost') %>
  port: <%= ENV.fetch('POSTGRES_PORT', '5432'.to_i) %>
  database: <%= ENV.fetch('POSTGRES_DB_NAME', 'test') %>
```

добавьте такой `.gitlab-ci.yml`

```yaml
default:
  image: ruby:3.1.3

stages:
  - test

variables:
  KUBERNETES_CPU_LIMIT: 4
  KUBERNETES_MEMORY_LIMIT: 8Gi
  KUBERNETES_SERVICE_CPU_LIMIT: 4
  KUBERNETES_SERVICE_MEMORY_LIMIT: 4Gi

test:
  variables:
    POSTGRES_DB: backend_xx_test
    POSTGRES_HOST: postgres
    POSTGRES_USER: postgres
    POSTGRES_PASSWORD: postgres
    POSTGRES_PORT: '5432'
    RAILS_ENV: test
    GITLAB_CI: 'true'
    TZ: 'Europe/Moscow'
    PGTZ: 'Europe/Moscow'
  stage: test
  services:
    - name: postgis/postgis:13-3.1-alpine
      alias: postgres

  cache:
    key: gems
    paths:
      - vendor/ruby
    policy: pull
  before_script:
    - export PATH=$PATH:/usr/local/rbenv/shims
    - gem install bundler
    - bundle install -j $(nproc)
    - make db_reset
  script:
    - make check
  artifacts:
    expire_in: 1 week
    when: always
    reports:
      # cobertura: coverage/coverage.xml
      junit:
        - ./junit/*.xml
```

закомитьте и запушьте правки, билд должен пройти

#### Checklist

- [ ] [добавления гема annotate](#добавления-гема-annotate)
  - [ ] [добавления аннотаций в конец модели](#добавления-аннотаций-в-конец-модели)
  - [ ] [проверка актуальности аннотаций на IC](#проверка-актуальности-аннотаций-на-ci)
