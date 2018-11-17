
mysql -uroot -p8911489656m | 登录账号 连接Mysql
----|---
 其它MySQL客户端|navcat MySQLfront phpMyAdmin
基本语句|基本语句
show database; | 查看数据库
show tables; | 查看表
create database xx charset utf8;|创建名为xx的数据库
drop database xx; | 删除数据库
数据库不能改名|!!!!
rename table xx to yy | 将表xx改名为yy
在mysql my.ini 中 搜 datadir | 查看数据库存放位置
Create table stu( Snum int , Sname varchar(10))engine myisam charset utf8;|基本表
truncate xx; | 清空表中数据(truncate删表重建 delete删除行数据)
tee location | 选择存放文件位置
desc xx | 查看xx的结构