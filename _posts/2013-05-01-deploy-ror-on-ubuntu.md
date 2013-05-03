---
layout: post
title: ubuntu server 部署 rails
tags: 
 - ubuntu
 - rails
 - nginx
 - unicorn
 - capistrano
---
记录在全新的 ubuntu server 上面用 capistrano 部署 ROR 程序的过程,其中 web server 用 nginx, appserver 用 unicorn, 数据库用 mysql, 部署工具用 capistrano .

1.创建部署用户:
登录 ubuntu server ，新建一个用于部署程序的用户 deployer:

```
sudo adduser deployer --ingroup sudo
```
    
2.安装系统必要的程序
  
```
su deploy #切换到deploy这个用户
sudo apt-get update
sudo apt-get -y install git-core
sudo apt-get -y install libmysqlclient-dev
sudo apt-get -y install libxml2-dev libxslt1-dev
```
	
3.安装 nginx

```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get -y install nginx
```
	
4.安装 rbenv

 ```
curl https://raw.github.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash
 ```
   
将下面内容添加到bash


```
export RBENV_ROOT="${HOME}/.rbenv"

if [ -d "${RBENV_ROOT}" ]; then
  	export PATH="${RBENV_ROOT}/bin:${PATH}"
  	eval "$(rbenv init -)"
fi
```

使 bash 生效


```
source ~/.bashrc
```
   
安装 rbenv 必要的依赖


```
rbenv bootstrap-ubuntu-12-04
```

4.安装 ruby

```
rbenv install 2.0.0-p0
rbenv global 2.0.0-p0
gem install bundler --no-ri --no-rdoc
```
    
安装gem时不安装 ri 和 rdoc:
将

```
gem: --no-ri --no-rdoc
```

或


```
install: --no-rdoc --no-ri 
update:  --no-rdoc --no-ri
```

添加到 `~/.gemrc`

5.安装 nginx

```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get -y install nginx
```

6.nodejs

```
sudo apt-get install nodejs

```
7.mysql

```
sudo apt-get install mysql-server libmysqlclient-dev
```


参考资料:

  [railscasts](http://railscasts.com/episodes/335-deploying-to-a-vps),
  [happycasts](http://happycasts.net/episodes/42)