## Deploy

### Возможные ошибки

#### Ошибка при установке гема psych

```sh
root@vm2540275:/opt/xx_backend# bundle
..
Installing psych 5.1.0 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/psych-5.1.0/ext/psych
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
checking for yaml.h... no
yaml.h not found
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/root/.rbenv/versions/3.1.3/bin/$(RUBY_BASE_NAME)
	--with-libyaml-source-dir
	--without-libyaml-source-dir
	--with-yaml-0.1-dir
	--without-yaml-0.1-dir
	--with-yaml-0.1-include
	--without-yaml-0.1-include=${yaml-0.1-dir}/include
	--with-yaml-0.1-lib
	--without-yaml-0.1-lib=${yaml-0.1-dir}/lib
	--with-yaml-0.1-config
	--without-yaml-0.1-config
	--with-pkg-config
	--without-pkg-config
	--with-libyaml-dir
	--without-libyaml-dir
	--with-libyaml-include
	--without-libyaml-include=${libyaml-dir}/include
	--with-libyaml-lib
	--without-libyaml-lib=${libyaml-dir}/lib

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/psych-5.1.0/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/psych-5.1.0 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/psych-5.1.0/gem_make.out

  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:102:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/ext_conf_builder.rb:28:in `build'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:171:in `build_extension'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:205:in `block in build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `each'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/installer.rb:843:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:72:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:28:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/source/rubygems.rb:202:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:54:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:16:in `install_from_spec'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:156:in `do_install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:141:in `install_serially'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:91:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:67:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:244:in `install_in_parallel'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:201:in `install'
  /root/.rbenv/rbenv.d/exec/gem-rehash/rubygems_plugin.rb:30:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:89:in `block in run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:12:in `block in lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `open'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:71:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:23:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli/install.rb:62:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:261:in `block in install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/settings.rb:130:in `temporary'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:260:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:34:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:28:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:37:in `block in <top (required)>'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/friendly_errors.rb:117:in `with_friendly_errors'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:29:in `<top (required)>'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `load'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `<main>'

An error occurred while installing psych (5.1.0), and Bundler cannot continue.

In Gemfile:
  irb was resolved to 1.8.0, which depends on
    rdoc was resolved to 6.5.0, which depends on
      psych
root@vm2540275:/opt/xx_backend# 
```

или когда делаете так
```sh
root@vm2540275:/opt/xx_backend# gem install psych -v 5.1.0
Building native extensions. This could take a while...
ERROR:  Error installing psych:
	ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/psych-5.1.0/ext/psych
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
checking for yaml.h... no
yaml.h not found
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/root/.rbenv/versions/3.1.3/bin/$(RUBY_BASE_NAME)
	--with-libyaml-source-dir
	--without-libyaml-source-dir
	--with-yaml-0.1-dir
	--without-yaml-0.1-dir
	--with-yaml-0.1-include
	--without-yaml-0.1-include=${yaml-0.1-dir}/include
	--with-yaml-0.1-lib
	--without-yaml-0.1-lib=${yaml-0.1-dir}/lib
	--with-yaml-0.1-config
	--without-yaml-0.1-config
	--with-pkg-config
	--without-pkg-config
	--with-libyaml-dir
	--without-libyaml-dir
	--with-libyaml-include
	--without-libyaml-include=${libyaml-dir}/include
	--with-libyaml-lib
	--without-libyaml-lib=${libyaml-dir}/lib

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/psych-5.1.0/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/psych-5.1.0 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/psych-5.1.0/gem_make.out
root@vm2540275:/opt/xx_backend# 
```

надо установить
```sh
sudo apt-get install libyaml-dev
```

https://stackoverflow.com/questions/14986663/gem-install-psych-error

после этого все ок

```sh
root@vm2540275:/opt/xx_backend# gem install psych -v 5.1.0
Building native extensions. This could take a while...
Successfully installed psych-5.1.0
Parsing documentation for psych-5.1.0
Installing ri documentation for psych-5.1.0
Done installing documentation for psych after 2 seconds
1 gem installed
```

#### Ошибка при установке гема pg

```sh
root@vm2540275:/opt/xx_backend# bundle
..
Installing pg 1.5.3 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/pg-1.5.3/ext
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
Calling libpq with GVL unlocked
checking for pg_config... no
checking for libpq per pkg-config... no
Using libpq from 
checking for libpq-fe.h... no
Can't find the 'libpq-fe.h header
*****************************************************************************

Unable to find PostgreSQL client library.

Please install libpq or postgresql client package like so:
  sudo apt install libpq-dev
  sudo yum install postgresql-devel
  sudo zypper in postgresql-devel
  sudo pacman -S postgresql-libs

or try again with:
  gem install pg -- --with-pg-config=/path/to/pg_config

or set library paths manually with:
  gem install pg -- --with-pg-include=/path/to/libpq-fe.h/ --with-pg-lib=/path/to/libpq.so/

*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/root/.rbenv/versions/3.1.3/bin/$(RUBY_BASE_NAME)
	--with-pg
	--without-pg
	--enable-gvl-unlock
	--disable-gvl-unlock
	--enable-windows-cross
	--disable-windows-cross
	--with-pg-config
	--without-pg-config
	--with-pg_config
	--without-pg_config
	--with-libpq-dir
	--without-libpq-dir
	--with-libpq-include
	--without-libpq-include=${libpq-dir}/include
	--with-libpq-lib
	--without-libpq-lib=${libpq-dir}/lib
	--with-libpq-config
	--without-libpq-config
	--with-pkg-config
	--without-pkg-config
	--with-pg-dir
	--without-pg-dir
	--with-pg-include
	--without-pg-include=${pg-dir}/include
	--with-pg-lib
	--without-pg-lib=${pg-dir}/lib

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/pg-1.5.3/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/pg-1.5.3 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/pg-1.5.3/gem_make.out

  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:102:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/ext_conf_builder.rb:28:in `build'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:171:in `build_extension'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:205:in `block in build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `each'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/installer.rb:843:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:72:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:28:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/source/rubygems.rb:202:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:54:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:16:in `install_from_spec'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:156:in `do_install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:141:in `install_serially'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:91:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:67:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:244:in `install_in_parallel'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:201:in `install'
  /root/.rbenv/rbenv.d/exec/gem-rehash/rubygems_plugin.rb:30:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:89:in `block in run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:12:in `block in lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `open'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:71:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:23:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli/install.rb:62:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:261:in `block in install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/settings.rb:130:in `temporary'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:260:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:34:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:28:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:37:in `block in <top (required)>'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/friendly_errors.rb:117:in `with_friendly_errors'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:29:in `<top (required)>'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `load'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `<main>'

An error occurred while installing pg (1.5.3), and Bundler cannot continue.

In Gemfile:
  pg
root@vm2540275:/opt/xx_backend# 
```

или когда делаете так
```sh
root@vm2540275:/opt/xx_backend# gem install pg -v 1.5.3
Building native extensions. This could take a while...
ERROR:  Error installing pg:
	ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/pg-1.5.3/ext
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
Calling libpq with GVL unlocked
checking for pg_config... no
checking for libpq per pkg-config... no
Using libpq from 
checking for libpq-fe.h... no
Can't find the 'libpq-fe.h header
*****************************************************************************

Unable to find PostgreSQL client library.

Please install libpq or postgresql client package like so:
  sudo apt install libpq-dev
  sudo yum install postgresql-devel
  sudo zypper in postgresql-devel
  sudo pacman -S postgresql-libs

or try again with:
  gem install pg -- --with-pg-config=/path/to/pg_config

or set library paths manually with:
  gem install pg -- --with-pg-include=/path/to/libpq-fe.h/ --with-pg-lib=/path/to/libpq.so/

*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/root/.rbenv/versions/3.1.3/bin/$(RUBY_BASE_NAME)
	--with-pg
	--without-pg
	--enable-gvl-unlock
	--disable-gvl-unlock
	--enable-windows-cross
	--disable-windows-cross
	--with-pg-config
	--without-pg-config
	--with-pg_config
	--without-pg_config
	--with-libpq-dir
	--without-libpq-dir
	--with-libpq-include
	--without-libpq-include=${libpq-dir}/include
	--with-libpq-lib
	--without-libpq-lib=${libpq-dir}/lib
	--with-libpq-config
	--without-libpq-config
	--with-pkg-config
	--without-pkg-config
	--with-pg-dir
	--without-pg-dir
	--with-pg-include
	--without-pg-include=${pg-dir}/include
	--with-pg-lib
	--without-pg-lib=${pg-dir}/lib

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/pg-1.5.3/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/pg-1.5.3 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/pg-1.5.3/gem_make.out
root@vm2540275:/opt/xx_backend# 
```

ну тут в общем в ошибке все написанно, надо установить
```sh
sudo apt-get install libpq-dev
```

и затем все корректно устанавливается
```sh
root@vm2540275:/opt/xx_backend# gem install pg -v 1.5.3
Building native extensions. This could take a while...
Successfully installed pg-1.5.3
Parsing documentation for pg-1.5.3
Installing ri documentation for pg-1.5.3
Done installing documentation for pg after 10 seconds
1 gem installed
root@vm2540275:/opt/xx_backend# 
```

#### Ошибка при установке гема unf_ext

```sh
root@vm2540275:/opt/xx_backend# bundle
..
Installing unf_ext 0.0.8.2 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
checking for -lstdc++... no
creating Makefile

current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
make DESTDIR\= sitearchdir\=./.gem.20240104-51106-uaf7k8 sitelibdir\=./.gem.20240104-51106-uaf7k8 clean

current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
make DESTDIR\= sitearchdir\=./.gem.20240104-51106-uaf7k8 sitelibdir\=./.gem.20240104-51106-uaf7k8
compiling unf.cc
make: g++: Command not found
make: *** [Makefile:215: unf.o] Error 127

make failed, exit code 2

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/unf_ext-0.0.8.2/gem_make.out

  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:102:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:51:in `block in make'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:43:in `each'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:43:in `make'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/ext_conf_builder.rb:42:in `build'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:171:in `build_extension'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:205:in `block in build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `each'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/ext/builder.rb:202:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0/rubygems/installer.rb:843:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:72:in `build_extensions'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/rubygems_gem_installer.rb:28:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/source/rubygems.rb:202:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:54:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/gem_installer.rb:16:in `install_from_spec'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:156:in `do_install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:141:in `install_serially'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:91:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer/parallel_installer.rb:67:in `call'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:244:in `install_in_parallel'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:201:in `install'
  /root/.rbenv/rbenv.d/exec/gem-rehash/rubygems_plugin.rb:30:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:89:in `block in run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:12:in `block in lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `open'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/process_lock.rb:9:in `lock'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:71:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/installer.rb:23:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli/install.rb:62:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:261:in `block in install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/settings.rb:130:in `temporary'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:260:in `install'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:34:in `dispatch'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/cli.rb:28:in `start'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:37:in `block in <top (required)>'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/lib/bundler/friendly_errors.rb:117:in `with_friendly_errors'
  /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/bundler-2.4.19/exe/bundle:29:in `<top (required)>'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `load'
  /root/.rbenv/versions/3.1.3/bin/bundle:25:in `<main>'

An error occurred while installing unf_ext (0.0.8.2), and Bundler cannot continue.

In Gemfile:
  http was resolved to 5.1.0, which depends on
    http-cookie was resolved to 1.0.5, which depends on
      domain_name was resolved to 0.5.20190701, which depends on
        unf was resolved to 0.1.4, which depends on
          unf_ext
(failed reverse-i-search)`gem': sudo apt-^Ct install postgresql
(failed reverse-i-search)`instal': sudo apt-get ^Cstall nginx
root@vm2540275:/opt/xx_backend# 
```

```sh
или когда делаете так
```sh
root@vm2540275:/opt/xx_backend# gem install unf_ext -v 0.0.8.2
Building native extensions. This could take a while...
ERROR:  Error installing unf_ext:
	ERROR: Failed to build gem native extension.

    current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
/root/.rbenv/versions/3.1.3/bin/ruby -I /root/.rbenv/versions/3.1.3/lib/ruby/3.1.0 extconf.rb
checking for -lstdc++... no
creating Makefile

current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
make DESTDIR\= sitearchdir\=./.gem.20240104-51250-4tchbd sitelibdir\=./.gem.20240104-51250-4tchbd clean

current directory: /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2/ext/unf_ext
make DESTDIR\= sitearchdir\=./.gem.20240104-51250-4tchbd sitelibdir\=./.gem.20240104-51250-4tchbd
compiling unf.cc
make: g++: Command not found
make: *** [Makefile:215: unf.o] Error 127

make failed, exit code 2

Gem files will remain installed in /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/gems/unf_ext-0.0.8.2 for inspection.
Results logged to /root/.rbenv/versions/3.1.3/lib/ruby/gems/3.1.0/extensions/x86_64-linux/3.1.0/unf_ext-0.0.8.2/gem_make.out
root@vm2540275:/opt/xx_backend# 
```

нужно установить на Ubuntu 20.04
```sh
sudo apt-get install g++
```

и затем все корректно устанавливается
```sh
root@vm2540275:/opt/xx_backend# gem install unf_ext -v 0.0.8.2
Building native extensions. This could take a while...
Successfully installed unf_ext-0.0.8.2
Parsing documentation for unf_ext-0.0.8.2
Installing ri documentation for unf_ext-0.0.8.2
Done installing documentation for unf_ext after 0 seconds
1 gem installed
```