---
layout: post
title: gentoo编译mysql
tags: 
 - gentoo
 - mysql
---
gentoo 编译nginx参见:[gentoo编译nginx](http://blog.hanhor.com/2012/07/compile-nginx-on-gentoo.html)

1.下载mysql源码:

我下载的是mysql-5.5.25a
    wget http://cdn.mysql.com/Downloads/MySQL-5.5/mysql-5.5.25a.tar.gz

2.创建mysql用户:

我创建mysql的用户名是mysql,用户组是mysql,命令如下:
    groupadd mysql
    useradd -g mysql -s /sbin/nologin -M mysql
3.安装cmake
    emerge cmake
4.编译mysql:
    tar mysql-5.5.25a.tar.gz
    cd mysql-5.5.25a
    cmake . \
    -DCMAKE_INSTALL_PREFIX=/opt/mysql \
    -DINSTALL_DATADIR=/opt/mysql/data \
    -DSYSCONFDIR=/opt/mysql/etc \
    -DWITH_MYISAM_STORAGE_ENGINE=1 \
    -DWITH_INNOBASE_STORAGE_ENGINE=1 \
    -DWITH_ARCHIVE_STORAGE_ENGINE=1 \
    -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
    -DENABLED_LOCAL_INFILE=1 \
    -DDEFAULT_CHARSET=utf8 \
    -DDEFAULT_COLLATION=utf8_general_ci \
    -DEXTRA_CHARSETS=all \
    -DMYSQL_TCP_PORT=3306 \
    -DMYSQL_UNIX_ADDR=/tmp/mysqld.sock \
    -DMYSQL_USER=mysql \
    -DWITH_DEBUG=0

安装目录是/opt/mysql,没指定data目录则data目录为安装目录下的data文件夹.其他的参数可根据需要自己添加.关于cmake可以参考:[MySQL5.5编译工具configure向cmake过渡指南](http://who0168.blog.51cto.com/253401/469898) .

接着:
    make
make时可以制定 -j参数,来提高编译的效率,参见[make(gmake,gnumake)的-j参数，优化多核、多线程的编译过程](http://hi.baidu.com/qshen/blog/item/4a06a41ec9ad6c1440341773.html).

make完成之后执行:
    make install
5.配置mysql:
    cd /opt/mysql
    cp support-files/my-medium.cnf /opt/mysql/etc/my.cnf
安装初始数据库:

    script/mysql_install_db --user=mysql --basedir=/opt/mysql
注意,这里的mysql_install_db 在安装mysql目录下的script/目录中.

执行完成之后会提示如下信息:
    Installing MySQL system tables...
    OK
    Filling help tables...
    OK

    To start mysqld at boot time you have to copy
    support-files/mysql.server to the right place for your system

    PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
    To do so, start the server, then issue the following commands:

    /opt/mysql/bin/mysqladmin -u root password 'new-password'
    /opt/mysql/bin/mysqladmin -u root -h hhw-server password 'new-password'

    Alternatively you can run:
    /opt/mysql/bin/mysql_secure_installation

    which will also give you the option of removing the test
    databases and anonymous user created by default.  This is
    strongly recommended for production servers.

    See the manual for more instructions.

    You can start the MySQL daemon with:
    cd /opt/mysql ; /opt/mysql/bin/mysqld_safe &

    You can test the MySQL daemon with mysql-test-run.pl
    cd /opt/mysql/mysql-test ; perl mysql-test-run.pl

    Please report any problems with the /opt/mysql/scripts/mysqlbug script!
按照上面输出的提示信息操作就好了.

接着:
    cp support-files/mysql.server /etc/init.d/mysql
    export PATH=/opt/mysql/bin:$PATH
    rc-update add mysql default
现在启动mysql看看:
    /etc/init.d/mysql start
发现安装已经完成了.

参考 [Ubuntu 安装MySQL](http://blog.csdn.net/htttw/article/details/6802130) .
