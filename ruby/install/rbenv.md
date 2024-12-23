## 💎 Ruby

### Установка через rbenv

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
sudo apt-get update
sudo apt-get install -y gcc
sudo apt-get install -y make
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

установите последнюю версию ruby, для этого нужно установить ruby-build

```sh
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

https://github.com/rbenv/ruby-build

установите дополнительные пакеты, если система новая

```sh
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev
```

так как иначе будет ошибка [💎 Ruby > Возможные ошибки > Try running .. to fetch missing dependencies](./emergency.md#try-running--to-fetch-missing-dependencies)

установите сами ruby, предварительно убедитесь что на машине есть минимум 768Мб оперативной памяти

перейдите в домашний каталог, во избежание ошибке [💎 Ruby > Возможные ошибки > line 305: popd: /root: Permission denied](./emergency.md#line-305-popd-root-permission-denied)

```sh
cd ~
time rbenv install 3.1.3
```

операция долгая, у меня выполнялась 18 минут

тем не менее у меня не выставлялась версия ruby с помощью rbenv

```sh
ubuntu@ubuntu-std2-1-1-10gb:~$ rbenv global 3.1.3
ubuntu@ubuntu-std2-1-1-10gb:~$ ruby -v
Command 'ruby' not found, but can be installed with:
sudo snap install ruby  # version 3.3.0, or
sudo apt  install ruby  # version 1:3.0~exp1
See 'snap info ruby' for additional versions.
```

пришлось в файл `.bash_profile` или `.bashrc` еще добавить

```sh
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```

https://stackoverflow.com/questions/10940736/rbenv-not-changing-ruby-version

в новой сессий стало ок
```sh
sudo su deployer
bash
cd ~
ruby -v
```

потом по идеи уже версию не надо устанавливать, хотя если еще не делали можно проверить

установим гем bundler
```sh
gem install bundler
```