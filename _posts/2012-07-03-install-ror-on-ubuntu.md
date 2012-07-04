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
    sudo apt-get install zlib1g-dev 
    cd ruby-1.9.3-p0/ext/zlib$
    sudo ruby extconf.rb 
    sudo  make 
    sudo make install

 4.在 ~/.gemrc或/etc/gemrc 文件中加上下面一行，之后通过gem安装的程序都不带ri/rdoc
    gem: --no-ri --no-rdoc
或
    install: --no-rdoc --no-ri 
    update:  --no-rdoc --no-ri

 6.换淘宝的源
    $ gem sources --remove http://rubygems.org/
    $ gem sources -a http://ruby.taobao.org/
    $ gem sources -l
    ** CURRENT SOURCES ***

    http://ruby.taobao.org
    # 请确保只有 ruby.taobao.org

 7.安装javascript runtime
    sudo apt-get install nodejs

 8.安装openssl支持
    sudo apt-get install libssl-dev
    cd /ruby-source-files/ext/openssl
    sudo ruby extconf.rb
    sudo  make
    sudo make install
 9.增加mysql支持
首先要安装mysql，没有安装的话请先安装
    sudo apt-get install mysql-server
    sudo apt-get install libmysql-ruby libmysqlclient-dev
    sudo gem install mysql2  --no-ri --no-rdoc

这样基本就安装完成了。
新建一个支持mysql数据库项目demo:
    rails new demo -d mysql
也可以直接
    rails new demo
完成之后再Gemfile文件中将默认的sqlite3改成mysql2，再执行
    bundle
就可以了。

参考[Ubuntu下搭建Ruby On Rails](http://blog.csdn.net/htttw/article/details/7628093)

补充：

 1.安装nokogiri
 
Nokogiri是一个高效的HTML/XML的解析器。安装方法如下:
    sudo apt-get install libxslt-dev libxml2-dev
    sudo gem install nokogiri
 2.安装postgres
    sudo aptitude installi postgresql-9.1 postgresql-server-dev-9.1 libpq-dev
安装postgres图形化管理工具pgAdmin
    sudo aptitude install pgadmin3

安装postgres的gem
    sudo gem install do_postgres
