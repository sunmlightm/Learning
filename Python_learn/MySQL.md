#### 数据库介绍
- 类型:
    - 关系型数据库: (RDBMS):MySQL,Oracle,DB2,SQL Serve
    - 非关系型数据库(No SQL):MongoDB,Redis,键值对数据库,文档数据库


#### MySQL
- **数据库-->库-->表-->数据链**
- 安装启动
    - 安装mysql服务端: sudo apt install mysql-server
    - 安装mysql服务端:sudo apt install mysql-client
    - 检查是否安装成功:sudo netstat -tap | grep mysql
    - 关闭mysql服务器: service mysql stop
    - 开启mysql服务器:service mysql start
    - 重启: service mysql restart
    - 需要远程登陆时需要更改配置文件:
        - vim /etc/mysql/mysql.conf.d/mysqld.cnf
        - 将bind-address= 127.0.0.1注释掉
        - 重启数据库
- 进入MySQL数据库: mysql -uroot -p  --->输入密码
- 退出:ctrl+d /exit/quit
- 创建用户:grant all privileges on *. * to username@"%" identified by "password" with grant option;(grant:授权命令. %表示允许host操作)
- 修改密码:
    - 1.退出mysql
    - 2.mysqladmin -u用户名 -p旧密码 passwod 新密码
- 查看用户:1.use mysql; 2.select user,host from users;


#### 数据库操作
- 显示有哪些数据库:show databases;
- 选用某个数据库:use name;
- 查看某个表的结构:desc name;
- 查看当前使用的是那个数据库:select database();
- **创建数据库**: create databases name charset=utf8;

- 删除数据库:drop database name;

#### 数据表操作
- 把当前数据库所有表列出来:show tables;
- 创建表:

    create table 数据表名(

    id int(10)  auto_increment primary key not null,
    
    name varchar(40)
    
    ) charset=utf8;

- 查看所有信息:select * from name;
    - 查看id为1的学生表的数据:select * from students where id=1
    - 查看name为wukong的学生表的数据:select * from students where name='wukong';
- **删除数据表**:drop table tab_name;
- 
- 增加一条数据: insert into students(id,name) values(0,'wukong'),(0,'bajie');
- 删除一条数据:delete from 表名 删除全部
    - 删除id为13 : delete from students where id=13;
- 修改数据:
    - update 表名 set 列1=值1,... where 条件

#### 备份与恢复
- 备份:
    - 切换到root : sudo -s
    - 切换到/var/lib/mysql目录
    - mysqldump -uroot -p 数据库名 > ~/Desktop/备份文件.sql;
- 恢复:
    - 创建一个数据库
    - mysql -uroot -p test1 < atguigudb.sql;


#### 查询
- select * from 表名--->查询所有
    - select id,name from students;--->只查看id,name
- 取别名:as ---select id as 编号,name as 姓名 from students;
- 消除重复行:distinct---select distinct name from students;
- 条件 -where :
    - 比较运算符:=,>,>=,<,<=,!=或者<>
    - 逻辑运算符: and,or,not
    - 模糊查询:like--%表示任意多个字符 _表示一个字符
        - select * from students where name like '黄_'
    - 范围查询:in,between...and...
        - select * from students where id in(1,2,4)
        - select * from students where id between 3 and 8;
        - 空判断: is null---非空判断:is not null
- 聚合
    - COUNT	计算表中的记录（行数）---select count(*) from students;
    - SUM	计算表中数值列的数据合计值(只适用于数值型的列)---select sum(id) from students where gender=1;
    - AVG	计算表中数值列的数据平均值(只适用于数值型的列)---select avg(id) from students where isdelete=0 and gender=0;
    - MAX	求出表中任意列中数据的最大值---select max(id) from students where gender=0;
    - MIN	求出表中任意列中数据的最小值---select min(id) from students where isdelete=0;
- 分组
    - 语法:select 列1,列2,聚合... from 表名 group by 列1,列2,列3...
        - select gender as 性别,count(*) from students group by gender;
        - select isdelete as 是否删除, count(*)  from students group by isdelete;
    - 分组后的数据筛选
        - select 列1,列2,聚合... from 表名 group by 列1,列2,列3... having 列1,...聚合...
    - select count(*) from students where gender=1;
    - select gender as 性别,count(*) from students group by gender having gender=1;


- 排序:
    - select * from 表名 order by 列1 asc|desc,列2 asc|desc,...
    - 默认按照列值从小到大排列
    - asc从小到大排列，即升序
    - desc从大到小排序，即降序
    - select * from students where gender=1 and isdelete=0 order by id asc,name;
- 分页select * from 表名limit start,count
    - 分页公式:select * from 表名 limit (n-1) * m,m
