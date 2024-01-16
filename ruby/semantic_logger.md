## 💎 Ruby

### Настройка гема rails_semantic_logger

Ставим гем [rails_semantic_logger](https://github.com/reidmorrison/rails_semantic_logger)
```
  gem 'rails_semantic_logger'
```

затем в файле `config/application.rb` прописываем настройки
```css
    config.rails_semantic_logger.format = :json
    config.log_tags = {
      request_id: :request_id,
      service_id: 'your-project-backend-key'
    }
    SemanticLogger.application = 'your-project-backend'

    $stdout.sync = true
    config.rails_semantic_logger.add_file_appender = false
    config.semantic_logger.add_appender(io: $stdout, formatter: config.rails_semantic_logger.format)
```

если используется Puma в cluster mode c несколькими воркерами, то нужно в config/puma.rb добавить
```
on_worker_boot do
  # Re-open appenders after forking the process
  SemanticLogger.reopen
end
```