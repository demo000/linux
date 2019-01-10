下载压缩包

--解压压缩包

#tar -xzvf /data/software/mysql-5.7.17-linux-glibc2.5-x86_64.tar.gz

--移动并修改文件名

#mv /data/software/mysql-5.7.17-linux-glibc2.5-x86_64 /usr/local/mysql

4创建数据仓库目录

--/data/mysql 数据仓库目录
# mkdir /data/mysql         
#ls /data

5新建mysql用户、组及目录
添加系统mysql组
```
groupadd mysql
```
添加mysql用户
```
useradd -r -g mysql mysql
```

6改变目录属有者

#cd /usr/local/mysql
#pwd
#chown -R mysql .
#chgrp -R mysql .
直接删除/etc/my.cnf 5.7不在需要
7配置参数
# bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/data/mysql
记下临时密码:xxxx
bin/mysql_ssl_rsa_setup  --datadir=/data/mysql


添加开机启动     
```
cp /usr/local/mysql/support-files/mysql.server  /etc/init.d/mysqld
```

修改   
```jshelllanguage
vi /etc/init.d/mysqld

```
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data


启动mysql   service mysqld start 
加入开机起动   chkconfig --add mysqld  

登录修改密码 mysql -uroot -p 上面初始化时的密码

如果出现错误 需要添加软连接  
```jshelllanguage
ln -s /usr/local/mysql/bin/mysql /usr/bin
```
修改密码
alter user 'root'@'localhost' identified by 'root'; 
为需要远程登录的用户赋予权限
```
1、新建用户远程连接mysql数据库
grant all on *.* to admin@'%' identified by '123456' with grant option; 
flush privileges;
允许任何ip地址(%表示允许任何ip地址)的电脑用admin帐户和密码(123456)来访问这个mysql server。
注意admin账户不一定要存在。

2、支持root用户允许远程连接mysql数据库
grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
flush privileges;

```