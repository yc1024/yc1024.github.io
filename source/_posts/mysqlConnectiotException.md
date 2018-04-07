---
title: mysqlConnectiotException
date: 2016-03-04 16:08:28
tags: mysql
---

授权语句:
```
grant all privileges on *.* to 'root'@'%' identified by 'root' with grant option;
//授权后刷新权限
flush privileges 
```
注: 将root 改为你的mysql用户
修改数据库中的root密码，登陆后在mysql终端输入：
```
update mysql.user set password=PASSWORD('111111') where user='root';
```
参考文献
[1] http://blog.csdn.net/xinshou_jiaoming/article/details/8585562  
[2] http://www.2cto.com/database/201412/364316.html


