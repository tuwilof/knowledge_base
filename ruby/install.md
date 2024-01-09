## 💎 Ruby

### Установка rbenv

#### Ubuntu

Вот простой список команд которые необходимо выполнить для Ubuntu 20.04

Перед их выполнением убедитесь в наличии gcc и make, иначе придется проделать всю операцию заново, удалив папку .rbenv и убрав из .bash_profile настройку

```sh
root@vm2540275:~# make

Command 'make' not found, but can be installed with:

apt install make        # version 4.2.1-1.2, or
apt install make-guile  # version 4.2.1-1.2

root@vm2540275:~# gcc

Command 'gcc' not found, but can be installed with:

apt install gcc
```

например нет, устаналиваем
```sh
sudo apt-get install gcc
sudo apt-get install make
```

теперь устанавливаем rbenv
```sh
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
~/.rbenv/bin/rbenv init
```

После нужно пересоздать сессию в bash что бы команда rbenv заработала

https://github.com/rbenv/rbenv

И конечно установим последнюю версию ruby, для этого нужно установить ruby-build

```sh
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

https://github.com/rbenv/ruby-build

Если система голая установим дополнительные пакеты

```sh
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev
```

Так как иначе вывалится ошибка

```sh
Downloading ruby-2.3.3.tar.bz2…
-> https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.3.tar.bz2
Installing ruby-2.3.3…

BUILD FAILED (Ubuntu 14.04 using ruby-build 20161121)

Inspect or clean up the working tree at /tmp/ruby-build.20161127161017.2360
Results logged to /tmp/ruby-build.20161127161017.2360.log

Last 10 log lines:
The Ruby openssl extension was not compiled.
The Ruby readline extension was not compiled.
The Ruby zlib extension was not compiled.
ERROR: Ruby install aborted due to missing extensions
Try running `apt-get install -y libssl-dev libreadline-dev zlib1g-dev` to fetch missing dependencies.

Configure options used:
— prefix=/home/vagrant/.rbenv/versions/2.3.3
LDFLAGS=-L/home/vagrant/.rbenv/versions/2.3.3/lib
CPPFLAGS=-I/home/vagrant/.rbenv/versions/2.3.3/include
```

Убедимся что на машине есть минимум 768Мб оперативной памяти

И теперь установим сами ruby

```sh
rbenv install 3.1.3
```

Тем не менее у меня не выставлялась версия ruby с помощью rbenv

Пришлось в файл .bash_profile еще добавить

```sh
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```

https://stackoverflow.com/questions/10940736/rbenv-not-changing-ruby-version