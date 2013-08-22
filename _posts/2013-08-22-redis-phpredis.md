---
layout: post
title: redis and phpredis扩展的安装
tags:
 - blog
 - markdown
---


##linux上安装redis和phpredis扩展
  #### 安装redis server
    1.下载redis稳定版，当前版本为2.6.15
        wget http://download.redis.io/releases/redis-2.6.15.tar.gz
    2.解压
        tar -zxvf redis-2.6.15.tar.gz
    3.cd redis-2.6.15/src
    4.make && make install ,如果没有权限+sudo，此时在/usr/local/bin/就有redis的相关命令
    5.将配置文件redis.conf 放到/usr/local/etc/redis下面便于管理，修改配置文件
        将daemonize yes 让redis可以后台运行
    6.启动redis，redis-server /usr/local/etc/redis/redis.conf就可以启动redis了,
        打开客户端redis-cli

#### 安装phpredis扩展
    phpredis的源代码托管在github上面，在github里就可以收索出来,现在来下载phpredis的源代码
    1.git clone https://github.com/nicolasff/phpredis.git
    2.clone下来之后，我们就可以进入这个目录进行编译安装了，
       1.cd phpredis
       2.phpize5，如果没有这个命令，可以sudo apt-get install php5-dev
       3.phpize5之后，就有了configure文件，./configure
       4.make && make install
    然后进入/etc/php5/apache2/conf.d ，这个文件夹里都是扩展的ini文件,
        在里面新建redis.ini文件，输入extension.so，重启apache，phpinfo(),就可以看到redis扩展了
        如果你的web服务器是nginx，那你用的应该是php5-fpm了，将这个文件建在/etc/php5/fpm/conf.d/
        下,重启php5-fpm(sudo service php5-fpm restart) ,然后重启nginx就ok了