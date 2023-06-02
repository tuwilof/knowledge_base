# Prometheus

## PromQL

При пострание графиком будет полезно работать PromQL

{% embed url="https://habr.com/ru/companies/timeweb/articles/562378/" %}

#### Difference

До с командой

```
ruby_tables_dimensions_dimension{job="xx"} 
```

![](<.gitbook/assets/Снимок экрана 2023-06-02 в 12.19.47.png>)

После команды

```
ruby_tables_dimensions_dimension{job="xx"} 
- ruby_tables_dimensions_dimension{job="xx"} offset 1h
```

![](<.gitbook/assets/Снимок экрана 2023-06-02 в 12.18.36.png>)

## Prometheus exporter

Предположим вы используете

{% embed url="https://github.com/discourse/prometheus_exporter?ysclid=liea087flk425501836" %}

#### Сравнение gauge и counter

Попробуем через рельс консоль

```
Services.metrics.register(:gauge, "xx", "xx xx").observe(1) 
```

Результат

```
# HELP ruby_xx xx xx
# TYPE ruby_xx gauge
ruby_xx 1
```

Еще раз повторим

```
Services.metrics.register(:gauge, "xx", "xx xx").observe(1)
```

Результат все тот же

```
# HELP ruby_xx xx xx
# TYPE ruby_xx gauge
ruby_xx 1
```

А теперь отправим

```
Services.metrics.register(:gauge, "xx", "xx xx").observe(2)
```

Результат такой

```
# HELP ruby_xx xx xx
# TYPE ruby_xx gauge
ruby_xx 2
```

И еще попробуем

```
Services.metrics.register(:gauge, "xx", "xx xx").observe(1)
```

Результат

```
# HELP ruby_xx xx xx
# TYPE ruby_xx gauge
ruby_xx 1
```

Отправим на этот раз **:counter**

```
Services.metrics.register(:counter, "yy", "yy yy").observe(1)
```

Результат

```
# HELP ruby_yy yy yy
# TYPE ruby_yy counter
ruby_yy 1
```

Повторим

```
Services.metrics.register(:counter, "yy", "yy yy").observe(1)
```

Теперь результат

```
# HELP ruby_yy yy yy
# TYPE ruby_yy counter
ruby_yy 2
```
