---
layout: post
title: gentoo缂栬瘧mysql
tags: 
 - gentoo
 - mysql
---
gentoo 缂栬瘧nginx鍙傝:[gentoo缂栬瘧nginx](http://lxyz.github.io/2012/07/compile-nginx-on-gentoo.html)

1.涓嬭浇mysql婧愮爜:

鎴戜笅杞界殑鏄痬ysql-5.5.25a
    wget http://cdn.mysql.com/Downloads/MySQL-5.5/mysql-5.5.25a.tar.gz

2.鍒涘缓mysql鐢ㄦ埛:

鎴戝垱寤簃ysql鐨勭敤鎴峰悕鏄痬ysql,鐢ㄦ埛缁勬槸mysql,鍛戒护濡備笅:
    groupadd mysql
    useradd -g mysql -s /sbin/nologin -M mysql
3.瀹夎cmake
    emerge cmake
4.缂栬瘧mysql:
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

瀹夎鐩綍鏄�opt/mysql,娌℃寚瀹歞ata鐩綍鍒檇ata鐩綍涓哄畨瑁呯洰褰曚笅鐨刣ata鏂囦欢澶�鍏朵粬鐨勫弬鏁板彲鏍规嵁闇�鑷繁娣诲姞.鍏充簬cmake鍙互鍙傝�:[MySQL5.5缂栬瘧宸ュ叿configure鍚慶make杩囨浮鎸囧崡](http://who0168.blog.51cto.com/253401/469898) .

鎺ョ潃:
    make
make鏃跺彲浠ュ埗瀹�-j鍙傛暟,鏉ユ彁楂樼紪璇戠殑鏁堢巼,鍙傝[make(gmake,gnumake)鐨�j鍙傛暟锛屼紭鍖栧鏍搞�澶氱嚎绋嬬殑缂栬瘧杩囩▼](http://hi.baidu.com/qshen/blog/item/4a06a41ec9ad6c1440341773.html).

make瀹屾垚涔嬪悗鎵ц:
    make install
5.閰嶇疆mysql:
    cd /opt/mysql
    cp support-files/my-medium.cnf /opt/mysql/etc/my.cnf
瀹夎鍒濆鏁版嵁搴�

    script/mysql_install_db --user=mysql --basedir=/opt/mysql
娉ㄦ剰,杩欓噷鐨刴ysql_install_db 鍦ㄥ畨瑁卪ysql鐩綍涓嬬殑script/鐩綍涓�

鎵ц瀹屾垚涔嬪悗浼氭彁绀哄涓嬩俊鎭�
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
鎸夌収涓婇潰杈撳嚭鐨勬彁绀轰俊鎭搷浣滃氨濂戒簡.

鎺ョ潃:
    cp support-files/mysql.server /etc/init.d/mysql
    export PATH=/opt/mysql/bin:$PATH
    rc-update add mysql default
鐜板湪鍚姩mysql鐪嬬湅:
    /etc/init.d/mysql start
鍙戠幇瀹夎宸茬粡瀹屾垚浜�

鍙傝� [Ubuntu 瀹夎MySQL](http://blog.csdn.net/htttw/article/details/6802130) .
