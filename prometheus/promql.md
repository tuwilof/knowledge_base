# PromQL

При построение графиком будет полезно работать PromQL

{% embed url="https://habr.com/ru/companies/timeweb/articles/562378/" %}

#### Difference

До с командой

```
ruby_tables_dimensions_dimension{job="xx"} 
```

![](<../.gitbook/assets/Снимок экрана 2023-06-02 в 12.19.47.png>)

После команды

```
ruby_tables_dimensions_dimension{job="xx"} 
- ruby_tables_dimensions_dimension{job="xx"} offset 1h
```

![](<../.gitbook/assets/Снимок экрана 2023-06-02 в 12.18.36.png>)
