# myFirstTest
创建数据库：create database 数据库名
检查数据库是否存在，不存在则创建数据库：create database if not exists 数据库名
创建数据库并指定字符集：create database 数据库名 character set 字符集
修改数据库默认数据集：alter database 数据库名 character set 字符集
删除数据库：drop database 数据库名
查看正在使用的数据库：select database（）
使用/切换数据库：use 数据库名
创建表的格式：
create table 表名(
  字段名1 字段类型1,
  字段名2 字段类型2    (没有逗号)
）；
常用的数据类型：int，double，varchar,date
eg:
create table student(
  id int;
  name varchar(20),
  birthday date   (没有逗号)
);
查看某个数据库中的所有表：show tables;
查看表结构：desc 表名；
查看创建表的SQL语句：show create table 表名；
快速创建一个表结构相同的表：create table 新表名 like 旧表名   eg:create table stu like student;desc stu;
删除表：
