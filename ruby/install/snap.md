## 💎 Ruby

### Установка через snap

При проверки версии Ruby даже на старой версии Ubuntu 20.04, будет предложена установка Ruby через snap

```sh
$ ruby -v

Command 'ruby' not found, but can be installed with:

sudo snap install ruby  # version 3.3.6, or
sudo apt  install ruby  # version 1:2.7+1

See 'snap info ruby' for additional versions.
```

проверьте доступные версии Ruby, командой `snap info ruby`

```sh
$ snap info ruby
name:      ruby
summary:   Interpreter for the Ruby programming language
publisher: Ruby core team (rubylang✓)
store-url: https://snapcraft.io/ruby
contact:   info@ruby-lang.org
license:   BSD-2-Clause OR Ruby
description: |
  Ruby is an interpreted object-oriented programming language often used for web
  development. It also offers many scripting features to process plain text and serialized
  files, or manage system tasks. It is simple, straightforward, and extensible.
snap-id: RjAgguCDAawLSJ3IByPe0R92xlNtrfGt
channels:
  latest/stable:    3.3.6  2024-11-07 (375) 34MB classic
  latest/candidate: ↑                            
  latest/beta:      ↑                            
  latest/edge:      3.3.4  2024-11-26 (377) 34MB classic
  3.3/stable:       3.3.6  2024-11-07 (375) 34MB classic
  3.3/candidate:    ↑                            
  3.3/beta:         ↑                            
  3.3/edge:         3.3.6  2024-11-05 (375) 34MB classic
  3.2/stable:       3.2.6  2024-11-01 (372) 31MB classic
  3.2/candidate:    ↑                            
  3.2/beta:         ↑                            
  3.2/edge:         3.2.6  2024-10-30 (372) 31MB classic
  3.1/stable:       3.1.6  2024-05-31 (347) 29MB classic
  3.1/candidate:    ↑                            
  3.1/beta:         ↑                            
  3.1/edge:         ↑                            
  3.0/stable:       3.0.7  2024-04-24 (335) 28MB classic
  3.0/candidate:    ↑                            
  3.0/beta:         ↑                            
  3.0/edge:         ↑                            
  2.7/stable:       2.7.8  2023-03-31 (308) 13MB classic
  2.7/candidate:    ↑                            
  2.7/beta:         ↑                            
  2.7/edge:         ↑                            
  2.6/stable:       2.6.10 2022-04-15 (269) 27MB classic
  2.6/candidate:    ↑                            
  2.6/beta:         ↑                            
  2.6/edge:         ↑                            
  2.5/stable:       2.5.9  2021-04-07 (209) 23MB classic
  2.5/candidate:    ↑                            
  2.5/beta:         ↑                            
  2.5/edge:         ↑                            
  2.4/stable:       2.4.10 2020-04-01 (178) 26MB classic
  2.4/candidate:    ↑                            
  2.4/beta:         ↑                            
  2.4/edge:         ↑                            
  2.3/stable:       2.3.8  2018-11-08 (109) 33MB classic
  2.3/candidate:    ↑                            
  2.3/beta:         ↑                            
  2.3/edge:         ↑ 
```

то есть как видите не доступен весь набор версий, как правило десяток последних минорных версий

вероятно вам нужно будет сначала произвести обновление версии Ruby в свом проекте

так же как видите выбора состоит из каналов, то есть например можете установить из нужного канала можете так

```sh
sudo snap install ruby --channel=3.1/stable --classic
```

и можете еще раз проверить доступную версию Ruby
```sh
$ ruby -v
ruby 3.1.6p260 (2024-05-29 revision a777087be6) [x86_64-linux]
```

#### Пример для Ansible

```yaml
- name: Установить Ruby через Snap
  become: true  # Поднимаем привилегии до sudo
  block:
    - name: Установить Ruby
      command: snap install ruby --channel=3.1/stable --classic
```