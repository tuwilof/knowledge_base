## 💎 Ruby

### Установка через apt

Перед установкой deb пакета для Debian Ubuntu, сначала проверьте доступные версии для установки, командой `apt show ruby`
Если у вас как у меня Ubuntu 20.04 то умолчанию будет доступна старая версия

```sh
dima@afishium:~$ apt show ruby
Package: ruby
Version: 1:2.7+1
Priority: optional
Section: interpreters
Source: ruby-defaults
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Ruby Team <pkg-ruby-extras-maintainers@lists.alioth.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 37.9 kB
Provides: irb, rdoc, rubygems
Depends: ruby2.7
Suggests: ri, ruby-dev
Conflicts: ruby-activesupport-2.3, ruby-activesupport-3.2
Breaks: apt-listbugs (<< 0.1.6), rbenv (<= 0.4.0-1), ruby-bootsnap (<< 1.4.6-1), ruby-debian (<< 0.3.8+b3), ruby-switch (<= 0.1.0)
Replaces: irb, rdoc, rubygems
Homepage: https://www.ruby-lang.org/
Task: ubuntu-budgie-desktop
Download-Size: 5,412 B
APT-Sources: http://ru.archive.ubuntu.com/ubuntu focal/main amd64 Packages
Description: Interpreter of object-oriented scripting language Ruby (default version)
 Ruby is the interpreted scripting language for quick and easy
 object-oriented programming.  It has many features to process text
 files and to do system management tasks (as in perl).  It is simple,
 straight-forward, and extensible.
 .
 This package is a dependency package, which depends on Debian's default Ruby
 version (currently v2.7).
```

для установки новой версии нужно найти и подключить репозиторий, например вот

https://debian.pkgs.org/12/debian-main-amd64/ruby3.1_3.1.2-7+deb12u1_amd64.deb.html

