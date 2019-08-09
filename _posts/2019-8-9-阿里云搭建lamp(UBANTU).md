---
layout: post
title:  "阿里云搭建lamp(UBANTU)"
categories: 杂记
tags: 杂记
author: 段雨寒
---

* content
{:toc}
## 备注：

\##################
备注：如果这时候发现无法访问公网ip， 请去配置阿里云后台的安全组。
添加一条 入方向的规则

eg:

允许 自定义 TCP 
80/80 地址段访问 
0.0.0.0/0
apahce
1 2017-06-27 11:31:46

mysql 3306 设置同理
第二：
无法连接。有密钥 ，可以在密钥管理中删除密钥，也可以使用密钥连接。建议删除
\###########

sudo apt-get install mysql-server mysql-client

(输入MySQL 密码)

sudo apt-get install php7.0

安装php apache模块
sudo apt-get install libapache2-mod-php

 

 

 

sudo apt-get install php7.0 table table 查看所有php7.0 的插件

 

一般装 php7.0-mysql php7.0-mysql php7.0-curl php7.0-gd php7.0-mbstring

php7.0-mcrypt php7.0-xml php7.0-zip

 

sudo apt-get install php7.0-mysql php7.0-mysql php7.0-curl php7.0-gd php7.0-mbstring php7.0-mcrypt php7.0-xml php7.0-zip php7.0-gd

 

 

安装 下载工具 wget

sudo apt-get install -y wget

 

\#安装composer

去composer 找命令

建议切换到 /usr/local/bin

使用wget安装composer wget 加上composer的官网下载地址

`wget https://getcomposer.org/composer.phar` 

重命名文件composer.phar 为 composer 
$ mv composer.phar composer

$ chmod +x composer

 

 

然后如果需要git 他自带有的

其实linux 和Windows 差别不大的，都是系统，我们用的也就是装软件而已。

常用的目录结构
WWW var/html

 

\#配置虚拟主机
修改文件
vi /etc/apache2/sites-avilabe/000-default.conf
代码如下：
<VirtualHost *:80>

ServerAdmin webmaster@localhost
DocumentRoot /var/www/html/laravel/public
ServerName www.shxdledu.cn

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

 

配置成功后重启apahce 
sudo service apache2 restart

 

## 扩展和优化

### 【01】开启路由重写模块

Ubuntu下apache2的rewrite模块默认是不加载的。
只要运行了一下这个命令：a2enmod rewrite 就可以启用rewrite模块了。

备注：
Apaceh2 多了一组 a2enmod, a2dismod指令，用于启用和禁用Apache的模块。a2enmod用于在Apache启用指定的模块,它实际上做的是在/etc/apache2 /mods-enabled目录下创建模块文件的符号链接。相反a2dismo则是通过删除符号链接而达到禁用指定模块的功能。当然，启用已启用的模块或禁用已禁用的模块是不会报错的。^^
这里有必要说明一下：
/etc/apache2/mods-available 放apache可用的模块文件
/etc/apache2/mods-enabled 放apache已启用的模块文件的链接
弄明白了，去查看一下/etc/apache2/mods-enabled目录，果然有新增了一条rewrite.load的链接。

重启apache 即可去掉index.php访问

 

### 【02】apache 配置错误码页面

 

配置404发现不跳转原因！

1.这个的内容根据你的情况改写 。可是有时候当你用IE浏览的时候会发现，这玩意压根就不跳转，关键的地方就是这个html，如果404.html的小于512字节的话，那么IE会认为这个错误页面不够“友好”，会忽视掉的！

 

然后注意，项目上传到/var/www/html
下 注意给777权限！！

域名记得解析对应好 就可以访问了。

 

### 解决外部无法连接mysql 问题

在虚拟机ubantu下安装了MySQL，但是在物理机中无法访问到该MySQL数据库。

排查问题过程：
在物理机中可以Ping通虚拟机的IP和telnet 3306端口也是正常的，所以不存在网络问题和防火墙的问题，就解决方法，在此做个笔记，以作备忘。
问题主要是由于MySQL默认安装后，并不允许远程访问（即非本机访问），说白了就是访问权限不够的问题。解决该问题的办法就是给用户授予对应的权限。

\##解决步骤：
1、修改配置文件：

cd /etc/mysql/mysql.conf.d    

vi mysqld.cnf

查找到bind-address，将 bind-address=127.0.0.1 修改为 bind-address = 0.0.0.0 ，以允许任何IP来访问MySQL服务。

2、重启MySQL服务：sudo service mysql restart

3、登录MySQL数据库，给需要远程访问的用户授权：

授权所有权限：

mysql> grant all privileges on *.* to root@"%" identified by "123456" with grant option;

授权只读权限是 grant select on *.* to onlyRead@"%" identified by "123456" with grant option;  执行修改删除 则会提示没有权限。
本次授权root用户远程访问test数据库的权限，如果你想授权所有数据库，则用*来代替test，就表明全部数据库。

4、刷新配置，使权限立即生效：
mysql> flush privileges;
这时，通过物理主机的MySQL客户端就可以正常登录了。

 

5、奇葩的报错nacvait ssh auth filed（如果你不手贱，你是不会出现这个错误的）

如果使用navcait或者其他远程工具连接 发现报错为

SSH远程登录失败，提示“Password authentication failed”

是因为mysql的密码加密方式是md5 与ssh不一样。

那么解决，请不要使用ssh 连接mysql。

如图报错

![img](https://leanote.com/api/file/getImage?fileId=5a69daffab64416129001e9f)

如图报错因为我使用了ssh

![img](https://leanote.com/api/file/getImage?fileId=5a69dae9ab64416129001e9a)

解决不勾选ssh连接后，提示连接成功

![img](https://leanote.com/api/file/getImage?fileId=5a69db29ab64416324001e07)

# 新阿帕奇 需要配置一下 阿里云后台

新安装apache服务器，在此记录安转过程，仅供自己日后参考。首先环境是阿里云+ubuntu16.04+apache2,安装好apache后会默认有这样一个界面。

![img](http://img.blog.csdn.net/20170517003650896?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc2luYXRfMzU1Mzc0NzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

​    在虚拟机上安装过很多次，第一次在云服务器上安装，安装之前也许需要执行下面这个操作来更新apt-get这个软件。

 

[html]

view plain

 [copy](http://blog.csdn.net/sinat_35537471/article/details/72355362#)

 

1. <span style="font-size:14px;">sudo update-grub</span>  

 

然后执行下载并安指令

[plain]

view plain

 [copy](http://blog.csdn.net/sinat_35537471/article/details/72355362#)

 

1. <span style="font-size:14px;">apt-get install apache2</span>  

完事之后就安装好了apache服务器。此时通过浏览器打开 http://127.0.0.1就可以看到上面的界面了，如果是在命令行情况下，通过curl http://127.0.0.1就可以访问本地apache服务器了，如果访问不成功，有可能是apache服务器未运行，那么就执行:

[html]

view plain

 [copy](http://blog.csdn.net/sinat_35537471/article/details/72355362#)

 

1. sudo /etc/init.d/apache2 start  

再次执行curl后就可以接收到如下的html代码：

 

![img](http://img.blog.csdn.net/20170517004955241)

​    不要嫌弃我的配色方案有点丑，putty天生就是这个尿性，也懒得改。这样在本地就可以访问我们的apache服务器了，可是这是一台服务器，我想要外网也能够访问到我的主页，这时候用外网访问发现无法显示出来，但是通过ping我服务器的IP是可以ping的到的。于是我就怀疑是防火墙的问题。

​    按照网上的教程呢，先关闭防火墙，这里我没安装别的防火墙，只有系统自带的iptables这个防火墙,很多人搞不清楚具体规则，那么可以执行清空所有规则指令，这样就可以避免访问被拒绝了。我做到这，发现apache网页依旧不能被公网IP访问到，继续研究，发现在阿里云中需要设置安全组属性才可以。具体设置方法如下：

![img](http://img.blog.csdn.net/20170517010247995)        在服务器的控制台中，点击这个安全组，进去后点击对应服务器旁边的配置规则，发现里面有设置端口访问规则的一张ACL表格。如下所示

![img](http://img.blog.csdn.net/20170517010551873)

​    在这里修改了80端口入方向的许可权，就可以让你的外网主机访问服务器啦。至此就是我的全部操作过程。

 http://blog.csdn.net/sinat_35537471/article/details/72355362

 

## 忘记mysql密码

忘了mysql密码，从网上找到的解决方案记录在这里。

编辑mysql的配置文件/etc/mysql/my.cnf，在[mysqld]段下加入一行“skip-grant-tables”。

![Ubuntu下忘记MySQL root密码解决方法](https://leanote.com/file/outputImage?fileId=5a043e27ab64414b3c002138)

重启mysql服务

www.linuxidc.com @ubuntu:~$ sudo service mysql restart  
mysql stop/waiting  
mysql start/running, process 18669 

用空密码进入mysql管理命令行，切换到mysql库。

www.linuxidc.com @ubuntu:~$ mysql  
Welcome to the MySQL monitor.  Commands end with ; or \g.  
mysql> use mysql  
Database changed 

执行update user set password=PASSWORD("new_pass") where user='root'; 把密码重置为new_pass。退出数据库管理。

mysql> update user set password=PASSWORD("new_pass") where user='root';    
Query OK, 0 rows affected (0.00 sec)    
Rows matched: 4  Changed: 0  Warnings: 0    
mysql>quit 

回到vim /etc/mysql/my.cnf，把刚才加入的那一行“skip-grant-tables”注释或删除掉。

再次重启mysql服务sudo service mysql restart，使用新的密码登陆，修改成功。

www.linuxidc.com @ubuntu:~$ mysql -uroot -pnew_pass  
Welcome to the MySQL monitor.  Commands end with ; or \g.  
mysql> 

 

# 一些坑：

## mysql 数据导入导出报错

问：mysql无法导出数据，出现ERROR 1290 20

ERROR 1290 (HY000): The MySQL server is running with the --secure-file-priv option so it cannot execute this statement.将my.ini里的seruce-file-priv条目注释掉之后，还是出现同一个错误。？

原因： mysql 默认限制了导入导出目录；

![img](https://leanote.com/api/file/getImage?fileId=5a4aeda7ab644116e2000dda)

1.进入mysql查看secure_file_prive的值

![img](https://leanote.com/api/file/getImage?fileId=5a4aedb7ab644116e2000de0)

备注：
$mysql -u root -p
mysql>SHOW VARIABLES LIKE "secure_file_priv";
secure_file_prive=null -- 限制mysqld 不允许导入导出
secure_file_priv=/tmp/ -- 限制mysqld的导入导出只能发生在/tmp/目录下
secure_file_priv=' ' -- 不对mysqld 的导入 导出做限制

解决方案： 到处指定目录

![img](https://leanote.com/api/file/getImage?fileId=5a4aede2ab644116e2000deb)