# Импорт и экспорт Dashboard

Для случаев когда&#x20;

* хочется сделать бекап изменений на дашбордах Grafana,&#x20;
* а так же после проверки на стейджинге их продублировать для другого окружения, например прода&#x20;

полезны инструменты импорта и экспорта в виде json в репку проекта.

Рассмотрим пример с использованием утилиты [https://software.es.net/gdg/docs/](https://software.es.net/gdg/docs/)\
Его достоинство в том что он умеет работать с grafana\_api\_key и grafana\_service\_accounts\_token

<mark style="color:blue;">**Makefile**</mark>

```makefile
.PHONY: pull_grafana_staging
pull_grafana_staging:
    docker run -it --rm --env GDG_CONTEXTS__STAGING__TOKEN="$(shell EDITOR=cat bundle exec rails credentials:edit | grep 'grafana_service_accounts_token' | cut -d ':' -f2 | tr -d ' ')" -v $(abspath .)/grafana/conf:/app/conf -v $(abspath .)/grafana/exports:/app/exports ghcr.io/esnet/gdg:latest dashboards import
 
.PHONY: push_grafana_staging
push_grafana_staging:
    docker run -it --rm --env GDG_CONTEXTS__STAGING__TOKEN="$(shell EDITOR=cat bundle exec rails credentials:edit | grep 'grafana_service_accounts_token' | cut -d ':' -f2 | tr -d ' ')" -v $(abspath .)/grafana/conf:/app/conf -v $(abspath .)/grafana/exports:/app/exports ghcr.io/esnet/gdg:latest dashboards export
```

<mark style="color:blue;">**grafana/conf/importer.yml**</mark>

```yaml
context_name: staging
contexts:
    staging:
        output_path: exports
        token: test
        url: https://grafana.xx.io
        watched:
            - XX
global:
    debug: true
    ignore_ssl_errors: false
loglevel: debug
```

{% hint style="info" %}
Может возникнуть проблема с алертами после импорта, или то что графики не отображаются. Возможная причина то что слетели uid базы и алертов. Их можно синхронизировать выгрузив с помощью gdg и поправив вручую все uid
{% endhint %}
