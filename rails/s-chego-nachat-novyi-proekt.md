# С чего начать новый проект

Начнем с установки новой версии Ruby, точнее проверим список свежих

```bash
rbenv install --list-all
```

Незабудьте установить <mark style="color:blue;">bundler</mark>

<pre class="language-bash"><code class="lang-bash"><strong>gem install bundler
</strong></code></pre>

Выводом команды можно ознакомиться подробнее

```bash
rails -h
```

Например так можно создать минимальный бэкенд

```bash
rails new partymatch_backend --api -d postgresql -MCSJT --skip-webpack-install --skip-action-mailbox --skip-action-text --skip-active-job --skip-active-storage --skip-spring --skip-listen --skip-system-test --skip-bootsnap --master  
```
