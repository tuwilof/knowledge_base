## 💎 Ruby

### Возможные ошибки

#### Try running .. to fetch missing dependencies.

При ошибке

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

установите дополнительные пакеты

```sh
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev
```

#### line 305: popd: /root: Permission denied

При ошибке

```sh
-> make install
/home/deployer/.rbenv/plugins/ruby-build/bin/ruby-build: line 305: popd: /root: Permission denied

BUILD FAILED (Ubuntu 20.04 on x86_64 using ruby-build 20240119)

You can inspect the build directory at /tmp/ruby-build.20240214225331.517335.1wPlfe
See the full build log at /tmp/ruby-build.20240214225331.517335.log
```

что бы ее не было, перейдите в каталог отличный от `/root`
в домашний каталог пользователя `deployer`

```sh
cd ~
```

https://stackoverflow.com/questions/9951043/rbenv-permission-denied
