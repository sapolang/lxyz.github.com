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
  记录在全新的 ubuntu server 上面用 capistrano 部署 ROR 程序的过程

1.创建部署用户:
登录 ubuntu server ，新建一个用于部署程序的用户 deployer:

    sudo adduser deployer --ingroup sudo
    
2.安装系统必要的程序
  
    su deploy #切换到deploy这个用户
    sudo apt-get update
	sudo apt-get -y install git-core
	sudo apt-get -y install libmysqlclient-dev
	sudo apt-get -y install libxml2-dev libxslt1-dev
	
安装nginx

	sudo apt-get install python-software-properties
	sudo add-apt-repository ppa:nginx/stable
	sudo apt-get update
	sudo apt-get -y install nginx
	