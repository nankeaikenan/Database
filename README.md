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
    -- 查询 math 分数大于 80 分的学生
      select * from student3 where math>80
    -- 查询 english 分数小于或等于 80 分的学生
      select * from student3 where english<=80
    -- 查询 age 等于 20 岁的学生
      select * from student3 where age=20
    -- 查询 age 不等于 20 岁的学生，注：不等于有两种写法
      select * from student3 where age!=20
      select * from student3 where age<>20
    -- 查询 age 大于 35 且性别为男的学生(两个条件同时满足)
      select * from student3 where age>35 and sex='男';
    -- 查询 age 大于 35 或性别为男的学生(两个条件其中一个满足)
      select * from student3 where age>35 or sex='男';
    -- 查询 id 是 1 或 3 或 5 的学生
      select * from student3 where id=1 or id=3 or id=5;
 6  6.1in关键字：select 字段名 from 表名 where 字段 in(数据1，数据2...);
              in里面每个数据都会作为一个条件，只要满足条件就会显示
             eg（查询id是1,3,5的学生）：select * from student3 where id in(1,3,5);
             eg（查询id不是1,3,5的学生）：select * from student3 where id not in(1,3,5);
    6.2 范围查询：between 值1 AND 值2
         表示值1到值2的范围，包头又包尾
         --查询 english 成绩大于等于 75，且小于等于 90 的学生
            select * from student3 where english between 75 and 90;
    6.3 like关键字
        like表示模糊查询：select * from 表名 where 字段名 like '通配符字符串'
        通配符字符串：%  匹配任意多个字符串
                    _  匹配一个字符
        -- 查询姓马的学生
          select * from student3 where name like '马%'；
        -- 查询姓名中包含'德'字的学生
          select * from student3 where name like '%马%'
        -- 查询姓马，且姓名有两个字的学生
          select * from student3 where name like '马_'
 7 7.1 单列排序：只按某一字段进行排序:SELECT 字段名 FROM 表名 WHERE 字段=值 ORDER BY 字段名 [ASC|DESC];
            ASC: 升序，默认值      DESC: 降序
            -- 查询所有数据,使用年龄降序排序            
                select * from student order by age desc;
       组合排序：SELECT 字段名 FROM 表名 WHERE 字段=值 ORDER BY 字段名 1 [ASC|DESC], 字段名 2 [ASC|DESC];
            同时对多个字段进行排序，如果第 1 个字段相等，则按第 2 个字段排序，依次类推。
              -- 查询所有数据,在年龄降序排序的基础上，如果年龄相同再以数学成绩升序排序
                select * from student3 order by age,
   7.2 聚合函数：max(列名) 求这一列的最大值
                min(列名) 求这一列的最小值
                avg(列名) 求这一列的平均值
                count(列名) 统计这一列有多少条记录
                sum(列名) 对这一列求总和
         eg:-- 查询年龄大于 20 的总数
              select count (*) from student where age>20；*（为了后面不是斜体）
            -- 查询数学成绩总分
              select sum(math) from student;
            -- 查询数学成绩平均分
              select avg(math) from student;
            -- 查询数学成绩最高分
              select max(math) from student;
            -- 查询数学成绩最低分
              select min(math) from student;
   7.3 分组（一般分组会跟聚合函数一起使用）：SELECT 字段 1,字段 2... FROM 表名 GROUP BY 分组字段 [HAVING 条件];        
         eg1:--查询男女各多少人
              1) 查询所有数据,按性别分组。
              2) 统计每组人数 
                  selecct sex,count(*) from student group by sex;*
         eg2 --查询年龄大于 25 岁的人,按性别分组,统计每组的人数
                1) 先过滤掉年龄小于 25 岁的人。
                2) 再分组。
                3) 最后统计每组的人数
                  select sex,count(*) from student where age>25 group by sex;*
         eg3 --查询年龄大于 25 岁的人，按性别分组，统计每组的人数，并只显示性别人数大于 2 的数据(对分组查询的结果再进行过滤)
                select sex,count(*) from student where age>25 group by sex having count(*) >2;*
        3.3.1 having 与 where 的区别
                where子句 对查询结果进行分组前，将不符合 where 条件的行去掉，即在分组之前过滤数据，即先过滤
                          再分组。where 后面不可以使用聚合函数
                having子句的作用是筛选满足条件的组，即在分组之后过滤数据，即先分组再过滤。
                          having 后面可以使用聚合函数        
    7.4 limit语句：LIMIT offset,length; 
                  offset：起始行数，从 0 开始计数，如果省略，默认就是 0 
                  eg:-- 查询学生表中数据，从第 3 条开始显示，显示 6 条。
                          select * from student limit 2,6;
                  使用场景：
                        分页：比如我们登录京东，淘宝，返回的商品信息可能有几万条，不是一次全部显示出来。是一页显示固定的
                              条数。 假设我们每页显示 5 条记录的方式来分页。
                                -- 如果第一个参数是 0 可以省略写：
                                      select * from student3 limit 5;
   7.5 数据库表的约束
         约束种类：
          约束名    约束关键字                      特点         
          主键      primary key                   唯一、非空                                                     
          唯一      unique      
          非空      not null
          外键      foreign key
          检查约束   check 注：mysql 不支持
      7.5.1 创建主键方式：
            1. 在创建表的时候给字段添加主键:字段名 字段类 primary key
            2. 在已有表中添加主键:ALTER TABLE 表名 add primary key
      7.5.2 删除主键：alter table 表名 drop primary key
      7.5.3 主键自增：AUTO_INCREMENT 表示自动增长(字段类型必须是整数类型)
            1.概念：如果某一列是数值类型的，使用 auto_increment 可以来完成值得自动增长
            2.在创建表时，添加主键约束，并且完成主键自增长
            create table stu(
              id int primary key auto_increment,-- 给id添加主键约束
              name varchar(20)
            );
            3. 删除自动增长：ALTER TABLE stu MODIFY id INT;
			      4. 添加自动增长：ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;   
            5.创建表时指定起始值（默认为1）
                CREATE TABLE 表名(
                列名 int primary key AUTO_INCREMENT
                ) AUTO_INCREMENT=起始值;
            6.       
      7.5.4 唯一约束：表中某一列不能出现重复的值
            字段名 字段类型 UNIQUE
      7.5.5 非空约束：某一列不能为 null。
      7.5.6 默认值：
            -- 创建一个学生表 st9，包含字段(id,name,address)， 地址默认值是广州
                create table st9 (
                 id int,
                 name varchar(20),
                 address varchar(20) default '广州'
                )
            -- 添加一条记录,使用默认地址
                insert into st9 values (1, '李四', default);
                  elect * from st9;
   7.6 外键约束
        1. 在创建表时，可以添加外键
          * 语法：
            create table 表名(
              ....
              外键列
              constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
            );
        2. 删除外键
          ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
        3. 创建表之后，添加外键
          ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
	4. 级联操作
	  1. 添加级联操作
		语法：ALTER TABLE 表名 ADD CONSTRAINT 外键名称 
		FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE  ;
	  2. 分类：
		1. 级联更新：ON UPDATE CASCADE 
		2. 级联删除：ON DELETE CASCADE 	  
    7.7  数据库的设计
	1. 多表之间的关系
		1. 分类：
			1. 一对一(了解)：
				* 如：人和身份证
				* 分析：一个人只有一个身份证，一个身份证只能对应一个人
			2. 一对多(多对一)：
				* 如：部门和员工
				* 分析：一个部门有多个员工，一个员工只能对应一个部门
			3. 多对多：
				* 如：学生和课程
				* 分析：一个学生可以选择很多门课程，一个课程也可以被很多学生选择
		2. 实现关系：
			1. 一对多(多对一)：
				* 如：部门和员工
				* 实现方式：在多的一方建立外键，指向一的一方的主键。
			2. 多对多：
				* 如：学生和课程
				* 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两					    张表的主键
			3. 一对一(了解)：
				* 如：人和身份证
				* 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。                     
     7.8  数据库设计的范式  
     		* 分类：
			1. 第一范式（1NF）：每一列都是不可分割的原子数据项
			2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于码（在1NF基础上消除非主属性对主码的部分函数依赖）
					  2NF是对记录的惟一性，要求记录有惟一标识，即实体的惟一性，即不存在部分依赖；
			3. 第三范式（3NF）：在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）
					  3NF是对字段的冗余性，要求任何字段不能由其他字段派生出来，它要求字段没有冗余，即不存在传递依赖；
8、 多表查询
	8.1 笛卡尔积：
		* 有两个集合A,B .取这两个集合的所有组成情况。
		* 要完成多表查询，需要消除无用的数据
	8.2 * 多表查询的分类：
		1. 内连接查询：
			1. 隐式内连接：使用where条件消除无用数据
				* 例子：
				-- 查询所有员工信息和对应的部门信息
				SELECT * FROM emp,dept WHERE emp.`dept_id` = dept.`id`;				
				-- 查询员工表的名称，性别。部门表的名称
				SELECT emp.name,emp.gender,dept.name FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
				SELECT 
					t1.name, -- 员工表的姓名
					t1.gender,-- 员工表的性别
					t2.name -- 部门表的名称
				FROM
					emp t1,
					dept t2
				WHERE 
					t1.`dept_id` = t2.`id`;
			2. 显式内连接：
				* 语法： select 字段列表 from 表名1 [inner] join 表名2 on 条件
				* 例如：
					* SELECT * FROM emp INNER JOIN dept ON emp.`dept_id` = dept.`id`;	
					* SELECT * FROM emp JOIN dept ON emp.`dept_id` = dept.`id`;	
			3. 内连接查询：
				1. 从哪些表中查询数据
				2. 条件是什么
				3. 查询哪些字段
		2. 外链接查询：
			1. 左外连接：
				* 语法：select 字段列表 from 表1 left [outer] join 表2 on 条件；
				* 查询的是左表所有数据以及其交集部分。
				* 例子：
					-- 查询所有员工信息，如果员工有部门，则查询部门名称，没有部门，则不显示部门名称
					SELECT 	t1.*,t2.`name` FROM emp t1 LEFT JOIN dept t2 ON t1.`dept_id` = t2.`id`;
			2. 右外连接：
				* 语法：select 字段列表 from 表1 right [outer] join 表2 on 条件；
				* 查询的是右表所有数据以及其交集部分。
				* 例子：
					SELECT 	* FROM dept t2 RIGHT JOIN emp t1 ON t1.`dept_id` = t2.`id`;
		3. 子查询：
			* 概念：查询中嵌套查询，称嵌套查询为子查询。
				-- 查询工资最高的员工信息
				-- 1 查询最高的工资是多少 9000
				SELECT MAX(salary) FROM emp;
				-- 2 查询员工信息，并且工资等于9000的
				SELECT * FROM emp WHERE emp.`salary` = 9000;
				-- 一条sql就完成这个操作。子查询
				SELECT * FROM emp WHERE emp.`salary` = (SELECT MAX(salary) FROM emp);
			* 子查询不同情况
				1. 子查询的结果是单行单列的：
					* 子查询可以作为条件，使用运算符去判断。 运算符： > >= < <= =
					-- 查询员工工资小于平均工资的人
					SELECT * FROM emp WHERE emp.salary < (SELECT AVG(salary) FROM emp);
				2. 子查询的结果是多行单列的：
					* 子查询可以作为条件，使用运算符in来判断
					-- 查询'财务部'和'市场部'所有的员工信息
					SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部';
					SELECT * FROM emp WHERE dept_id = 3 OR dept_id = 2;
					-- 子查询
				SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部');
				3. 子查询的结果是多行多列的：
					* 子查询可以作为一张虚拟表参与查询
					-- 查询员工入职日期是2011-11-11日之后的员工信息和部门信息
					-- 子查询
					SELECT * FROM dept t1 ,(SELECT * FROM emp WHERE emp.`join_date` > '2011-11-11') t2
					WHERE t1.id = t2.dept_id;					
					-- 普通内连接
				SELECT * FROM emp t1,dept t2 WHERE t1.`dept_id` = t2.`id` AND t1.`join_date` >  '2011-11-11'
					  
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                     
                  
