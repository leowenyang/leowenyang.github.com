---
layout: post
title:  ssh git 和 mysqldump 备份mysql 
category: database 
img: database.png 
description : 介绍使用ssh git 和mysqldump 工具链备份mysql
keywords: git ssh mysql 
---

## ssh+git+mysqldump备份mysql

一直以来，有一个想法，想通过git 来备份VPS上的mysql数据库，好处如下：

1. 数据可以保存
2. 数据可以回溯
3. 不同版本间可以查看差别

经过摸索，终于找到如下的方法：

## 1. VPS 上创建git bare 仓库
    git init --bare wordpress_backup.git
        --bare: 创建bare 仓库

## 2. clone git bare 仓库
    git clone wordpress_backup.git

**note: 上面两步是为远程备份做准备，如果只是在VPS上备份，可用git init 代替**

## 3. mysqldump 导出Mysql数据库
    cd wordpress_backup
    mysqldump -uleowenyang -p123 -hroclinux.cn -P8080 wordpress > wordpress_db_backup.sql
        -u: 用户名
        -p: 密码
        -h: VPS的域名
        -P: 端口

## 4. 存储导出的数据库到git 仓库，commit, 并push
    git add .
    git commit -m "update sql file"
    git push

到此，已经完成了服务上备份mysql数据库的操作。写成shell就可以在服务器上定期备份数据库了。

    cd wordpress_backup
    mysqldump -uleowenyang -p123 -hroclinux.cn -P8080 wordpress > wordpress_db_backup.sql
    git add .
    git commit -m "update sql file"
    git push

下面，进一步在本地备份mysql数据库的操作

## 5. 本地clone VPS上的git 仓库
    git clone leowenyang@roclinux.cn:wordpress_backup.git

## 6. 本地pull VPS上的git 仓库
    git pull

到此，只能从VPS取出已经备份好的数据，如果要实时备份，进行下一步

## 7. 本地通过SSH备份数据库
    ssh leowenyang@roclinux.cn 'cd wordpress_backup; \
        mysqldump --extended-insert=FALSE --complete-insert=TRUE 
        -uleowenyang -pMYPASSWORD wordpress > wordpress_backup.sql; \
        git commit -a -m"update sql file";\
        git push’

    cd wordpress_backup; git pull

至此，如何想要备份mysql数据库，直接执行上面的命令就行。写成shell, 方便以后使用。  
最后，如果数据库出现问题，可以通过git来查看不同版本之间的差异来定位问题了。
