---
layout : post
title: ubuntu安装Ruby on Rails
tags:
  - ruby
  - rails
---
1.安装yaml

    wget http://pyyaml.org/download/libyaml/yaml-0.1.4.tar.gz
    tar xzvf yaml-0.1.4.tar.gz
    cd yaml-0.1.4
    ./configure --prefix=/usr/local
    make
    sudo make install

2.安装ruby
    ./configure --prefix=/usr/local --enable-shared --disable-install-doc --with-opt-dir=/usr/local/lib
    make
    sudo make install
3.安装zlib
```bash
sudo apt-get install zlib1g-dev 
cd ruby-1.9.3-p0/ext/zlib$
sudo ruby extconf.rb 
sudo  make 
sudo make install
```
4.在 ~/.gemrc或/etc/gemrc 文件中加上下面一行，之后通过gem安装的程序都不带ri/rdoc
`gem: --no-ri --no-rdoc`
或
```ruby
install: --no-rdoc --no-ri 
update:  --no-rdoc --no-ri
```

6.换淘宝的源
```ruby
$ gem sources --remove http://rubygems.org/
$ gem sources -a http://ruby.taobao.org/
$ gem sources -l
*** CURRENT SOURCES ***

http://ruby.taobao.org
# 请确保只有 ruby.taobao.org
```

7.安装javascript runtime
```bash
sudo apt-get install nodejs
```

8.安装libssl-dev
```bash
cd /ruby-source-files/ext/openssl
sudo ruby extconf.rb
sudo  make
sudo make install
```
9.增加mysql支持
首先要安装mysql，没有安装的话请先安装
sudo apt-get install mysql-server
sudo apt-get install libmysql-ruby libmysqlclient-dev
sudo gem install mysql2  --no-ri --no-rdoc

错误1.
It seems your ruby installation is missing psych (for YAML output).
To eliminate this warning, please install libyaml and reinstall your ruby.
http://rubygems.org/ removed from sources



