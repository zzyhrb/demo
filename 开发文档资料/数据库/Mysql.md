# Mysql 配置

## 1 .配置文件(my.ini)

```java 
[mysqld]
basedir=F:\dataBase\mysql-5.7.21-winx64\
datadir=F:\dataBase\mysql-5.7.21-winx64\data\
port=3306
event_scheduler=ON # 开启定时任务
#basedir表示mysql安装路径
#datadir表示mysql数据文件存储路径
#port表示mysql端口
#skip-grant-tables#表示忽略密码
max_connections=10000 # 最大连接数量
```

> 存储过程创建于调用

``` sql  
-- 创建
DELIMITER $  --声明一个结束标识
create  proceDure myp1()
begin
	insert into sys_loginfo (loginname,loginip) values ('1','12.1.4.1'),('2','4.5.6.8');
end $
-- 调用
CALL   myp1() $

```

# Mysql（基础篇）

##  1. 安装



## 2. 命令

```   shell
sc delete mysql   #清空服务
select version() # 查看mysql 版本
# 1 修改密码 2 刷新权限
update mysql.user set authentication_string=PASSWORD('123456') where user='root' and
HOST = 'localhost'  # 1.修改root 密码

flush privileges   # 2. 刷新权限

desc  [表明]     # 显示表结构

select  @@auto_increment_increment  # 查询自增的步长
```







> 数据库 xxx 语言

* DDL 定义

* DML  操作

* DQL  查询

* DCL    控制

  



## 3.操作 数据库

### 3.1 数据库列类型

> 数值

* tinyint		十分小的数据					1 个字节
* smallint      较小的数据                       2个字节
* mediumint  中等大小的数据              3 个字节
* int               标准整数                            4个字节    （常用）
* bigint        较大的数据                      8个字节
* float         浮点数                              4个字节
* double     浮点数                              8个字节
* decimal     字符串形式的浮点数   金融计算的时候，一般是使用decimal



> 字符串



* char    字符串固定大小      0-255
* varchar   可变字符串  0-65535  常用变量   string
* tinytext  微型文本   2^8-1
* text    文本串    2^16-1          保存大文本

> 时间

	* date        YYYY-MM-DD  日期
	* time       HH:mm:ss  时间格式
	* datetime   YYYY-MM-DD  HH:mm:ss  常用时间格式
	* timestamp  时间戳    1970.1.1 到现在的毫秒数   
	* year   年份

> null

*  没有值 ， 未知
*  注意，不要用null 进行运算，结果为null

### 3.2 数据库的字段属性（重点）



Unsigned:

*  无符号的整数
*  声明了该列不能声明为负数



zerofill：

* 0 填充
* 不足的位数，使用0填充， int(3), 5 --005



自增

* 可自定义设计主键的起始值 和不长
* 新增数据后主键id 自动增长

非空

* 假设设置为not null  如果不给他赋值，就会报错
* null ,如果不填写值 ，默认就是null

默认:

* 设置默认的值
* sex ，默认是为男， 如果不指定该列的值 则会有默认的值

番外篇：

``` shell
id			 主键
version 	 乐观锁
is_delete	 伪删除
gmt_create 	 创建时间
gmt_update	 修改时间
```



``` sql 
show create database ryoa   --查看创建数据库sql 语句
CREATE DATABASE `ryoa` /*!40100 DEFAULT CHARACTER SET utf8mb4 */
show create table sys_log    -- 查看创建表sql 语句
CREATE TABLE `sys_log` (
  `id` bigint(18) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `user_id` bigint(18) NOT NULL COMMENT '用户ID',
  `username` varchar(50) NOT NULL COMMENT '登录名称',
  `operation` varchar(150) NOT NULL COMMENT '操作功能',
  `forward_action` varchar(300) NOT NULL COMMENT '操作uri',
  `ip` varchar(255) DEFAULT NULL COMMENT 'IP',
  `browser` varchar(100) DEFAULT '0' COMMENT '浏览器',
  `os` varchar(100) DEFAULT NULL COMMENT '系统',
  `time` bigint(20) NOT NULL DEFAULT '0' COMMENT '请求耗时。毫秒',
  `create_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 ROW_FORMAT=DYNAMIC COMMENT='日志表'
```

### 3.3 数据库引擎

``` txt
--- 关于数据库引擎
InnoDB   默认使用
MyISAM   早些年使用
```



|            | MyISAM | InnoDB        |
| ---------- | ------ | ------------- |
| 事务支持   | 不支持 | 支持          |
| 数据行锁定 | 不支持 | 支持          |
| 外键索引   | 不支持 | 支持          |
| 全文索引   | 支持   | 不支持        |
| 表空间大小 | 较小   | 较大，约为2倍 |
|            |        |               |

常规使用操作:

* MyISAM 		 节约空间，速度较快
* InnoDB       安全性高，事务处理，多表多用户操作



> 在物理空间存在的位置

所有数据文件都在data 目录下，一个文件夹 对应一个数据库 ，本质还是文件的存储！

mysql 引擎在物理文件上的区别

* innoDB  在数据库表中只有一个*.frm 文件
* MyiSAM 对应文件
  * *.frm  表结构定义文件
  * *.MYD 数据文件（data）
  * *.MYI  索引文件（index）



> 设置数据库表的字符集编码

不设置的话会是mysql 默认的字符集（不支持中文）

MySQL 的默认编码是Latin1 ，不支持中文

在my.ini 中配置默认的编码

> character-set-server=utf8



> 删除表



``` sql 
---- 删除表（如果表存在在删除）
deop table if exists teacher1
```

 

注意点：



* ’‘ 字段名，使用'' 包裹！
* 注释 --  /* */
* sql 关键字大小写不敏感，建议写小写
* 所有符号全部用英文！



## 4.MySql 数据管理

###  4.1 外键 

【强制】 不得使用外键与级联， 一切外键概念必须在应用层解决



### 4.2 DML 语言（全记住）

``` sql 
1. 插入语句
insert into 表名（字段1，字段2） values(值1 ，值2)

2.修改
update 表明 set calum_name=value, where 条件

3.删除
delete  from 表明  where  [条件]

4.查询

--函数 concat(a,b)  拼接
select CONCAT('姓名:',studentname) as 新名字 from student

```



> 去重  distinct



### 4.3 where 条件字句

| 运算符      | 语法                | 描述                                |
| ----------- | ------------------- | ----------------------------------- |
| is null     | a is null           | 如果操作符为null 结果为 真          |
| is not null | a is not null       | 如果操作符不为null 结果 为真        |
| between     | a between  b and  c | 若 a  在b 和c 之间  则结果为真      |
| like        | a like b            | sql 匹配，如果 a 匹配b  则 结果为真 |
| in          | a in (a1,a2,a3)     | 假设 a 存在 a1 或者a2  结果为真     |



### 4.4 关联查询

``` sql 
内连接 INNER JOIN    左连接 LEFT JOIN   又连接 RIGHT JOIN
```





### 4.5 分页和排序

``` sql 
=========================
limit 0,5  // (当前页，每页显示数量) 公式：（n-1）*5

-- [pageSize:页面大小]
--【(n-1)*pageSize:起始值】
-- [n:当前页]
-- [总数/页面大小 = 总页数]

```



### 4.6 子查询



## 5  mySql函数



### 5.1 函数

``` sql  
select ABS(-8)   -- 绝对值
select CEILING(9.4)  -- 向上取整
select FLOOR(9.4)  -- 向下取整
select RAND()    -- 返回一个0-1 之间的随机数
select SIGN(10)   -- 判断一个数的符号 0-0 负数返回-1 正数返回1 

select CHAR_LENGTH('开始了吗？')   -- 字符串长度
select CONCAT('今天','心情','棒棒的')  -- 字符串拼接
select insert ('我爱吃饺子',1,2,'超级爱')  -- 查询 ，从某个位置开始替换某个长度

```



### 5.2  聚合函数

``` sql 

```



### 5.3 流程函数

``` sql 
--1. if 函数 
select if(10>5,'大','小')   // 执行结果为大
-- 2.case  函数 case when  else end   （when  后面等值比较  还可以i添加条件判断）
select pwd , status, 
case status 
when 0 then '是'
when 1/  status >1 then '否' else '五'
end  as s 
from tbl_user


```





## 6. 事务



> 事务原则: ACID  原则 原子性，一致性， 隔离性 ，持久行  (脏读，  幻读。。。。)



**原子性**: 

要么都成功  要么都失败

**一致性 **

一个事务可以从一个一致的状态切换到另一个一至的状态

**隔离性**

一个事务不受其他事务的干扰，多个事务相互隔离

**持久行**

一个事务一旦提交，则永久保存到本地

 

> 事务的使用步骤

隐式(自动)事务:没有明显的开启和结束，本身就是一条事务可以自动提交，比如insert ,update ，delete

显示事务:  具有明显的开始和结束

> 使用显示事务

``` sql 
----1.开启事务
set autocommit=0；--当前session禁用自动提交事物，自此句执行以后，每个SQL语句或者语句块所在的事务都需要显示"commit"才能提交事务。
START TRANSACTION  --- 可以省略
```



| 能否决绝                            | 脏读 | 不可重复 | 幻读 |
| ----------------------------------- | ---- | -------- | ---- |
| read uncommitted：读未提交          | 不能 | 不能     | 不能 |
| read committed：读已提交            | 能   | 不能     | 不能 |
| repeatable read ：可重复度（mysql） | 能   | 能       | 不能 |
| serializable：串行化                | 能   | 能       | 能   |





## 7.  视图

> 含义: 虚拟表 ，和普通表一样使用

``` sql 
----1. 创建视图语句
CREATE VIEW <视图名> AS <SELECT语句>
--- 2. (1)修改视图
	create or replace view <视图名> AS <SELECT语句>
	--(2)
	alter view  <视图名>
	
--- 3.删除视图
语法 : DROP VIEW <视图名1> [ , <视图名2> …]


```

|      | 创建语法      | 是否占用物理空间      | 使用                         |
| ---- | ------------- | --------------------- | ---------------------------- |
| 视图 | create   view | 只是保存 了 sql  逻辑 | 增删改查 （y一般不能增删改） |
| 表   | create table  | 保存了数据            | 增删改查                     |
|      |               |                       |                              |

## 8.存储过程

### 8.1 变量

 **系统变量**

* 全局变量
* 会话变量

**自定义变量**

* 用户变量
* 局部变量

> 系统变量

说明:  变量由系统提供，不是用户定义，属于服务器层面

> 使用语法

``` sql 
SHOW GLOBAL VARIABLES; --全局变量
SHOW SESSION VARIABLES; --会话变量

查看满足条件的部分系统变量
show global| [session] variables like '%char%'
查看指定的某个系统变量值
1.方式1
set global |[Session]   系统变量名=值;
2.方式2
set @@global|[session].系统变量名=值;

select @@global.autocommit -- 查询指定全局变量的值
select @@tx_isolation
set @@ global.autocommit=0  -- 为某个指定的全局变量赋值

```

>  会话变量



``` sql 
set  session tx_isolation ='read-committed'
```



> 自定义变量

1. 声明并初始化

   ``` sql 
   set @用户变量名 = 值; 或
   set @用户变量名 := 值;
   select @用户变量名 :=值;
   ```

   

> 赋值



``` sql 
方式一：
set @用户变量名 = 值; 或
set @用户变量名 := 值;
select @用户变量名 :=值;、

方式二: 通过 select into 
select 字段 into @变量名 from 表名

案例 ：
set  @name ='zy'
set  @name=100
set @count=1

select count(*) into @count
from 表名

select @count


```

> 局部变量：仅仅在定义的begin  end  中有效



1.声明

declare  变量名 类型；

declate  变量名 类型 default 值；

2.赋值

方式一：

通过 set  或 insert 

set @用户变量名 = 值; 或
set @用户变量名 := 值;
select @用户变量名 :=值;

方式二：通过 select  into  

selest   字段  into 局部变量名   from 表名

3. 使用

   select  局部变量名；



|          | 作用域          | 定义和使用的位置                  | 语法                        |
| -------- | --------------- | --------------------------------- | --------------------------- |
| 用户变量 | 当前会话        | 会话中的任何位置                  | 必须加@ 符号 ，不用限定类型 |
| 局部变量 | begin  end   中 | 只能在begin end 中  且为 第一句话 | 不用加@ 需要限定类型        |



### 8.2 存储过程和方法



> 创建语法

``` sql 
1.创建
create procedure  存储过程名(参数列表)

begin 
	存储过程体(一组合法的sql )

end

注意: 参数列表包含三部分
参数模式  参数名  参数类型
举例:
IN stuname  varchar(20)

参数模式：
IN 
OUT
INOUT
	
2. 调用语法


```

> 案例1

```  sql 
CREATE PROCEDURE myp4 (in login_name varchar(20),in pwd varchar(20))
begin 
	declare result int default 0;  # 声明并初始化
	select count(1) into result 
	from tbl_user
	where tbl_user.login_name=LOGIN_NAME
	and tbl_user.pwd=pwd;
	select result;
end 
	
CALL myp4('root','Hckj201509..')
```

> 带out 模式的存储过程



``` sql
CREATE PROCEDURE myp5 (in login_name varchar(20),out agencyname varchar(20))
begin 
	select tbl_agency.ORGAN_NAME  from tbl_user inner join tbl_agency on tbl_user.POWERGUID =tbl_agency.POWERGUID where tbl_user.LOGIN_NAME=login_name;
end 
CALL myp5('tly_hs',@agencyname)

```

> 



> 存储过程删除



``` sql 
语法 ：drop  procedure  存储过聪明
```



## 9.函数

### 9.1 创建语法

 ```` sql 
1.创建语法
create function  函数名（参数列表） returns 返回类型
begin
	函数体
end

--注意
1.参数列表包含两部分:参数名  参数类型

2.函数体:肯定有reurn 语句，如果没有就会报错
如果return 语句没有放在函数体的最后也不报错，但不建议
3.函数体中仅有一句话，则可以省略begin end
4.使用delimiter 语句设置结束标记

 ````

> 案例



``` sql 
---1.无参有返回的
create function myf1() returns int
begin
	declare nu int DEFAULT 0;
	select count(1) into  nu  from  tbl_user;
	return nu;
END
---2.



```

