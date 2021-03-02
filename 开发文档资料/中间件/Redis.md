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

  下载地址：https://github.com/dmajkic/redis/releases



1,解压完成后，双击运行启动。

2.使用Redis  客户端连接Redis



# Redis 安装配置

![图片](F:\gitproject\demo\开发文档资料\images\redis-01.png)



## 1.安装

```jaiva
1.创建挂在文件目录 [root] #mkdir -p /mydata/redis/conf 
2.创建配置文件 【root】# touch redis.conf 
3.【root】#docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \ > -v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \ > -d redis redis-server /etc/redis/redis.conf 
4.查看运行状态 【root】#docker ps
```

## 2.测试

```javascript
[root@iZ2zedq4zbdzwebsgsxi9bZ conf]# ls redis.conf [root@iZ2zedq4zbdzwebsgsxi9bZ conf]# docker exec -it redis redis-cli 127.0.0.1:6379> set a b OK 127.0.0.1:6379> get a "b" 127.0.0.1:6379>
```









**Linux 安装**

1.下载安装包！ Redis-6.0.6.tar.gz

2.解压Redis 的安装包！ 程序/opt

3.进入解压后的文件，查看我们redis的配置文件

![](F:\gitproject\demo\开发文档资料\images\Redis\6.png)

4.安装基本环境安装

```
1.安装  1.yum install gcc-c++
       2.make 
       3.make install
       
2.注意 如出现错误：  Centos7安装redis6.0.3，报错make[1]: *** [server.o] Error 1的解决  
yum -y install centos-release-scl

yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils

scl enable devtoolset-9 bash

echo "source /opt/rh/devtoolset-9/enable" >> /etc/profile

gcc -v

make 和make install以后即可。注意安装完成以后redis-server在/usr/local/bin/目录下。
       
```

5.安装完后

![](F:\gitproject\demo\开发文档资料\images\Redis\7.png)

 出现上图证明安装完成

6.redis  的默认安装路径 、/user/local/bin

![](F:\gitproject\demo\开发文档资料\images\Redis\8.png)

7.将redis 配置文件复制到我们当前的目录下

![](F:\gitproject\demo\开发文档资料\images\Redis\9.png)

8.redis 默认不是后台启动的，修改配置文件

```xml
# vim redis.conf
```

![](F:\gitproject\demo\开发文档资料\images\Redis\13.png)

9.启动 Redis 服务 

查看当前目录

```
# pwd
通过指定的配置文件启动服务
```

![](F:\gitproject\demo\开发文档资料\images\Redis\14.png)

10.使用命令测试

```javascript
[root@iZ2zedq4zbdzwebsgsxi9bZ bin]# redis-cli -p 6379
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> set name zzy
OK
127.0.0.1:6379> get name
"zzy"
127.0.0.1:6379> kays *
(error) ERR unknown command `kays`, with args beginning with: `*`,
127.0.0.1:6379> keys *
1) "aa"
2) "name"
127.0.0.1:6379>

    
 

```

11.查看进程

![](F:\gitproject\demo\开发文档资料\images\Redis\15.png)

12.如何关闭Redsi 服务命令

>shutdown 
>
>exit

## 4.性能测试

![](F:\gitproject\demo\开发文档资料\images\Redis\16.png)

我们自己测试下：

>#测试：100个并发连接 10000请求
>
>#redis-benchmark -h localhost -p 6379 -c 100 -n 100000

  ![](F:\gitproject\demo\开发文档资料\images\Redis\17.png)



## 5.基础知识

* Redis 默认由16个数据库  默认使用第0个数据库 

  ```
  127.0.0.1:6379> ping
  PONG
  127.0.0.1:6379> get name
  (nil)
  127.0.0.1:6379> select 3   #切换数据库
  OK
  127.0.0.1:6379[3]> dbsize   #查看数据库大小
  (integer) 0
  127.0.0.1:6379[3]>
  
  ```

* 清空数据库

  ```
  ># flushdb       #清空当前数据库数据
  ># flushall      #清空所有数据
  ```

  思考：为啥端口号是6379

  



## 5.五大数据类型

>常用命令必须熟记
>
>1.EXISTS name   # 查看 key 是否存在。
>
>2.移除key 值 ：move name 1(当前数据库)
>
>3.key值设置失效时间 ：EXPTRE name 10（秒）
>
>4.查看失效时间 剩余：ttl  name
>
>5.查看当前key 类型 ： type name
>
>

### String (字符串)



```bash
# 字符串 获取
127.0.0.1:6379> APPEND name "helllo"   #追加字符串，如果当前key 不存在，就相当于setkey
(integer) 9
127.0.0.1:6379> get name
"zzyhelllo"
127.0.0.1:6379> STRLEN name  ",zy"
(error) ERR wrong number of arguments for 'strlen' command
127.0.0.1:6379> get name
"zzyhelllo"
127.0.0.1:6379> STRLEN name   #获取字符串长度
(integer) 9
127.0.0.1:6379>  append name ",ly"
(integer) 12
127.0.0.1:6379> get name
"zzyhelllo,ly"
127.0.0.1:6379>
#####################################
#i++
#步长 i+=
127.0.0.1:6379> set views 0  #初始浏览量为0
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> incr views  #自增 1
(integer) 1
127.0.0.1:6379> incr views
(integer) 2
127.0.0.1:6379> incr views
(integer) 3
127.0.0.1:6379> get views
"3"
127.0.0.1:6379> decr views  # 自减 1
(integer) 2
127.0.0.1:6379> INCRBY views 10  #设置步长指定增量 10
(integer) 12
127.0.0.1:6379> INCRBY views 10
(integer) 22
127.0.0.1:6379> DECRBY views 5
(integer) 17
127.0.0.1:6379>
##########################################################
#字符串范围 range
127.0.0.1:6379> get key
"hello,tiankong"
127.0.0.1:6379> GETRANGE key 0 3  # 截取字符串【0 ，3】
"hell"
127.0.0.1:6379> getrange key 0 -1 #截取全部字符串  和get key 是一样的
"hello,tiankong"
127.0.0.1:6379>

# 替换
127.0.0.1:6379> set key2 abcdefg
OK
127.0.0.1:6379> get key2
"abcdefg"
127.0.0.1:6379> setrange key2 1 xx # 替换指定位置开始的自发串！
(integer) 7
127.0.0.1:6379>  get key2
"axxdefg"
127.0.0.1:6379>

##############################################################
#setex(set with expire) #  设置过期时间 
#setnx(set if not exist) # 不存在在设置
127.0.0.1:6379> setex key3 30 "hello" #设置 key3 值为 hello  30秒过期
OK
127.0.0.1:6379> ttl key3
(integer) 23
127.0.0.1:6379> setnx mykey "redis" # 如果mykey 不存在 创建mykey
(integer) 1
127.0.0.1:6379> keys *
1) "key"
2) "mykey"
3) "key2"
127.0.0.1:6379>  ttl key3
(integer) -2
127.0.0.1:6379> setnx mykey "java" #如果 mykey 存在 ，创建失败。
(integer) 0
127.0.0.1:6379> get mykey
"redis"
127.0.0.1:6379>
##############################################################
#mset(批量设置值)
#mget(批量获取值)

127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3
OK
127.0.0.1:6379> keys *
1) "k1"
2) "k3"
3) "k2"
127.0.0.1:6379> mget k1 k2 k3
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> msetnx k1 v1 k4 v4 # msetnx 是一个原子性的操作，要么一起成功，要么一起失败。
(integer) 0
127.0.0.1:6379> get k4
(nil)
127.0.0.1:6379>

# 对象
set user:1 {name:zzy,age:3}  # 设置一个user:1 对象值为json 字符来保存一个对象。
#这里的key 是一个巧妙的设计 user:{id}:{filed},
127.0.0.1:6379> mset user:1:name zzy user:1:age 2
OK
127.0.0.1:6379> mget user:1name user:1:age
1) (nil)
2) "2"
127.0.0.1:6379> mget user:1:name user:1:age
1) "zzy"
2) "2"
127.0.0.1:6379>

##############################################################
getset #先get 在 set  
127.0.0.1:6379> getset db redis #如果不存在值返回nil
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db java #如果存在值，获取原来的值，并设置新的值
"redis"
127.0.0.1:6379> get db
"java"
127.0.0.1:6379>

##############################################################
```

### list(列表)

基本数据类型，列表

在redis 里面、可以吧list 玩出 。栈、队列、阻塞队列！

多有的list 命令都是以l开头的

```bash
##############################################################
127.0.0.1:6379> lpush list one # 将一个值或者多个值，插入到列表头部(左)
(integer) 1
127.0.0.1:6379> LPUSH list two
(integer) 2
127.0.0.1:6379> LPUSH list three
(integer) 3
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> LRANGE 0 1
(error) ERR wrong number of arguments for 'lrange' command
127.0.0.1:6379> LRANGE list 0 1
1) "three"
2) "two"
127.0.0.1:6379>
127.0.0.1:6379> RPUSH list right # 将一个值或者多个值，插入到列表头部(右)
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"
127.0.0.1:6379>


##############################################################
LPOP（左侧移除）
RPOP(右侧移除)
127.0.0.1:6379> LPOP list
"three"
127.0.0.1:6379> Rpop list
"right"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379>

##############################################################
Lindex(获取值)
127.0.0.1:6379> LINDEX list 1
"one"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> LINDEX list 1 #通过下标获取list中的值
"one"
127.0.0.1:6379>

127.0.0.1:6379> llen list  #返回列表长度
(integer) 2
127.0.0.1:6379>


##############################################################
# lrem(移除)

127.0.0.1:6379> lpush list three
(integer) 5
127.0.0.1:6379> lrem list 1 three #移除list 集合中指定个数的value 精确匹配
(integer) 1
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "three"
3) "two"
4) "one"
127.0.0.1:6379> lrem list 2 three
(integer) 2
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379>


##############################################################
trim  修剪：截断
127.0.0.1:6379> LRANGE list 0 -12
(empty array)
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> lpush list three
(integer) 3
127.0.0.1:6379> lpush list four
(integer) 4
127.0.0.1:6379> ltrim  list 1 2  # 通过下标截取指定长度。
OK
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
127.0.0.1:6379>

##############################################################
 rpoplpush # 移除列表的最后一个元素，将他移动到新的列表中
  127.0.0.1:6379> keys *
(empty array)
127.0.0.1:6379> rpush mylist "hello"
(integer) 1
127.0.0.1:6379> rpush mylist "hello1"
(integer) 2
127.0.0.1:6379> rpush mylist "hello2"
(integer) 3
127.0.0.1:6379> rpoplpush mylist myotherlist # 移除列表中最后一个元素，将其移动到新的列表中
"hello2"
127.0.0.1:6379> lrange mylist
(error) ERR wrong number of arguments for 'lrange' command
127.0.0.1:6379> lrange mylist 0 -1 # 查看原来的列表
1) "hello"
2) "hello1"
127.0.0.1:6379> lrange myotherlist 0 -1 # 查看新的列表
1) "hello2"
127.0.0.1:6379>

##############################################################
lset # 将列表中指定小标的值替换为另一个值，更新操作。
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> exists list  #判断这个列表是否存在
(integer) 0
127.0.0.1:6379> lset list 0 item # 不存在更新就会报错
(error) ERR no such key
127.0.0.1:6379> lpush list value1
(integer) 1
127.0.0.1:6379> lrange list 0 0
1) "value1"
127.0.0.1:6379> lset list 0 litm # 存在更新当前下标值。
OK
127.0.0.1:6379> lrange list 0 0
1) "litm"
127.0.0.1:6379> lset list 1 other # 不存在报错
(error) ERR index out of range
127.0.0.1:6379>


##############################################################
linsert # 将某个值插入到指定值得前面或者后面
127.0.0.1:6379> fulshdb
(error) ERR unknown command `fulshdb`, with args beginning with:
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> rpush mylist "hello"
(integer) 1
127.0.0.1:6379> rpush mylist "word"
(integer) 2
127.0.0.1:6379> linsert mylist before "word" "other"
(integer) 3
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "other"
3) "word"
127.0.0.1:6379>



##############################################################
```

> 小结

* list 实际上市一个链表，before Node after ,left ,right 都可以插入值
* 如果key不存在、创建新的链表
* 如果key存在、新增内容
* 如果移除了所有的值、空链表、也代表不存在
* 在两边插入或者改动值、效率最高!中间元素、相对来说效率会低一点。

消息排队！消息队列（Lpush Rpop）,栈（Lpush Lpop）

### Set (集合)

set 中的值时不能重复读的！

```bash
##############################################################
127.0.0.1:6379> sadd myset "hello" # set 集合添加元素
(integer) 1
127.0.0.1:6379> sadd myset "zzy"
(integer) 1
127.0.0.1:6379> sadd myset "lokay"
(integer) 1
127.0.0.1:6379> SMEMBERS myset  # 查看set 集合中元素
1) "hello"
2) "lokay"
3) "zzy"
127.0.0.1:6379> SISMEMBER myset hello # 判断元素是不是在set集合 中
(integer) 1
127.0.0.1:6379> sismember myset word
(integer) 0
127.0.0.1:6379>

127.0.0.1:6379> scard myset  # 获取set 集合中元素个数
(integer) 3
127.0.0.1:6379>

##############################################################
rem #移除
7.0.0.1:6379> srem myset hello # 移除set 集合中指定元素
(integer) 1
127.0.0.1:6379> scard myset
(integer) 2
127.0.0.1:6379> smember myset
(error) ERR unknown command `smember`, with args beginning with: `myset`,
127.0.0.1:6379> smember myset
(error) ERR unknown command `smember`, with args beginning with: `myset`,
127.0.0.1:6379> smembers myset
1) "lokay"
2) "zzy"
127.0.0.1:6379>

##############################################################
set 无序不重复集合
127.0.0.1:6379> smembers myset
1) "lokay"
2) "zzy"
127.0.0.1:6379> srandmember myset  # 随机抽取一个元素
"lokay"
127.0.0.1:6379> srandmember myset
"lokay"
127.0.0.1:6379> srandmember myset
"lokay"
127.0.0.1:6379> srandmember myset\
(nil)
127.0.0.1:6379> srandmember myset\
(nil)
127.0.0.1:6379> srandmember myset
"zzy"
127.0.0.1:6379>

##############################################################
删除指定的key 随机删除key

127.0.0.1:6379> SMEMBERS myset
1) "lokay"
2) "zzy"
127.0.0.1:6379> spop myset  # 随机删除key
"zzy"
127.0.0.1:6379> smembers myset
1) "lokay"
127.0.0.1:6379>
[root@iZ2zedq4zbdzwebsgsxi9bZ bin]#


##############################################################
将一个指定值移动到另外一个set集合中
27.0.0.1:6379> ping
PONG
127.0.0.1:6379> smembers myset
1) "lokay"
127.0.0.1:6379> sadd myset "timi"
(integer) 1
127.0.0.1:6379> sadd myset "tk"
(integer) 1
127.0.0.1:6379> smembers myset
1) "tk"
2) "lokay"
3) "timi"
127.0.0.1:6379> sadd  myset2 'xiaoh'
(integer) 1
127.0.0.1:6379> smove myset myset2  "tk" # 将一个指定元素移动到另一个set 集合中
(integer) 1
127.0.0.1:6379> smembers myset2
1) "tk"
2) "xiaoh"
127.0.0.1:6379>

##############################################################
微博 B站 共同关注（并集）
-- 差集
-- 交集
-- 并集
127.0.0.1:6379> sdiff key1 key2 -- 差集
1) "a"
2) "b"
127.0.0.1:6379> sinter key1 key2 -- 交集
1) "c"
127.0.0.1:6379> sunion key1 key2 -- 并集
1) "d"
2) "a"
3) "c"
4) "b"
127.0.0.1:6379>

```



### Hash（哈希）

Map 集合，key-map !时候这个值是一个map集合！本质和String 类型没有太大区别，还是一个简单的key-value

```bash
127.0.0.1:6379> hset myhash dield1 zzy  # set 一个具体的key -value
(integer) 1
127.0.0.1:6379> hget myhash gield1 
(nil)
127.0.0.1:6379> hget myhash dield1  # 获取一个值
"zzy"
127.0.0.1:6379> hset myhash field1 hello field2 word  #set 多个key-value
(integer) 2
127.0.0.1:6379> hmget myhash field1 field2
1) "hello"
2) "word"
127.0.0.1:6379> hgetall myhash
1) "dield1"
2) "zzy"
3) "field1"
4) "hello"
5) "field2"
6) "word"
127.0.0.1:6379>

127.0.0.1:6379> hdel myhash dield1  #删除hasha 指定的kay字段，对应的value值也就消失了。
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "field1"
2) "hello"
3) "field2"
4) "word"
127.0.0.1:6379>
##############################################################

127.0.0.1:6379> hlen myhash   # 获取字段数量
(integer) 2
127.0.0.1:6379>

##############################################################
127.0.0.1:6379> HEXISTS myhash dield1
(integer) 0
127.0.0.1:6379> HEXISTS myhash field1  # 判断hash 中指定字段是否存在！
(integer) 1
127.0.0.1:6379>


##############################################################
incr  decr

127.0.0.1:6379> hset myhash field3 5   #指定增量
(integer) 1
127.0.0.1:6379> HINCRBY myhash field3
(error) ERR wrong number of arguments for 'hincrby' command
127.0.0.1:6379> HINCRBY myhash field3 1
(integer) 6
127.0.0.1:6379> HINCRBY myhash field3 -1
(integer) 5
127.0.0.1:6379> hsetnx myhash field4 hello # 不存在可以设置
(integer) 1 
127.0.0.1:6379> hsetnx myhash field4 word # 存在不能设置
(integer) 0
127.0.0.1:6379>

```

hash 变更的数据username  age ,尤其是用户信息之类的，经常变动的信息！hash 更适合于对象的存储，String更适合字符串存储。

### Zset(有序集合)

在set基础上，增加一个值，set k1 v1 zset k1 score1 v1

```bash
127.0.0.1:6379> zadd myset 1 one  #添加一个值
(integer) 1
127.0.0.1:6379> zadd myset 2 two 3 three  # 添加多个值
(integer) 2
127.0.0.1:6379> ZRANGE myset 0 -1  # 查看
1) "one"
2) "two"
3) "three"
127.0.0.1:6379>
##############################################################
127.0.0.1:6379> zadd salary 2500 xiaoming  
(integer) 1
127.0.0.1:6379> zadd salary 5000 titi
(integer) 1
127.0.0.1:6379> zadd salary 1000 mimi
(integer) 1
127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf # 显示全部的用户 从小到大
1) "mimi"
2) "xiaoming"
3) "titi"
127.0.0.1:6379> ZREVRANGE salary 0 -1  # 显示全部的用户 从大到小
1) "titi"
2) "xiaoming"
3) "mimi"

127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf withscores # 显示全部的用户 从小到大附带成绩
1) "mimi"
2) "1000"
3) "xiaoming"
4) "2500"
5) "titi"
6) "5000"
127.0.0.1:6379> ZRANGEBYSCORE salary -inf 1000 withscores # 显示工资小于1000 的员工信息
1) "mimi"
2) "1000"
127.0.0.1:6379>
##############################################################
移除rem 中的元素

127.0.0.1:6379> zrange salary 0 -1
1) "mimi"
2) "xiaoming"
3) "titi"
127.0.0.1:6379> zrem salary mimi  # 移除有序集合中指定的元素
(integer) 1
127.0.0.1:6379> zrange salary 0 -1
1) "xiaoming"
2) "titi"
127.0.0.1:6379> zcard salary # 获取有序集合中的个数
(integer) 2
127.0.0.1:6379>

##############################################################
127.0.0.1:6379> zadd myset 1 hello
(integer) 1
127.0.0.1:6379> zadd myset 2 word 3 zzy
(integer) 2
127.0.0.1:6379> zcount myset 1 3 # 获取指定区间的成员数量
(integer) 6
127.0.0.1:6379> ZCOUNT myset 1 2
(integer) 4
127.0.0.1:6379>




```

## 三种得数数据类型

### geospatial 地理位置

朋友的定位，附近的人，

相关命令

- [GEOADD](http://www.redis.cn/commands/geoadd.html)

- [GEODIST](http://www.redis.cn/commands/geodist.html)

- [GEOHASH](http://www.redis.cn/commands/geohash.html)

- [GEOPOS](http://www.redis.cn/commands/geopos.html)

- [GEORADIUS](http://www.redis.cn/commands/georadius.html)

- [GEORADIUSBYMEMBER](http://www.redis.cn/commands/georadiusbymember.html)

  

官方文档：https://www.redis.net.cn/order/3685.html

> geoadd

```bash
# geoadd 添加地址位置
# 规则： 两级无法直接添加，我们一般会下载城市数据，直接通过java 程序一次性导入
# 有效的纬度从-85.05112878度到85.05112878度。
127.0.0.1:6379> geoadd china:city 116.40 39.90 beijing
(integer) 1
127.0.0.1:6379> geoadd china:city 121.47 31.23 shanghai
(integer) 1
127.0.0.1:6379> geoadd china:city 106.50 29.53 chongqing 114.05 22.52 shenzgen
(integer) 2
127.0.0.1:6379> geoadd china:city 120.16 30.24 hangzhou 108.96 34.26 xian
(integer) 2
127.0.0.1:6379>

```

> geopos
>
> 

```bash

127.0.0.1:6379> geopos china:city beijing # 获取指定的城市经纬度！
1) 1) "116.39999896287918091"
   2) "39.90000009167092543"
127.0.0.1:6379> geopos china:city beijing xian
1) 1) "116.39999896287918091"
   2) "39.90000009167092543"
2) 1) "108.96000176668167114"
   2) "34.25999964418929977"
127.0.0.1:6379>

```

> geodist

两人之间的距离！

- **m** 表示单位为米。
- **km** 表示单位为千米。
- **mi** 表示单位为英里。
- **ft** 表示单位为英尺。

```bash

127.0.0.1:6379> geodist china:city beijing xian # 查看北京到西安的直线距离
"910056.5237"
127.0.0.1:6379> geodist china:city beijing xian km
"910.0565"
127.0.0.1:6379>

```

> # Redis GEORADIUS 命令 - 以给定的经纬度为中心， 找出某一半径内的元素

附近人？（获取所有附近的人地址，定位！）通过半径来查询

获取指定的人数，200 

```bash
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km # 以100 30 经纬度为中心，寻找方圆1000 km 内的城市
1) "chongqing"
2) "xian"
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withdist # 显示到中间距离的位置
1) 1) "chongqing"
   2) "629.6756"
2) 1) "xian"
   2) "967.2846"
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withcode
(error) ERR syntax error
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withcoord # 显示他人定位信息
1) 1) "chongqing"
   2) 1) "106.49999767541885376"
      2) "29.52999957900659211"
2) 1) "xian"
   2) 1) "108.96000176668167114"
      2) "34.25999964418929977"
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withcoord count 1 # 筛选指定结果 
1) 1) "chongqing"
   2) 1) "106.49999767541885376"
      2) "29.52999957900659211"
127.0.0.1:6379>


```

> # Redis GEORADIUSBYMEMBER 命令 - 找出位于指定范围内的元素，中心点是由给定的位置元素决定

```bash
# 
127.0.0.1:6379> GEORADIUSBYMEMBER china:city beijing 1000 km
1) "beijing"
2) "xian"
127.0.0.1:6379>

```



### HyperLogLog

> 什么是基数

A{1,3,5,6,8,7}

B{1,3,5,7,8}

 基数(不重复的元素)=5

> 简介

Redis Pfadd 命令将所有元素参数添加到 HyperLogLog 数据结构中。

HyperLogLog  基数的统计算法！

优点：占用内存是固定的，

网页 UV（一个人访问一个网站多次，但还是算作一个人！）

```bash
127.0.0.1:6379> clear
127.0.0.1:6379> PFADD mykey a b c d e f g h i j  #创建第一组元素
(integer) 1
127.0.0.1:6379> PFCOUNT mykey   # 统计mykey 元素基数个数
(integer) 10
127.0.0.1:6379> PFADD mykey 2 i j z x c v b n m
(integer) 1
127.0.0.1:6379> PFMERGE mykey3 mykey mykey2  # 合并 并集
OK
127.0.0.1:6379> PFCOUNT mykey3 # 查看并集数量
(integer) 16
127.0.0.1:6379>
```

### Bitmaps

> 位存储

统计用户信息，活跃、不活跃！登录、未登录！打卡，365天打卡、两个状态的都可以使用Bitmaos!

Bitmaps 位图，数据结构！都是二进制来进行记录的，就只有0 1 两个状态。

```bash
127.0.0.1:6379> setbit sign 0 1 # 添加打卡记录
(integer) 0
127.0.0.1:6379> setbit sign 1 1
(integer) 0
127.0.0.1:6379> setbit sign 2 0
(integer) 0
127.0.0.1:6379> setbit sign 3 0
(integer) 0
127.0.0.1:6379> setbit sign 4 1
(integer) 0
127.0.0.1:6379> setbit sign 5 1
(integer) 0
127.0.0.1:6379> setbit sign 6 0
(integer) 0
127.0.0.1:6379>  getbit sign 3 # 查看指定时期是否打卡
(integer) 0
127.0.0.1:6379>  getbit sign 4
(integer) 1
127.0.0.1:6379> BITCOUNT sign  # 统计这周的打卡记录
(integer) 4
127.0.0.1:6379>

```



## 事务

Redis  事务本质：一组命令的集合！一个事务中所有命令都会被系列化，在事务执行过程中，会按照顺序执行！ 一次性，顺序性，排他性,执行一系列命令。

> ------------ 队列 set set  set  执行 --------

<font color=red>Redis 事务没有隔离级别的概念</font>

所有的命令在事务中，并没有直接被执行！只有发起执行命令的时候才会执行 Exec

<font color=red>Redis 单条明亮是保持原子性的，但是事务不保证原子性。</font>

Redis的事务

* 开启事务(mulit)
* 命令入队()
* 执行事务(exec)

> 正常执行事务！

```bash
127.0.0.1:6379> MULTI  #开启事务
OK
# 命令入队
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> EXEC # 执行事务
1) OK
2) OK
3) OK
127.0.0.1:6379>


```

>放弃事务

``` bash
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k4 v4
QUEUED
127.0.0.1:6379> DISCARD  #取消事务
OK
127.0.0.1:6379> get k1  # 事务队列中的命令都不会被执行。
(nil)
127.0.0.1:6379>
```



>编译型异常（代码有问题！命令有错！），事务中所有的命令都不会被执行！

```bash
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> setk3 v3
(error) ERR unknown command `setk3`, with args beginning with: `v3`,
127.0.0.1:6379> EXEC
(error) EXECABORT Transaction discarded because of previous errors.
127.0.0.1:6379> get k1
(nil)
127.0.0.1:6379>

```





> 运行时异常（1/0），如果事务队列中存在与发行，那么实行命令的时候、其他命令是可以正常执行的、错误命令抛出异常！

```bash
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> EXEC
(empty array)
127.0.0.1:6379> set k2 "v1"
OK
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> incr k1  # 命令会执行失败
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> get k3
QUEUED
127.0.0.1:6379> EXEC
1) (integer) 1
2) OK
3) (nil)
127.0.0.1:6379>


```

> 监控！Watch

**悲观锁**：

* 很悲观，认为什么时候都会出现问题，无论做什么都会加锁

**乐观锁**：

* 很乐观、什么时候都会出现问题，所以不会上锁！更新数据时候去判断一下，在此期间是否有人修改过这个数据。
* 获取version
* 更新的时候比较version

> Redis 检测测试

正常执行成功！

```bash
127.0.0.1:6379> set money 100
OK
127.0.0.1:6379> set out 0
OK
127.0.0.1:6379> watch money
OK
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> DECRBY money 20
QUEUED
127.0.0.1:6379> incrby out 20
QUEUED
127.0.0.1:6379> EXEC
1) (integer) 80
2) (integer) 20
127.0.0.1:6379>

```

测试多线程修改值、使用watch 可以当做redis的乐观锁操作！

```bash
127.0.0.1:6379> watch monry  # 监视money
OK
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> DECRBY money 10
QUEUED
127.0.0.1:6379> INCRBY out 10
QUEUED
127.0.0.1:6379> exec # 执行前，另外一个线程修改了monty值，就会导致食物执行失败。

```

如果修改失败，获取最新的值就好

![](F:\gitproject\demo\开发文档资料\images\Redis\18.png) 





## Jedis

我们用java 来操作Redis

> 什么是jedis 是Redis 官方推荐的java 链接工具！使用java 操作Redis 中间件 如果你要使用java 操作redis那么一定要对jedis十分的熟悉。

> 测试

1.导入依赖、

```xml
 <!--导入jedis的包-->
    <dependency>
        <groupId>redis.clients</groupId>
        <artifactId>jedis</artifactId>
        <version>3.3.0</version>
    </dependency>
    <!-- fastjson-->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.73</version>
    </dependency>
```

2.编码测试：

* 链接数据库
* 操作命令
* 断开链接

```java
public static void main(String[] args) {
        //1 new Jedis 对象即可
        Jedis jedis = new Jedis("127.0.0.1",6379);
        System.out.print(jedis.ping());
    }
```



**常用API **





```java
 public static void main(String[] args) {
        Jedis jedis = new Jedis("127.0.0.1",6379);

        jedis.flushDB();
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("hello","word");
        jsonObject.put("name","zzy");
        //开启事务
        Transaction multi = jedis.multi();
        String result = jsonObject.toJSONString();
        try {
            multi.set("user1",result);
            multi.set("user2",result);
            multi.exec(); //执行事务
        }catch (Exception ex){
            multi.discard();//放弃事务
            ex.printStackTrace();
        }finally {
            System.out.print(jedis.get("user1"));
            System.out.print(jedis.get("user2"));
            jedis.close(); //关闭连接
        }

    }
```

### Spring Boot  整合

Springboot 操作数据：spring-data jpa jdbc mongodb redis!

SpringData 也是和SpringBoot齐名的项目！

说明：在Springboot2.x之后，原来使用的jedis 被替换为了lettuce

jedis: 采用的直连，多个线程操作的话，是不安全的，如果想要避免不安全，使用jedis pool 链接池！更像 BIO 模式

lettuce: 采用netty,实例可以在多个线程中进行共享，不存在线程不安全的情况！可以减少线程数据了，更像Nio模式

> 整合测试

 1.导入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

2.配置链接

```xml

```



3.测试



4. redisutil

   ```java
   package com.zy.utils;
   
   import org.omg.CORBA.ObjectHelper;
   import org.springframework.beans.factory.annotation.Autowired;
   
   import org.springframework.data.redis.core.RedisTemplate;
   import org.springframework.stereotype.Component;
   import org.springframework.util.CollectionUtils;
   
   import java.util.List;
   import java.util.Map;
   import java.util.Set;
   import java.util.concurrent.TimeUnit;
   
   /**
    * @author: zzy
    * @Date: $ $
    * @Description:
    */
   @Component
   public final class RedisUtil {
   
       @Autowired
       private RedisTemplate<String,Object> redisTemplate;
   
   
       /**
        * 设置缓存失效时间
        *
        * @param key Redis键
        * @param time 时间(秒)
        */
       public  boolean expire(final String key, final long time) {
           try{
               if(time>0){
                   redisTemplate.expire(key,time, TimeUnit.SECONDS);
               }
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /**
        * 根据key获取过期时间
        *
        * @param key 不能为null
        * @return  时间（秒）返回0代表永久有效
        */
       public  long getexpire(String key) {
   
          return redisTemplate.getExpire(key,TimeUnit.SECONDS);
       }
   
       /**
        * 判断key是否存在
        * @param key 键
        * @return true=存在；false=不存在
        */
       public  boolean hasKey(String key) {
   
           try{
               return redisTemplate.hasKey(key);
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /**
        * 删除缓存
        *
        * @param key 可以传一个i值 或多个值
        */
       public  void del(String... key) {
   
           if(key!=null&& key.length>0){
               if(key.length ==1){
                   redisTemplate.delete(key[0]);
               }else {
                  // redisTemplate.delete(CollectionUtils.arrayToList(key));
               }
           }
       }
       //================String====================
   
       /**
        * 普通缓存获取
        *
        * @param key 键
        * @return value 值
        */
       public Object get(String key){
           return key == null?null:redisTemplate.opsForValue().get(key);
       }
   
       /**
        * 普通缓存放入
        * @param key 键
        * @param value 值
        * @return true 成功 false 失败
        */
       public  boolean set(String key,Object value){
           try{
               redisTemplate.opsForValue().set(key,value);
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
   
       /**
        * 普通缓存放入 并摄制时间
        * @param key 键
        * @param value 值
        * @param time 时间(秒) time 要大于0 如果time 小于0 将设置无限期
        * @return true 成功 false 失败
        */
       public  boolean set(String key,Object value,long time){
           try{
               if(time>0){
                   redisTemplate.opsForValue().set(key,value,time,TimeUnit.SECONDS);
               }else {
                   set(key,value);
               }
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /**
        * 递增
        * @param key 键
        * @param delta 要增加几（大于0）
        * @return
        */
       public  long incr(String key,long delta){
           if(delta <0){
               throw  new RuntimeException("递增因子必须大于0");
           }
           return redisTemplate.opsForValue().increment(key,delta);
       }
       /**
        * 递减
        * @param key 键
        * @param delta 要减少几（小于0）
        * @return
        */
       public  long decr(String key,long delta){
           if(delta <0){
               throw  new RuntimeException("递减因子必须大于0");
           }
           return redisTemplate.opsForValue().increment(key,-delta);
       }
   
       /**
        * HashGet
        * @param key  键不能为null
        * @param item 项不能为null
        * @return
        */
       public Object hget(String key,String item){
           return redisTemplate.opsForHash().get(key,item);
       }
   
       /**
        * huoqu hashkay 对应所有值
        * @param key 键
        * @return 对应的多个键值
        */
       public Map<Object,Object> hmget(String key){
           return redisTemplate.opsForHash().entries(key);
       }
   
   
       /**
        * HashSet
        * @param key 键
        * @param map 对应多个值
        * @return
        */
       public  boolean hmset(String key,Map<String,Object> map){
           try {
               redisTemplate.opsForHash().putAll(key,map);
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return false;
           }
       }
   
   
       /**
        * HashSet 并设置时间
        * @param key 键
        * @param map 对应多个值
        * @param time 时间(秒)
        * @return
        */
       public  boolean hmset(String key,Map<String,Object> map,long time){
           try {
               redisTemplate.opsForHash().putAll(key,map);
               if(time>0){
                   expire(key,time);
               }
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return false;
           }
       }
   
       /**
        * 向一张hash 表中放入数据如果不存在将创建
        * @param key
        * @param item
        * @param value
        * @return
        */
       public  boolean hset(String key, String item,Object value){
           try{
               redisTemplate.opsForHash().put(key,item,value);
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /***
        * 向一张hash表中放入数据 如果不放将创建
        * @param key 键
        * @param item 项
        * @param value 值
        * @param time 时间(秒) 注意:如果已经存在hash表有时间，这里将会替换原有时间
        * @return true 成功 false 失败
        */
       public boolean hset(String key,String item,Object value,long time){
           try{
               redisTemplate.opsForHash().put(key,item,value);
               if(time>0){
                   expire(key,time);
               }
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /**
        * 删除hash 表中的值
        * @param key
        * @param item
        */
       public void hdel(String key ,Object... item){
           redisTemplate.opsForHash().delete(key,item);
       }
   
       /***
        * 判断hash 表是否有该项的值
        * @param key
        * @param item
        * @return
        */
       public  boolean hHasKey(String key,String item){
           return redisTemplate.opsForHash().hasKey(key,item);
       }
   
       /**
        * hash 递增 如果不存在，就会创建一个并把新增后的值返回
        * @param key 键
        * @param item 项
        * @param by 要增加几（大于0）
        * @return
        */
       public  double hincr(String key,String item,double by){
           return  redisTemplate.opsForHash().increment(key,item,by);
       }
   
   
       /**
        * hash 递减
        * @param key 键
        * @param item 项
        * @param by 要减少几（小于0）
        * @return
        */
       public  double hdecr(String key,String item,double by){
           return  redisTemplate.opsForHash().increment(key,item,-by);
       }
   
       /**
        * 根据key 获取set 中的所有值
        * @param key
        * @return
        */
       public Set<Object> sGet(String key){
           try {
               return redisTemplate.opsForSet().members(key);
           }catch (Exception e){
               e.printStackTrace();
               return null;
           }
       }
   
       /**
        * 根据value 从一个set中查询，是否存在
        * @param key 键
        * @param value 值
        * @return true 存在 false 不存在
        */
       public boolean sHasKey(String key,Object value){
           try{
               return redisTemplate.opsForSet().isMember(key,value);
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
   
       }
   
       /**
        * 将数据放入Set 缓存
        * @param key 键
        * @param values 值  可以是多个
        * @return 成功个数
        */
       public long sSet(String key,Object... values){
           try {
               return  redisTemplate.opsForSet().add(key,values);
           }catch (Exception e){
               e.printStackTrace();
               return 0;
           }
       }
   
       /***
        * 将set数据放入缓存
        * @param key 键
        * @param time 时间(秒)
        * @param values 值(可以树多个)
        * @return 成功个数
        */
       public  long sSetAndTime(String key,long time,Object... values){
           try {
               Long count = redisTemplate.opsForSet().add(key, values);
               if(time>0){
                   expire(key,time);
               }
               return  count;
           }catch (Exception e){
               e.printStackTrace();
               return 0;
           }
       }
   
       /***
        * 获取set 缓存的长度
        * @param key 键
        * @return
        */
       public  long sGetSetSize(String key){
           try {
               return redisTemplate.opsForSet().size(key);
           }catch (Exception e){
               e.printStackTrace();
               return  0;
           }
   
       }
   
       /***
        * 移除值为value
        * @param key  键
        * @param valuse 值 可以是多个
        * @return
        */
       public  long setRemove(String key, Object... valuse){
           try {
               Long count = redisTemplate.opsForSet().remove(key, valuse);
               return  count;
           }catch (Exception e){
               e.printStackTrace();
               return 0;
           }
       }
   
       //===============================list====================================
   
       /***
        * 获取list 缓存的长度
        * @param key  键
        * @return
        */
       public  long lGetListSize(String key){
           try {
               return redisTemplate.opsForList().size(key);
           }catch (Exception e){
               e.printStackTrace();
               return  0;
           }
       }
   
       /***
        * 通过索引 获取list 中的值
        * @param key 键
        * @param index 索引 index >=0时，0 表头 1 第二个元素，依次类推，index<0时 ，-1 表尾 -2 倒数第二个元素,依次类推
        * @return
        */
       public  Object lGetIndex(String key,long index){
           try {
               return redisTemplate.opsForList().index(key,index);
           }catch (Exception e){
               e.printStackTrace();
               return null;
           }
   
       }
   
       /***
        * 将list 放入缓存
        * @param key  键
        * @param value 值
        * @return
        */
       public  boolean lSet (String key,Object value){
           try {
               redisTemplate.opsForList().rightPush(key,value);
               return  true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
       }
   
       /***
        * 将list 放入库存
        * @param key 键
        * @param value 值
        * @param time 时间(秒)
        * @return
        */
       public  boolean lSet(String key,Object value,long time){
           try {
               redisTemplate.opsForList().rightPush(key,value);
               if (time>0){
                   expire(key,time);
               }
               return  true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
   
       }
   
       /***
        * 将list 放入缓存
        * @param key 键
        * @param value 值
        * @return
        */
       public boolean lSet(String key, List<Object> value){
           try {
               redisTemplate.opsForList().rightPush(key,value);
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return  false;
           }
   
       }
   
       /***
        * 将list 放入缓存
        * @param key  键
        * @param value 值
        * @param time 时间(秒)
        * @return
        */
       public  boolean lSet(String key,List<Object> value,long time){
   
           try {
               redisTemplate.opsForList().rightPushAll(key,value);
               if(time>0){
                   expire(key,time);
               }
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return false;
           }
   
       }
   
       /***
        * 根据索引修改list 中的某条数据
        * @param key 键
        * @param index 索引
        * @param value 值
        * @return
        */
       public boolean lUpdateIndex(String key,long index, Object value){
           try {
               redisTemplate.opsForList().set(key,index,value);
               return true;
           }catch (Exception e){
               e.printStackTrace();
               return false;
           }
       }
   
       /**
        * 移除N个值为value
        * @param key 键
        * @param count 移除多个
        * @param value 值
        * @return 移除的个数
        */
       public  long lRemove(String key,long count, Object value){
           try {
               Long remove = redisTemplate.opsForList().remove(key, count, value);
               return remove;
           }catch (Exception e){
               e.printStackTrace();
               return 0;
           }
       }
   
   
   }
   
   ```

   

### Redis.conf详解

启动时候，就通过配置文件来启动

> 单位



![](F:\gitproject\demo\开发文档资料\images\Redis\19.png)

1.配置文件unit单位对大小写不敏感

> 包含

![](F:\gitproject\demo\开发文档资料\images\Redis\20.png)

相当于 spring, import ,include

> 网络



```bash
bind 127.0.0.1  # 绑定的ip

protected-mode yes # 保护模式
port 6379 #端口设置
```

> 通用 GENERAL

```bash
daemonize yes # 以守护进程的方式运行，默认是no ,我们需要自己开启yes
pidfile /var/run/redis_6379.pid # 如果以后台的方式运行，我们需要指定一个pid文件！


# 日志
# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably) #生产环境
# warning (only very important / critical messages are logged)
loglevel notice

logfile "" # 日志文件位置名
databases 16 # 16个数据库

always-show-logo yes  # 是否总是显示log

```



>快照 SNAPSHOTTING

持久化，在规定时间内，执行力多次操作，则会持久化到文件，rdb.aof

redis 是内存数据库吗，如果没有持久化，那么数据断电及失。

```bash
# 如果 900s 内，如果至少有一个key进行了修改，我们进行持久化操作。
save 900 1
# 如果300s内 ，如果至少10key进行了修改，我们进行持久化操作。
save 300 10
# 如果60s内 ，如果至少10000key进行了修改，我们进行持久化操作。
save 60 10000
#以后学习持久化，会自定义这个测试

stop-writes-on-bgsave-error yes # 持久化如果出错，是否还需要继续工作。

rdbcompression yes # 是否压缩rdb 文件，需要消耗一些cpu资源。

rdbchecksum yes  # 保存rdb 文件时候，进行错误检查校验。

dir ./  # rdb 文件保存路径。


```

> REPLICATION  复制





> SECURITY 安全

可以在这里设置redis 的密码，默认没有密码

```bash
127.0.0.1:6379> CONFIG  get requirepass
1) "requirepass"
2) ""
127.0.0.1:6379> CONFIG set requirepass "123456"
OK
127.0.0.1:6379> CONFIG  get requirepass
1) "requirepass"
2) "123456"
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> auth 123456
OK
127.0.0.1:6379> CONFIG  get requirepass
1) "requirepass"
2) "123456"
127.0.0.1:6379>
```

![](F:\gitproject\demo\开发文档资料\images\Redis\21.png)

> CLIENTS  限制



```bash
maxclients 10000 # 设置连接上redis 最大客户端数量 

maxmemory <bytes> # redis 配置最大内存容量

maxmemory-policy noeviction # 内存到达上限之后的处理策略
1.volatile-lru：设定超时时间的数据中,删除最不常使用的数据.

2.allkeys-lru：查询所有的key中最近最不常使用的数据进行删除，这是应用最广泛的策略.

3.volatile-random：在已经设定了超时的数据中随机删除.

4.allkeys-random：查询所有的key,之后随机删除.

5.volatile-ttl：查询全部设定超时时间的数据,之后排序,将马上将要过期的数据进行删除操作.

6.Noeviction：如果设置为该属性,则不会进行删除操作,如果内存溢出则报错返回.

```

> APPEND ONLY 模式 aof配置

```bash
appendonly no # 默认是不开启aof 模式的，默认是侍弄rdb 方式持久化的，在大部分情况下，rdb完全够用了！

appendfilename "appendonly.aof" # 持久化的文件名字

# appendfsync always # 每次修改都会 sync ,消耗性能
appendfsync everysec # 没秒执行一次 sync ,可能会丢失者ls 的数据
# appendfsync no   # 不执行 sync, 这个时候操作系统自己同步数据，速度最快。



```





## Redis持久化

面试和工作，持久化都是重点！

Redis 是内存数据库，如果不将内存中的数据库状态保存到磁盘那么一旦服务器进程退出，服务器中的数据库状态也会消失。所以redis 提供了持久化功能。

**RDB(Redis DataBase)**

> 什么是RDB

![](F:\gitproject\demo\开发文档资料\images\Redis\22.png)



在指定时间间隔内将内存中的数据集快照写入磁盘么也就是行话讲的Snapshot 快照，它恢复时是将快照直接读到内存里。

Redis会单独创建（fork） 一个子进程来进行持久化，会将数据写到临时文件中，待持久化过程都结束了，在用这个临时文件替换上次持久化好的文件，整个过程中，主进程是不进行任何IO操作的。这就确保了极高的性能。如果需要进行大规模数据恢复,且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。RDB的缺点是最后一次持久化后的数据可能丢失，我们默认的就是RDB一般情况下不需要修改这个配置！

<font color="red"> rdb保存的文件是dump.rdb</font>> 都是在我们的配置文件中快照中进行配置！

 ![](F:\gitproject\demo\开发文档资料\images\Redis\24.png)



> 触发机制

1.save 的规则妈祖的情况下，会自动触发rdb规则

2.执行flushall命令、也会触发我们的rdb规则！

3.退出redis 、也会产生rdb文件！

备份就会自动生成一个dump.rdb

> 如何恢复rdb 文件！

1.只需要将rdb文件当在我们redis启动目录就可以，redis启动时候就会自动检测dump.rdb恢复其中的数据！

2.查看需要存在的位置

```bash
127.0.0.1:6379> config get dir
1) "dir"
2) "/usr/local/bin"  #如果这个目录先存在dump.rdb文件，启动时候就会自动恢复其中的数据。
127.0.0.1:6379>

```



## 3.配置Redis 持久化

```javascript
1.查看挂载路径 【root】# pwd
2.修改配置文件 【root】# vi redi.conf 
3.如下图【root】# appendonly yew
```

![图片](F:\gitproject\demo\开发文档资料\images\redis-02.png)

### AOF(Append Only File)

将我们所有命令都记录下来，history,恢复的时候就把这个文件全部都在执行一遍。

> 是什么

![](F:\gitproject\demo\开发文档资料\images\Redis\23.png)

以日志的形式来记录每一个操作，将Redis 执行过的所有记录指令记录下来（读操作不记录），只许追加文件但不可以改写文件，reids启动之初就会读取该文件重新构建数据，换言之，redis 重启的话就根据日志文件的内容将写指令从前后执行一次以完成数据的恢复工作。

Aof保存的是 appendonly.aof 文件

> append



![](F:\gitproject\demo\开发文档资料\images\Redis\25.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\26.png)



## Redis 发布订阅

![](F:\gitproject\demo\开发文档资料\images\Redis\27.png)



![](F:\gitproject\demo\开发文档资料\images\Redis\28.png)



> 测试

![](F:\gitproject\demo\开发文档资料\images\Redis\29.png)



![](F:\gitproject\demo\开发文档资料\images\Redis\30.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\31.png)



![](F:\gitproject\demo\开发文档资料\images\Redis\32.png)







## Redis主从复制

 ![](F:\gitproject\demo\开发文档资料\images\Redis\33.png)



![](F:\gitproject\demo\开发文档资料\images\Redis\34.png)





主从复制，读写分离！80%的情况下都是在读数据操作！减缓服务器的压力！框架中经常使用！一主二从！

只要在公司中，主从复制就是必须要使用的，因为真实的项目中不可能单机使用redis!

### 环境配置

```bash
127.0.0.1:6379> info replication  # 查看当前库的信息
# Replication
role:master   #角色
connected_slaves:0  #没有从机
master_replid:2e74ef2b015db3e66e2c6806076835ace0cc4e58
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
127.0.0.1:6379>

# 复制配置文件
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]# ls
redis.conf
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]# cp redis.conf  redis79.conf
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]# cp redis.conf  redis80.conf
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]# cp redis.conf  redis81.conf
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]# ls
redis79.conf  redis80.conf  redis81.conf  redis.conf
[root@iZ2zedq4zbdzwebsgsxi9bZ zyconfig]#



# 
root@iZ2zedq4zbdzwebsgsxi9bZ bin]# ps -ef|grep redis
root      3789     1  0 18:12 ?        00:00:00 redis-server 127.0.0.1:6380
root      3795     1  0 18:13 ?        00:00:00 redis-server 127.0.0.1:6381
root      3804  3726  0 18:14 pts/3    00:00:00 grep --color=auto redis
root     29292     1  0 Jan21 ?        00:06:22 redis-server 127.0.0.1:6379
[root@iZ2zedq4zbdzwebsgsxi9bZ bin]#


```

 ![](F:\gitproject\demo\开发文档资料\images\Redis\35.png)



一主二从

```bash
默认情况下，每台Redis服务器都是主节点；我们一般情况下只能配置从机就好了

认老大！一主（79）二从（80,81）


```



![](F:\gitproject\demo\开发文档资料\images\Redis\36.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\37.png)

 

![](F:\gitproject\demo\开发文档资料\images\Redis\38.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\39.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\40.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\41.png)



### 哨兵模式

（自动选举老大的模式）

>概述

主从切换技术的方法是:当服务器宕机后，需要手动吧一台从服务器切换为主服务器，这就需要人工干预，费事费力、还会造成一段时间内服务器不可用，这不是一种推荐的方式，更多时候、我们优先考虑哨兵模式，redis从2.8开始正式提供了Sentinel(哨兵)架构来解决这个问题。

谋朝篡位的自动版、能后台监控主机是否故障、如果故障了根据投票数<font color="red">自动将从库转移为主库</font> 、 

哨兵模式是一种特殊的模式、首先redis提供了哨兵的命令，哨兵是一个独立的进程，作为进程他会独立运行、其原理是哨兵听过发送命令、等待redis服务器响应、从而监控运行的多个redis实例。

![](F:\gitproject\demo\开发文档资料\images\Redis\42.png)



这里哨兵有两个作用

* 通过发送命令、让redis 服务器返回监控器运行状态，包括住服务器和从服务器
* 当哨兵监控到master宕机、会自动将slave切换成master、然后通过发布订阅模式通知其他从服务器、修改配置文件、让他们切换主机。

然而一个哨兵进程对redis服务器进行监控、可能会出现问题、为此、我们可以使用多个哨兵进行监控、各个哨兵之间进行监控、这样就形成了哨兵模式。

![](F:\gitproject\demo\开发文档资料\images\Redis\43.png)



假设主服务器宕机、哨兵1先检测到这个结果、系统并不会马上进行failover过程、仅仅是哨兵1主观认为主服务器不可用、这个显现为主观下线。当后面的哨兵也检测到住服务器不可用、并且数量达到一定值时、那么哨兵之间就会进行一次选票，投票的结果由一个哨兵发起，进行failover(故障转移）操作、切换成功后、就会通过发布订阅模式、让各个哨兵吧自己监控的从服务器实现切换主机、这个过程称为客观下线。



> 测试



我们目前的状态是一主二从

1.配置哨兵配置文件sentinel.conf

```bash
# sentinel monitor 被监控的名称host port 1
sentinel monitor myredis 127.0.0.1 6379 1
```

后面的这个数据字1，代表主机挂了、slave投票看让谁接替成为主机、票数最多的就会成为主机。



![](F:\gitproject\demo\开发文档资料\images\Redis\44.png)



如果Master 节点断开了，这个时候就会从从机中随机选择一个服务器（这里面有一个算法）



如果主句此时回来了，只能归并新的主机下，当做从机，这就是哨兵模式的规则。

> 哨兵模式

优点

* 哨兵集群、基于主从复制模式，所有的主从配置优点，他全有。
* 主从可以切换，故障可以转移，系统的可用性就会更好。
* 哨兵模式就是主从模式的升级手动到自动、更加健壮。

缺点

* Redis 不好在线扩容的，集群容量一旦达到上限，在线扩容就十分麻烦，
* 实现哨兵模式的配置其实很麻烦的，里面有很多选择。

>哨兵模式的全部配置



```bash
# Example   sentinel.conf
# 哨兵sentinel实例运行的端口   默认是26379，如果有哨兵集群，我们还需要配置每个哨兵端口
port 26379

#哨兵sentinel的工作目录
dir /tmp


#哨兵 sentine1 监控的redis主节点的 ip port   
# master-name  ，可以自己命名的主节点名字 只能由字母A-Z、数字0-9、这三个字符"  .   -  _ "组成。
# quorum配置多少个sentine1哨兵统- -认为master主节点失联那么这时客观上认为主节点失联了
# sentine1 monitor <master-name> <ip> <redis-port> <quorum>
sentinel monitor mymaster   127.0.0.1   6379   2


#当在Redis实例中开启了requirepass foobared 授权密码这样所有连接kedis实例的客户端都要提供密码
#设置哨兵sentinel连接主从的密码注意必须为主从设置- - 样的验证密码
# sentine1 auth-pass <master-name> <password>
sentine1 auth-pass mymaster MySUPER--secret-0123passwOrd

#指定多少毫秒之后主节点没有应答哨兵sentine1 此时哨兵主观上认为主节点下线默认30秒
# sentinel down-after-mi 11i seconds <master-name> <mi 11iseconds>
sentine1 down-after-mi 11iseconds mymaster 30000

#这个配置项指定了在发生failover主备切换时最多可以有多少个slave同时对新的master进行同步，这个数字越小，完成fai lover所需的时间就越长，但是如果这个数字越大，就意味着越多的slave因为replication而 不可用。可以通过将这个值设为1来保证每次只有一个slave处于不能处理命令请求的状态。
# sentine1 paralle1-syncs <master-name> <numslaves>
sentine1 paralle1-syncs mymaster 1

#故障转移的超时时间failover-timeout 可以用在以下这些方面:
#1.同一个sentine1对同一 个master两次fai lover之间的间隔时间。
#2.当一个slave从一 个错误的master那里同步数据开始计算时间。直到s1ave被纠正为向正确的master那里同步数据时。
#3.当想要取消一个正在进行的failover所需要的时间。
#4.当进行failover时，配置所有s1aves指向新的master所需的最大时间。不过，即使过了这个超时，slaves 依然会被正确配置为指向master,但是就不按parallel-syncs所配置的规则来了
#默认三分钟
# sentine1 failover-timeout <master-name> <milliseconds>
sentine1 fai lover-ti meout mymaster 180000

# SCRIPTS EXECUTION
#配置当某一事件发生时所需要执行的脚本，可以通过脚本来通知管理员，例如当系统运行不正常时发邮件通知相关人员。
#对于脚本的运行结果有以下规则:
#若脚本执行后返回1，那么该脚本稍后将会被再次执行，重复次数目前默认为10
#若脚本执行后返回2，或者比2更高的一个返回值，脚本将不会重复执行。
#如果脚本在执行过程中由于收到系统中断信号被终止了，则同返回值为1时的行为相同。
#一个脚本的最大执行时间为60s，如果超过这个时间，脚本将会被-一个SIGKILL信号终止，之后重新执行。

#通知型脚本:当sentine1有任何警告级别的事件发生时(比如说redis实例的主观失效和客观失效等等)，将会去调用这个脚本，这时这个脚本应该通过邮件，SMS等 方式去通知系统管理员关于系统不正常运行的信息。调用该脚本时，将传给脚本两个参数，一 个是事件的类型，一个是事件的描述。如果sentine1. conf配置文件中配置了这个脚本路径，那么必须保证这个脚本存在于这个路径，并且是可执行的，否则sentine1无法正常启动成功。
#通知脚本
# she11编程
# sentine1 notification-script <master-name> <script-path>
sentine1 notificati on-script mymaster /var/redis/notify. sh

#客户端重新配置主节点参数脚本
#当一个master由于failover而发生改变时，这个脚本将会被调用，通知相关的客户端关于master地址已经发生改变的信息。
#以下参数将会在调用脚本时传给脚本: 
# <master-name> <role> <state> <from-ip> <from-port> <to-ip> <to-port>
#目前<state>总是“failover",
# <role>是“Teader"或者"observer"中的-一个。
#参数from-ip， from-port， to-ip，to-port是用来和旧的master和新的master(即旧的s lave)通信的
#这个脚本应该是通用的，能被多次调用，不是针对性的。
# sentine1 client-reconfig-script <master-name> <script-path>
sentine1 client-reconfig-script mymaster /var/redis/reconfig.sh #一般都是由运维来配置!
```

## Redis 缓存穿透和雪崩



​    Redis缓存的使用，极大的提升了应用程序的性能和效率，特别是数据查询方面。但同时，它也带来了一些问题。其中最重要的问题就是数据的一致性问题，从严格意义上讲，这个问题无解。如果对数据的一直行要求很高，那么就不能使用缓存。



### 缓存穿透

> 概念

缓存穿透的概念很简单，用户想要查询一个数据，发现redis内存数据库没有，也就是缓存没有命中，于是向持久层数据库查询。发现也没有，于是本次查询失败，当用户很多的时候吗，缓存都没有命中，于是都去请求持久层数据库。这会给持久层数据库造成很大的压力，这时候就相当于出现了缓存穿透。

> 解决方案



布隆过滤器

布隆过滤器是一种数据结构，对有可能查询的参数一hash形式存储，在控制层先进行校验，不符合则丢弃，从而避免了对底层存储系统的查询压力。

![](F:\gitproject\demo\开发文档资料\images\Redis\45.png)



缓存空对象

当存储不命中后，即使返回的空对象也将其缓存起来，同时会设置一个过期时间，之后再访问这个数据将会从缓存中获取，保护了后端数据源：



![](F:\gitproject\demo\开发文档资料\images\Redis\46.png)

但是这种方法会存在两个问题：

1.如果空值能够被缓存起来，这就意味着缓存需要更过的空间存储更多的键，因为这当中可能会很多的空值键；

2.即使对空值设置了过期时间，还是会存在缓存层和存储层的数据会有一段时间窗口不一致，这对于西药保持一致性的业务会有影响。



### 缓存击穿(查询量大)

> 概述

这里需要注意和缓存击穿的区别，缓存击穿，是指一个key非常热点、在不停的扛着大并发、大并发集中对一个点进行访问，当这个key在失效瞬间、持续的大并发就击穿缓存，直接请求数据库，就像屏幕上凿开一个小洞。

当某个key在过期瞬间、又大量请求并发访问，这类数据一般是热点数据，由于缓存过期，会同时访问数据库来查询最新数据、并且会写缓存，会导致数据库瞬间压力过大。

> 解决方案

设置热点数据永远不过期

从缓存层面看，没有设置过期时间，所以不会出现热点key过期后产生的问题。

**加互斥锁**

![](F:\gitproject\demo\开发文档资料\images\Redis\47.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\48.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\49.png)

![](F:\gitproject\demo\开发文档资料\images\Redis\50.png)