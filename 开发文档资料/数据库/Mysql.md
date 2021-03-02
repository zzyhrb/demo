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

