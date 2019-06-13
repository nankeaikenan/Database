# Database
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
            values (值1，值2...）：设置具体的值；
  1.1 插入    全部字段：所有的字段名都写出来：insert into 表名 （字段名1，字段名2...） values (值1，值2...）;
                     不写字段名：insert into 表名 values (值1，值2...）;
                     eg:insert into table student (id,name,age,sex) values (1,'甲',18,'男')；
                         (student一共有id,name,age,sex，addr五个字段)
                        插入所有列：insert into table student values (1,'甲',18,'男'，'家里')；
                        插入部分列：insert into table student (id,name) values (2,'乙');(插入部分列必须写列名)
  1.2 查看mysql内部设置的编码:show variables like 'character%';
  1.3 将表2中所有的的列复制到表一中:insert into  表1 select * from 表2；
      将表2中部分列复制到表一中:insert into 表1 （列1，列2） select 列1，列2 from 表2 ；
2.更新表记录：update 表名 set 列名=值 [where 条件表达式]        （可以同时更新一个或多个字段）
            eg（将所有的性别修改成女）:update student set sex='女'；
               （将id为2的学生性别修改为男）：update student set sex='男' where id=2;
               (将id等于3的学生，年龄改成26岁，住址改为北京)：update student set age=26,address='北京' where id=3;
3.删除表记录：delete from 表名 [where 条件表达式]；（如果没有条件表达式表中所有记录将被删除）；
            eg（删除id为1的数据）:delete from student where id=1;
4.DQL查询表中数据：select 列名 from 表名 [where 条件表达式]
                eg（查询所有学生）：select * from student;
  4.1 查询指定列：select 字段1，字段2... from 表名;
              eg（查询student表中的name和age列）：select name,age from student;
  4.2 指定列的别名进行查询
        对列指定别名：select 字段1 AS 别名，字段2 AS 别名... from 表名；
  4.3 去除重复值：select distinct 字段名 from 表名 ；   eg（查询学生来自于哪些地方）：select distinct address from student;
  4.4 查询结果参与运算：eg（所有数学加5分）：select math+5 from student;
5.条件查询：select 字段名 from 表名 where 条件；
   5.1创建一个学生表，包含以下列：
       CREATE TABLE student3 (
           id int, -- 编号
           name varchar(20), -- 姓名
           age int, -- 年龄
           sex varchar(5), -- 性别
           address varchar(100), -- 地址
           math int, -- 数学
           english int -- 英语
    );

            
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                  
