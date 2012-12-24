---
layout: post
title: github多帐号配置
tags: 
 - 设计
 - github
---
有两个github帐号github_a和github_b(仅仅为了方便区分这样命名)，现在要在本地分别配置两个帐号进行配置，具体配置方法如下：

1.配置基本的git配置信息

    git config --list //查看己有配置信息

    //基本配置 
    git config --global user.name "HanHor Wu"
    git config --global user.email "hanhor.wu@gmail.com"

    //alias,方便操作
    git config --global alias.co "checkout"
    git config --global alias.ci "commit"
    git config --global alias.st "status"
 
也可以直接编辑文件~/.gitconfig，添加以下信息
    [user]
         name = HanHor Wu
         email = hanhor.wu@gmail.com
    [alias]
         co = checkout
         br = branch
         ci = commit
         st = status

2. 生成和配置两个ssh key
    ssh-keygen -t rsa -C "your-email_a"
注意：在存储key的时候建议用自己定义的名字，以免覆盖了系统中本来存在的key，比如这里我们把生成的key存为：github_a,用同样的方法生成key:github_b;

把生成的key加到ssh agent上
    ssh-add ~/.ssh/github_a
    ssh-add ~/.ssh/github_b
通过
    ssh-add -l
来确认结果。

3.添加配置文件
新建配置文件：
    vim ~/.ssh/config
添加如下信息:
    #default github
    Host github_a
         HostName github.com
         IdentityFile ~/.ssh/github_a

    Host github_b
        HostName github.com
        IdentityFile ~/.ssh/github_b
并保存。

4.配置github帐号
分别登录github_a和github_b，添加对应的key,这样github帐号就配置好了.
随便在本地建立一个测试文件，并提交。
    mkdir test
    cd test
    git init
    touch README.md
    git add README.md
    git commit -m "first commit'
#push到github上去
    git remote add origin git@github_a:xxxx/test.git
    git push origin master

注意，在添加别名时（即git remote add origin git@github_a:xxxx/test.git），这里所对应的github_a:xxxx不是github的URL，而是自己在第三部中对应的host信息，xxxx为自己的github帐号名。