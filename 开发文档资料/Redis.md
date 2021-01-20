# Redis学习

## 1.Nosql 概述

> 1.单机Mysql 的时代

思考：网站瓶颈是什么？

1.数据量太大，一个机器放不下。

2.数据索引(B+tree)，一个机器内存放不下。

3.访问量(读写混合)，一个服务器承受不了。

> 2.Memcached (缓存) + MySQL + 垂直拆分（读写分离）



![image-20210121030720067](F:\gitproject\demo\开发文档资料\images\Redis\2.png)



## 2.什么是NoSQL

No SQL = Not Only SQL(不仅仅是SQL)

关系型数据库：表格 ，行 ，列。

很多的数据类型用户的个人信息，社交网络，地理位置。这些数据类型的存储不需要一个固定的格式。不需要多余的操作就可以横向扩展的！Map<Stirng,Object> 使用键值对来控制

> NoSQL 特点

1.方便扩展（数据之间没有关系，很好扩展）

2.大数据量高性能（Redis 一秒读取11万 写8万，NoSQL 的缓存 记录级，性能比较高）

3.数据类型是多样的！(不需要实现设计数据库！随取随用！如果数据量十分大的表，跟多人就没法设计了)

4.传统 RDBMS 和 NoSQL

``` 
传统的 RDBMS
- 结构化组织
- SQL
-数据和关系都存在单独的表中
-操作，数据定义语言
-严格的一致性
- 基础的事务
```



``` 
NoSQL 
-不仅是数据
-么有固定的查询语言
- 键值对存储，列存储，文档存储，图形数据库（社交关系）
- 最终一致性
- CAP 定理BASE 
- 高性能 高可用 ，搞扩张
```

> 了解 3V+ 3高

大数据时代3V ：主要描述问题

​	1.海量Volume

​	2.多样

​	3. 实时

![image-20210121041807658](F:\gitproject\demo\开发文档资料\images\Redis\3.png)





![image-20210121041905833](F:\gitproject\demo\开发文档资料\images\Redis\4.png)



## 3.Redis 入门

**概述**

Redis（Remote Dictionary Server )，即远程字典服务

是一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库/103728)，并提供多种语言的API。从2010年3月15日起，Redis的开发工作由VMware主持。从2013年5月开始，Redis的开发由[Pivotal](https://baike.baidu.com/item/Pivotal)赞助

> Redis 能干啥？

1.内存存储，持久化，内存中是断电既失，所以持久化很重要（rdb ，aof）

2.效率高，可以用以告诉缓存

3.发布订阅系统

4.地图信息分析

5.计数器（浏览区），计时器

> 特性

1.多样的数据类型

2. 持久化

3. 集群

4. 事务

   

**Windows 安装**

  



**Linux 安装**