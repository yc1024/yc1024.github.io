---
title: mysql忘记root密码
date: 2018-04-04 16:08:28
tags: mysql
---
今天意外的发现很久没有使用的mysql数据库密码忘记了..于是就秀一波操作吧..

```
sudo vim /etc/mysql/my.cnf
skip-grant-tables  //添加这句话，见名知意，绕过授权
sudo service mysql restart
sudo mysql -u root
use mysql;
update user set password=password('root') where user='root'; 
flush privileges;
quit
```
最后记得把`skip-grant-tables` 干掉..
