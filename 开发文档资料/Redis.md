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

