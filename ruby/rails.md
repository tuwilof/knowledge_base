## 💎 Ruby

### Про Ruby on Rails

#### Checklist для идеального нового проекта

- Настройки
  - [ ] [Создать новый проект без лишних зависимостей](#создать-новый-проект-без-лишних-зависимостей)
  - [ ] [Убрать db/schema.rb](#убрать-dbschemarb)
- Гемы
  - [ ] [Добавления гема annotate](#добавления-гема-annotate)
    - [ ] [Добавления аннотаций в конец модели](#добавления-аннотаций-в-конец-модели)
    - [ ] [Проверка актуальности аннотаций на CI](#проверка-актуальности-аннотаций-на-ci)
  - [ ] [Добавления гема rspec-rails](#для-тестирования-rspec-rails)
  - [ ] [Для дебага byebug](#для-дебага-byebug)
  - [ ] [Для проверки style guide rubocop-rails](#для-проверки-style-guide-rubocop-rails)
    - [ ] [Разрешить не замораживать строки](#разрешить-не-замораживать-строки)
  - [ ] [Красивые данные для тестов](#красивые-данные-для-тестов)
- Команды для Makefile
  - [ ] [Создание базы](#создание-базы)
  - [ ] [Выполнение миграций](#выполнение-миграций)
  - [ ] [Аннотации](#аннотации)
  - [ ] [Проверка аннотации](#проверка-аннотации)

#### Советы

По генератору
- [Создание модели и таблицы через генератор](#создание-модели-и-таблицы-через-генератор)
- [Генерация контроллера](#генерация-контроллера)

По работе с бд
- [Создание модели и таблицы через генератор](#создание-модели-и-таблицы-через-генератор)
- [Работа с геоданным](#работа-с-геоданным)

#### Создать новый проект без лишних зависимостей

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

#### Создание модели и таблицы через генератор

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
      t.boolean   :join_group,     default: false
      t.boolean   :save_favoutire, default: false
      t.boolean   :save_display,   default: false
      t.integer   :liked,          default: 0
      t.datetime  :start_date

      t.timestamps
    end
  end
end
```

выполните [аннотации](#аннотации) если исползуете гем

#### Работа с геоданным

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

#### Генерация контроллера

```sh
bundle e rails generate controller user
```

#### Создание базы

```sh
db_create:
	bundle exec rake db:create --trace
```

#### Выполнение миграций

```sh
db_migrate:
	bundle exec rake db:migrate
	bundle exec rake db:migrate RAILS_ENV=test
	make annotate
```

#### Аннотации

```sh
annotate:
	bundle exec annotate --models
```

#### Проверка аннотации

Вариант 1

Сначала вызвать аннотации, а затем проверить

```sh
check_annotate:
	git diff --exit-code app/models
```

Вариант 2

Сразу проверить без вызова

```sh
check_annotate:
	bundle exec annotate --models --frozen
```

#### Добавления гема annotate

Добавьте гем https://github.com/ctran/annotate_models в `Gemfile`

```ruby
gem 'annotate'
```

выполните команду
```sh
bundle
```

#### Добавления аннотаций в конец модели

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

#### Проверка актуальности аннотаций на GitLab CI

Добавьте make команду для [проверки аннотаций](#проверка-аннотации)

Вариант 1 хорош тем что можно добавить вызов аннотаций при вызове миграций, и тогда не будете забывать вызывать аннотации

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

#### Для тестирования rspec-rails

Добавьте в `Gemfile` https://github.com/rspec/rspec-rails

```ruby
gem 'rspec-rails'
```

и настройте

```sh
rails generate rspec:install
```

#### Для дебага byebug

```ruby
gem 'byebug'
```

#### Для проверки style guide rubocop-rails

Установка
```ruby
gem 'rubocop-rails'
```

автофрматирование
```sh
bundle e rubocop -A
```

сгенерировать файл со скипами того что не отавтоформатировать
```sh
bundle e rubocop --auto-gen-config
```

#### Разрешить не замораживать строки

Что бы убрать

```ruby
frozen_string_literal: true
```

```yaml
# Разрешить не замораживать строки.
Style/FrozenStringLiteralComment:
  EnforcedStyle: never
```

```sh
bundle e rubocop -A
```


#### Красивые данные для тестов

```ruby
gem 'factory_bot_rails'
```

#### Убрать db/schema.rb

Добавить в `config/application.rb` строку

```ruby
config.active_record.dump_schema_after_migration = false
```
