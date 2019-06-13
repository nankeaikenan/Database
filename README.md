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
删除表：drop table 表名
判断表是否存在，存在则删除表：drop table if exists 表名
添加表列：alter table 表名 add 列名 类型     
eg：为学生添加一个新的字段remark，类型为varchar(20)
  alter table student add remark varchar(20)
修改列类型：alter table 表名 modify 列名 新类型；       eg:alter table student modify remark varchar(100);
修改列名：alter table 表名 change 旧列名 新列名 类型；   eg:alter table student change remark intro varchar(30);
清除列：alter table 表名 drop 列名；     eg(删除学生表中的字段intro）：alter table student drop intro;
修改表名：rename table 旧表名 to 新表名      eg:rename table student to student2;
修改字符集：alter table 表名 character set 字符集；   eg:alter table student2 character set gbk;
重点部分：
DML操作表中的数据
1.插入记录：insert [into] 表名 [字段名] values (字段值)；
            insert into 表名：表示要往哪张表里添加数据；
            （字段名1，字段名2...）:要给哪些字段设置值；
            values(值1，值2...）：设置具体的值；
  1.1插入    全部字段：所有的字段名都写出来：insert into 表名 (
