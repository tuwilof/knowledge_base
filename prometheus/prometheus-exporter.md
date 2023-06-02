# Prometheus exporter

Предположим вы используете gem prometheus\_exporter

{% embed url="https://github.com/discourse/prometheus_exporter?ysclid=liea087flk425501836" %}

{% hint style="info" %}
НО! Лучше следить и использовать разные имена, иначе вызов поменяется, а обработка так и будет использовать не та, и как следствие некорректные графики будут!
{% endhint %}

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
