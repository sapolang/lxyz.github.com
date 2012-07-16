---
layout: post
title: gentoo编译nginx
tags: 
 - gentoo
 - nginx
---
  今天搞了个gentoo玩玩.内存开销确实小啊.先在上面编译个nginx.步骤如下:

1.下载nginx:

我下载的是nginx 1.2.2 stable
    wget http://nginx.org/download/nginx-1.2.2.tar.gz

2.创建nginx用户和组:

我创建nginx的用户名是www,用户组是www,命令如下:
    groupadd www
    useradd -g www -s /sbin/nologin -M www
3.编译nginx:
    tar zxvf nginx-1.2.2.tar.gz
    cd nginx-1.2.2
    ./configure --user=www --group=www --prefix=/opt/nginx --with-http_stub_status_module --with-http_ssl_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module

安装目录是/opt/nginx,其他的模块可根据需要自己添加.具体可以参见[nginx官方wiki](http://wiki.nginx.org/Modules) .

4.设置开机启动,环境变量等:

将[nginx.init](https://github.com/HorX/gentoo_server)这个文件下载下来,copy到/etc/init.d/nginx
    cp nginx.init /etc/init.d/nginx
然后执行:
    export PATH=/opt/nginx/sbin:$PATH
接着:
    rc-update add nginx default
现在启动nginx看看:
    /etc/init.d/nginx start
如果提示错误:
    /etc/init.d/nginx: line 22: /lib/lsb/init-functions: No such file or directory
将rc.status和init-functions[两个文件](https://github.com/HorX/gentoo_server)分别copy/etc/ 和/etc/lsb/目录(参考:[gentoo wiki](http://www.gentoo-wiki.info/Rivendell)):
    cp rc.status /etc/rc.status
    mkdir /lib/lsb/
    cp init-functions /lib/lsb/init-functions
然后再启动nginx,就没什么问题了.

接下来就是配置nginx,这个可以参考nginx官方的wiki.

文中所涉及到的要下载的文件:
    nginx.init
    rc.status
    init-functions
见 [https://github.com/HorX/gentoo_server](https://github.com/HorX/gentoo_server) .
