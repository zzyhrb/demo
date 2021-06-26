#   Docker  安装



## 安装Docker



> 环境准备

1.需要linux 基础

2.CentOS7

3.使用远程工具连接

>环境查看

``` bash
#系统内核
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# uname -r
3.10.0-1127.18.2.el7.x86_64
#系统版本
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#



```

> 查看Docker文档安装

网址：https://docs.docker.com/engine/install/centos/

1.卸载旧版本

``` bash
 #1.卸载旧版本
 sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
#2.使用存储库进行安装
 sudo yum install -y yum-utils
 
#3.设置镜像仓库
  sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo #默认是国外的
 
  sudo yum-config-manager \
    --add-repo \
 http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo #阿里云镜像地址
 #更新软件吧索引
 yum makecache fast
 
 #4. 安装 Docker 引擎 docker-ce 社区  ee 企业版
  sudo yum install docker-ce docker-ce-cli containerd.io
 #5 启动docker
  systemctl start docker
  #6.查看是否安装成功
  
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker version  # 查看是否安装成功
Client: Docker Engine - Community
 Version:           20.10.6
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        370c289
 Built:             Fri Apr  9 22:45:33 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.6
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       8728dd2
  Built:            Fri Apr  9 22:43:57 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.4
  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
 runc:
  Version:          1.0.0-rc93
  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
# 7.  hello-world
docker run hello-world
```

![](F:\gitproject\demo\开发文档资料\images\Docker\01.png)

``` bash
#8.查看下载的hello-word 镜像
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    d1165f221234   2 months ago    13.3kB
mysql         5.7.30    a4fdfd462add   11 months ago   448MB
redis         latest    987b78fc9e38   11 months ago   104MB
tomcat        latest    1b6b1fe7261e   12 months ago   647MB
nginx         latest    9beeba249f3e   12 months ago   127MB
java          8         d23bdf5b1b1b   4 years ago     643MB

```

> 卸载docker

``` bash
#1.卸载依赖
 yum remove docker-ce docker-ce-cli containerd.io
 
#2.删除资源
rm -rf /var/lib/docker  #docker默认工作路径
```

## 阿里云镜像加速

1.登录阿里云

![](F:\gitproject\demo\开发文档资料\images\Docker\02.png)





2.配置使用

``` bash
# 1.创建目录
sudo mkdir -p /etc/docker
# 2.
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://8jcvkn4r.mirror.aliyuncs.com"]
}
EOF
# 3
sudo systemctl daemon-reload
# 4
sudo systemctl restart docker
```





## 底层原理

Docker 是怎么工作的

Docker 是一个Client-Server 结构的系统，Docker的守护进程运行在主机上，通过Socket从客户端访问！

DockerServer 接受到的Docker-Client的命令，就会执行这个命令



## Docker 常用命令

> 帮助命令

``` bash
docker version		#显示docker 的版本信息
docker info 		# 显示docker的系统信息，包括镜像和容器的数量
docker -- help  	#帮助命令
》systemctl start docker
2.重启Docker 
》systemctl restart docker
3.停止Docker
》systemctl stop docker
# 查看docker状态：
systemctl status docker
```



##  镜像命令



docker images 

``` bash
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker images -a
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    d1165f221234   2 months ago    13.3kB

# 注释
REPOSITORY  镜像仓库源
TAG			镜像标签
IMAGE ID	镜像ID
CREATED		镜像创建时间
SIZE		镜像大小
# 可选项
-a , --all	 #列出所有镜像
-q,  --quite #只显示镜像的id
```

docker search 搜索镜像

``` bash
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker search mysql
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   10876     [OK]
mariadb                           MariaDB Server is a high performing open sou…   4102      [OK]
mysql/mysql-server                Optimized MySQL Server Docker images. Create…   808                  [OK]

#可选项 通过搜索来过滤

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker search --help
Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   10876     [OK]
mariadb   MariaDB Server is a high performing open sou…   4102      [OK]
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#
```

> 下载镜像  （socker pull）

``` bash
 docker pull mysql
 # 如果不写tag 默认是latest    (分层下载，docker iamges 的核心 联合文件系统)
# 指定版本下载
docker pull mysql:5.7


```

>  删除镜像 （docker rml）

``` bash
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker rmi -f 镜像id
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker rmi -f 镜像id 镜像id  镜像id
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker rmi -f $(docker images -aq)  #删除全部镜像
```



## 容器命令

说明 ：先有镜像才可以创建容器，linux ,下载一个centos 镜像来测试学习

```bash
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker pull centos   
```



新建容器并启动

``` bash
docker run [可选参数] image

#参数说明
-- name="Name"   容器名字 tomcat01  tomcat02 ，用来区分容器
-d				 后台方式运行
-it				 使用交互方式运行，进入容器查看内容
-P 				 指定容器端口 -P 8080:8080
	-p  ip:主机端口：容器端口
	-p 主机端口：容器端口(常用)
	-p 容器端口
	
-p 		随机指定端口  （小写p）

#测试，启动并进入容器
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -it centos /bin/bash
[root@4aefcf5c7da5 /]# ls	# 查看容器内的centos
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@4aefcf5c7da5 /]#

#退出容器命令到主机 exit

#docker ps 命令
	#列出当前正在运行的容器
-a	#列出当前正在运行的容器+带出历史运行过的容器
-n=?#显示最近创建过的容器（-n=1）
-q	#只显示容器的编号
 
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps  查看运行的容器
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps -a  # 查看曾经运行的容器
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                            PORTS     NAMES
4aefcf5c7da5   centos         "/bin/bash"              2 minutes ago   Exited (127) About a minute ago             sleepy_hugle
58866b0081d1   hello-world    "/hello"                 2 days ago      Exited (0) 2 days ago                       xenodochial_elgamal
5fcf4c9916de   987b78fc9e38   "docker-entrypoint.s…"   6 months ago    Exited (0) 3 months ago                     redis
01b7586b01cd   mysql:5.7.30   "docker-entrypoint.s…"   8 months ago    Exited (0) 2 days ago                       mysql
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#


```



> 退出容器

``` bash
exit  #  直接退出容器并停止运行
Ctrl +P + Q  #容器不停止退出
```

删除容器

``` bash
docker rm 容器id				# 删除指定id 容器
docker rm -f $(docker ps -aq)  # 删除全部容器


```

启动停止容器

``` shell
docker start 容器id		#启动容器
docker restart 容器id		#重启容器
docker stop 	容器id	#停止容器
docker kill		容器id 	# 强制停止当前的容器


```

## 其他常用命令



后台容器命令

``` shell
#命令 docker run -d 镜像名
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -d centos

#问题docker ps 发现centos 停止了
#常见的坑 docker 容器食用后台运行，就必须要一个前台进程，docker发现没有应用，就会自动停止


```

查看日志

``` sh
docker logs -f -t --tail 容器，没有日志
#自己编写一段shell脚本
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -d centos /bin/sh -c "while true;do echo zzy;sleep 1;done"


[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS     NAMES
11efc06c764e   centos    "/bin/sh -c 'while t…"   37 seconds ago       Up 36 seconds                 reverent_wozniak
b481316f12ba   centos    "/bin/sh -c 'while t…"   About a minute ago   Up About a minute             goofy_goodall
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker logs -tf --tail 10 11efc06c764e

#显示日志
-tf		#显示日志
--tail  #要显示日志条数
```



查看容器进程信息



``` shell
# 命令 docker top 容器id
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker top 11efc06c764e
UID                 PID                 PPID                C                   STIME     
root                8490                8470                0                   21:15     
root                9260                8490                0                   21:21      
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#

```

查看镜像元数据

``` shell
# docker inspect 容器id 
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker inspect 11efc06c764e

```

进入 当前正在运行的容器

``` shell
#方式一 
#命令
docker exec -it 11efc06c764e /bin/bash
#测试
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
11efc06c764e   centos    "/bin/sh -c 'while t…"   17 minutes ago   Up 17 minutes             reverent_wozniak
b481316f12ba   centos    "/bin/sh -c 'while t…"   18 minutes ago   Up 18 minutes             goofy_goodall
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker exec -it 11efc06c764e /bin/bash
[root@11efc06c764e /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@11efc06c764e /]#

# 方式二
docker  attach 容器id 
# 测试

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker attach 11efc06c764e
正在执行当前运行的代码。。。

# docker exec  #进入容器后开启一个新的终端，可以在里面操作(常用)
# docker attach # 进入容器正在执行的终端，不会启动新的进程
```



从容器内拷贝文件到主机上

 ``` shell
#docker cp 容器id:容器内路径   目的的主机路径

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -it centos /bin/bash
[root@c07f0870739a /]# [root@iZ2zedq4zbdzwebsgsxi9bZ ~]#
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
c07f0870739a   centos    "/bin/bash"   19 seconds ago   Up 18 seconds             stupefied_wilson
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker attach c07f0870739a
[root@c07f0870739a /]# cd /home/
[root@c07f0870739a home]# ls
#新建文件
[root@c07f0870739a home]# touch test.java
[root@c07f0870739a home]# ls
test.java
[root@c07f0870739a home]# exit
exit
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker cp c07f0870739a:/home/test.java  /home
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# ls
Dockerfile
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# cd ../
[root@iZ2zedq4zbdzwebsgsxi9bZ /]# ls
bin  boot  dev  etc  home  lib  lib64  lost+found  media  mnt  my  mydata  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@iZ2zedq4zbdzwebsgsxi9bZ /]# cd home/
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# ls
project  test.java
[root@iZ2zedq4zbdzwebsgsxi9bZ home]#

 ```







安装部署nginx

``` shell
# 1.搜索镜像 search  建议大家去docker 搜索，可以看到帮助文档
# 2.下载镜像 pull
# 3.运行测试


[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    d1165f221234   2 months ago    13.3kB
centos        latest    300e315adb2f   5 months ago    209MB
mysql         5.7.30    a4fdfd462add   12 months ago   448MB
tomcat        latest    1b6b1fe7261e   12 months ago   647MB
nginx         latest    9beeba249f3e   12 months ago   127MB
java          8         d23bdf5b1b1b   4 years ago     643MB

# -d 后台运行
# --name 给容器命名
# -宿主机端口，容器内部端口

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -d --name nginx01 -p 3389:80 nginx
2636b2ce94f30c6ad2df71b5d50caa4e0c844522d31ec6e8e7f9bfc91efe138b
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                   NAMES
2636b2ce94f3   nginx     "nginx -g 'daemon of…"   6 seconds ago   Up 5 seconds   0.0.0.0:3389->80/tcp, :::3389->80/tcp   nginx01
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# curl localhost:3389


```

> 部署es +kibana



``` shell
# es 暴露的端口很多
# es 十分耗内存
# es 的数据一般需要放置在安全目录！挂载
#  --net  somentwork ? 网络配置
# docker stats 查看cpu 状态
#启动 elasticsearch
docker run -d --name elasticsearch  -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2


# 测试 一下 es 是否成功

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# curl localhost:9200
{
  "name" : "Obn1ABq",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "YLFVoP4oREu2uJeDgZffVA",
  "version" : {
    "number" : "6.8.15",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "c9a8c60",
    "build_date" : "2021-03-18T06:33:32.588487Z",
    "build_snapshot" : false,
    "lucene_version" : "7.7.3",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#


# 增加内存的限制 修改配置文件  -e环境配置修改

docker run -d --name elasticsearch  -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m"  elasticsearch:7.6.2

```

##  可视化

* portainer(先用这个)



``` shell
docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

* Rancher(Cl/CD 再用)



commit  镜像

``` shell 
docker commit 提交容器成为一个新的副本

# 命令和git原理类似

docker commit -m="提交信息" -a="作者" 容器id 目标镜像名:[tag]

```



实战

``` shell
# 1.启动一个默认的tomcat
# 2.发现这个默认的tomcat 没有webapps应用 ，镜像的原因，官方的默认镜像 webapps 下面没有文件
# 3.自己拷贝了基础文件
# 4.将我们操作过的容器通过commit 提交为一个镜像! 我们以后就使用修改过的镜像即可，这就是我们自己的一个修改的镜像

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker commit -a="zzy" -m="add webapps" d1d14dbb73fb tomcat04:1.0
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED         SIZE
tomcat04              1.0       7c2ef7ea5ba3   6 seconds ago   652MB
portainer/portainer   latest    580c0e4e98b0   8 weeks ago     79.1MB
elasticsearch         6.8.15    b71dbc55f668   2 months ago    931MB
hello-world           latest    d1165f221234   2 months ago    13.3kB
centos                latest    300e315adb2f   5 months ago    209MB
mysql                 5.7.30    a4fdfd462add   12 months ago   448MB
tomcat                latest    1b6b1fe7261e   12 months ago   647MB
nginx                 latest    9beeba249f3e   12 months ago   127MB
elasticsearch         7.6.2     f29a1ee41030   13 months ago   791MB
java                  8         d23bdf5b1b1b   4 years ago     643MB

```



##  容器数据券



总结：容器的持久化和同步操作!容器间也是可以数据共享的!



使用数据券

> 方式一  :直接使用命令挂载 -v

``` shell
docker run -it -v 主机目录：容器目录
# 测试
[root@iZ2zedq4zbdzwebsgsxi9bZ /]# docker run -it -v /home/ceshi:/home centos /bin/bash

#启动起来时候我妈可以通过deocker inspect 容器id
 "Mounts": [			#挂载-v 券
            {
                "Type": "bind",
                "Source": "/home/ceshi",  # 主机内地址
                "Destination": "/home",   # docker 容器内地址
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],

```

再测试

``` shell
# 1. 停止容器
# 2. 在本地服务器上修改挂载文件添加记录 vim te.java
# 3. 启动容器  docker start 容器id 
# 4. 进入容器 docker attach 文件内容已经同步 cat te.java

```



## 实战 ：安装MySQL

mysql 数据持久化问题

``` shell
# 获取镜像
docker pull mysql:5.7

# 运行容器，需要做数据挂载! # 安装启动mysql, 需要配置密码。
# 官方测试 ；$ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# 启动
-d  后台运行
-p 端口映射
-v 券挂载
-e 环境配置
-- name 容器名字

[root@iZ2zedq4zbdzwebsgsxi9bZ /]# docker run -d -p 3306:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root --name mysql01 mysql:5.7

```

假设我们将容器删除

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ mysql]# docker rm -f mysql01

```

发现，我们挂载到本地的数据券依旧没有丢失，这就实现了容器数据持久化功能。

## 具名和匿名挂载

``` shell 
# 匿名挂载
-v 容器内路径
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -d -P --name nginx01 -v /ect/nginx nginx

# 查看所有 volume 的情况
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker volume ls
DRIVER    VOLUME NAME
local     73e11ce9c37e3d88fdb09160dc0593f0812f3bae9e3572aba305fccb747db558
local     3239a18a7f0dfea24cfa15391bf96f535d66b31accec1f692b884605cac7a048
local     de0a652f0e2ff873a2b3cdd2fdbfbdf2119eb07b7d3c83fd9cfafe9989b64198
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#

# 这里发现 ，这种是匿名挂载，我们在-v 只写了容器内的路径，没有写容器外的路径!

# 具名挂载
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -d -P --name nginx03 -v juming-nginx:/etc/nginx  nginx
1a13b068fe4f830aa0dbda555ff5bb22c32ab8f061d533e98edb5c52592dcb96
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker volume ls
DRIVER    VOLUME NAME
local     73e11ce9c37e3d88fdb09160dc0593f0812f3bae9e3572aba305fccb747db558
local     3239a18a7f0dfea24cfa15391bf96f535d66b31accec1f692b884605cac7a048
local     de0a652f0e2ff873a2b3cdd2fdbfbdf2119eb07b7d3c83fd9cfafe9989b64198
local     juming-nginx
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#

# 通过 -v 卷名:容器内路径
# 查看下个这个券
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker volume inspect juming-nginx
[
    {
        "CreatedAt": "2021-05-18T10:36:27+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/juming-nginx/_data",
        "Name": "juming-nginx",
        "Options": null,
        "Scope": "local"
    }
]
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#


```

所有docker容器内的券，没有指定目录的情况下都是在  /var/lib/docker/volumes/xxxx/_data

我们通过具名挂载可以方便的找到我们的一个券，大多数情况在使用的具名挂载

``` shell
# 如何确定 是具名挂载还是匿名挂载，还是指定路径挂载!
-v 容器内路径  # 匿名挂载
-v 卷名：容器内路径 #具名挂载
-v /宿主机路径：容器内路径  #指定路径挂载！


```

拓展

``` shell
# 通过 -v 容器内路径： ro  rw 改变读写权限
ro	 realonly  # 只读
rw	 readwrite # 可读可写

# 一旦这个设置了容器权限，容器对我们挂载v胡来的内容就有设定了
docker run -d -P --name nginx03 -v juming-nginx:/etc/nginx:ro  nginx
docker run -d -P --name nginx03 -v juming-nginx:/etc/nginx:rw  nginx

# ro 只能通过宿主机来操作 ，容器内无法操作。

```



## 初识Dockerfile

Dockerfile 就是用来构建docker 镜像的构建文件! 命令脚本

通过这个脚本可以生成镜像，镜像是一层一层的，脚本一个个的命令

> 方式 二:



``` shell
# 创建一个dockersfile
FROM centos

VOLUME["volume01","volume02"]
CMD echo "---end-----"
CMD /bin/bash

[root@iZ2zedq4zbdzwebsgsxi9bZ docker-test]# docker build -f /home/docker-test/dockerfile1  -t zzy/centos:1.0 .


```

启动自己写的容器

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ docker-test]# docker run -it 4d20495fe76a /bin/bash
[root@94a625e2bc23 /]# docker ps
bash: docker: command not found
[root@94a625e2bc23 /]# docker ps
bash: docker: command not found
[root@94a625e2bc23 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  volume01  volume02
[root@94a625e2bc23 /]# ls -l
total 56
lrwxrwxrwx   1 root root    7 Nov  3  2020 bin -> usr/bin
drwxr-xr-x   5 root root  360 May 18 04:32 dev
drwxr-xr-x   1 root root 4096 May 18 04:32 etc
drwxr-xr-x   2 root root 4096 Nov  3  2020 home
lrwxrwxrwx   1 root root    7 Nov  3  2020 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Nov  3  2020 lib64 -> usr/lib64
drwx------   2 root root 4096 Dec  4 17:37 lost+found
drwxr-xr-x   2 root root 4096 Nov  3  2020 media
drwxr-xr-x   2 root root 4096 Nov  3  2020 mnt
drwxr-xr-x   2 root root 4096 Nov  3  2020 opt
dr-xr-xr-x 106 root root    0 May 18 04:32 proc
dr-xr-x---   2 root root 4096 Dec  4 17:37 root
drwxr-xr-x  11 root root 4096 Dec  4 17:37 run
lrwxrwxrwx   1 root root    8 Nov  3  2020 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Nov  3  2020 srv
dr-xr-xr-x  13 root root    0 May 18 04:32 sys
drwxrwxrwt   7 root root 4096 Dec  4 17:37 tmp
drwxr-xr-x  12 root root 4096 Dec  4 17:37 usr
drwxr-xr-x  20 root root 4096 Dec  4 17:37 var
drwxr-xr-x   2 root root 4096 May 18 04:32 volume01
drwxr-xr-x   2 root root 4096 May 18 04:32 volume02
[root@94a625e2bc23 /]#


```

这个券一定和外部有一个i同步的目录



```` shell 
# 1.在容器内新建文件
[root@94a625e2bc23 volume01]# touch coinner.text
[root@94a625e2bc23 volume01]# ls
coinner.text
[root@94a625e2bc23 volume01]#


# 2.在宿主机上查看卷信息
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                  NAMES
94a625e2bc23   4d20495fe76a   "/bin/bash"              12 minutes ago   Up 12 minutes                                                          silly_kilby
1a13b068fe4f   nginx          "nginx -g 'daemon of…"   2 hours ago      Up 2 hours      0.0.0.0:49154->80/tcp, :::49154->80/tcp                nginx03
26663632e044   nginx          "nginx -g 'daemon of…"   2 hours ago      Up 2 hours      0.0.0.0:49153->80/tcp, :::49153->80/tcp                nginx02
d144b5f29b06   mysql:5.7      "docker-entrypoint.s…"   3 hours ago      Up 3 hours      0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysql01
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker inspect 94a625e2bc23


# 3. 查看信息
"Mounts": [
            {
                "Type": "volume",
                "Name": "5411337d7585fe5c86b70cb4c69907bc1b020698f21b58ed8e2eb0ff02ce281d",
                "Source": "/var/lib/docker/volumes/5411337d7585fe5c86b70cb4c69907bc1b020698f21b58ed8e2eb0ff02ce281d/_data",
                "Destination": "volume02",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            },
            {
                "Type": "volume",
                "Name": "c9c078af16146276d692c5866c762a8ed48d183f1f85fe0da5a660b723d30cab",
                "Source": "/var/lib/docker/volumes/c9c078af16146276d692c5866c762a8ed48d183f1f85fe0da5a660b723d30cab/_data",
                "Destination": "volume01",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],

# 4. 查看同步文件
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# cd /var/lib/docker/volumes/c9c078af16146276d692c5866c762a8ed48d183f1f85fe0da5a660b723d30cab/_data
[root@iZ2zedq4zbdzwebsgsxi9bZ _data]# ls
coinner.text

````

## 数据卷容器

> 容器间数据共享



``` shell 
# 1. 启动容器  发现数券（volume01  volume02）

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -it --name docker01 zzy/centos:1.0
[root@413162a86e75 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  volume01  volume02
[root@413162a86e75 /]#

#  docker02 挂载 docker01   （--volumes-from 通过它 实现容器间的共享） 类似java 中继承
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker run -it --name docker02 --volumes-from docker01 zzy/centos:1.0
[root@7ec833bb9554 /]# docker ps
bash: docker: command not found
[root@7ec833bb9554 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  volume01  volume02
[root@7ec833bb9554 /]#



```

多个mysql 实现共享

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ /]# docker run -d -p 3306:3306 -v /etc/mysql/conf.d  -e MYSQL_ROOT_PASSWORD=root --name mysql01 mysql:5.7
[root@iZ2zedq4zbdzwebsgsxi9bZ /]# docker run -d -p 3306:3306 -v /etc/mysql/conf.d  -e MYSQL_ROOT_PASSWORD=root --name mysql02 --volumes-from mysql01 mysql:5.7

```





## DockerFile

dockerfile 是用来构建docker 镜像的文件!命令参数脚本！

构建步骤

1. 编写一个dockerfile 文件
2. dockerbuild 构建成为一个镜像
3. docker run 运行镜像
4. docker push 发布镜像（Docker Hub ,阿里云镜像仓科！）

``` shell 

```

DockerFile:构建文件，定义了一切的步骤，源代码

Dockerimages:通过DockerFile 构建生成镜像，最终发布和运行的产品

Docker容器：容器就是镜像运行起来提供服务器

## DockerFile 的指令

Dockerfile中包括FROM、MAINTAINER、RUN、CMD、EXPOSE、ENV、ADD、COPY、ENTRYPOINT、VOLUME、USER、WORKDIR、ONBUILD等13个指令。下面一一讲解。

``` shell 
FROM、   	# 基础镜像，一切从这里开始构建 centos
MAINTAINER、 # 镜像是谁写的， 姓名+邮箱
RUN、		# 镜像构建时候需要运行的命令
ADD			#  步骤，tomcat镜像，这个tocmat 压缩包 就是添加的内容
WORKDIR、	#镜像的工作目录
CMD、		# 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代
EXPOSE、		# 保留端口配置
ENV、		# 构建时候设置环境变量
COPY、		# 类似ADD 将我们文件拷贝到镜像中
ENTRYPOINT、 # 指定这个容器启动的时候h要云行的命令，可以最佳命令
VOLUME、		#挂载的目录
USER、
ONBUILD		# 当构建一个被继承 Dockerfile 这个时候就会运行 ONBUILD 的命令 出发指令

```





``` shell 
1.FROM
格式为FROM image或FROM image:tag，并且Dockerfile中第一条指令必须是FROM指令，且在同一个Dockerfile中创建多个镜像时，可以使用多个FROM指令。

2.MAINTAINER
格式为MAINTAINER user_name user_email，指定维护者信息

3.RUN
格式为RUN command或 RUN ["EXECUTABLE","PARAM1","PARAM2".....]，前者在shell终端中运行命令，/bin/sh -c command，例如：/bin/sh -c "echo hello"；后者使用exec执行，指定其他运行终端使用RUN["/bin/bash","-c","echo hello"]

每条RUN指令将当前的镜像基础上执行指令，并提交为新的镜像，命令较长的时候可以使用\来换行。

4.CMD
支持三种格式：
CMD ["executable","param1","param2"]，使用exec执行，这是推荐的方式。
CMD command param1 param2 在/bin/sh中执行。
CMD ["param1","param2"] 提供给ENTERYPOINT的默认参数。
CMD用于指定容器启动时执行的命令，每个Dockerfile只能有一个CMD命令，多个CMD命令只执行最后一个。若容器启动时指定了运行的命令，则会覆盖掉CMD中指定的命令。

5.EXPOSE
格式为 EXPOSE port [port2,port3,...]，例如EXPOSE 80这条指令告诉Docker服务器暴露80端口，供容器外部连接使用。
在启动容器的使用使用-P，Docker会自动分配一个端口和转发指定的端口，使用-p可以具体指定使用哪个本地的端口来映射对外开放的端口。

6.ENV
格式为：EVN key value 。用于指定环境变量，这些环境变量，后续可以被RUN指令使用，容器运行起来之后，也可以在容器中获取这些环境变量。
例如
ENV word hello
RUN echo $word

7.ADD
格式：ADD src dest
该命令将复制指定本地目录中的文件到容器中的dest中，src可以是是一个绝对路径，也可以是一个URL或一个tar文件，tar文件会自动解压为目录。

8.COPY
格式为：COPY src desc
复制本地主机src目录或文件到容器的desc目录，desc不存在时会自动创建。

9.ENTRYPOINT
格式有两种：
ENTRYPOINT ["executable","param1","param2"]
ENTRYPOINT command param1,param2 会在shell中执行。
用于配置容器启动后执行的命令，这些命令不能被docker run提供的参数覆盖。和CMD一样，每个Dockerfile中只能有一个ENTRYPOINT，当有多个时最后一个生效。

10.VOLUME
格式为 VOLUME ["/data"]
作用是创建在本地主机或其他容器可以挂载的数据卷，用来存放数据。

11.USER
格式为：USER username
指定容器运行时的用户名或UID，后续的RUN也会使用指定的用户。要临时使用管理员权限可以使用sudo。在USER命令之前可以使用RUN命令创建需要的用户。
例如：RUN groupadd -r docker && useradd -r -g docker docker

12.WORKDIR
格式： WORKDIR /path
为后续的RUN CMD ENTRYPOINT指定配置工作目录，可以使用多个WORKDIR指令，若后续指令用得是相对路径，则会基于之前的命令指定路径。

13.ONBUILD
格式ONBUILD [INSTRUCTION]
该配置指定当所创建的镜像作为其他新建镜像的基础镜像时所执行的指令。
例如下面的Dockerfile创建了镜像A：
ONBUILD ADD . /app
ONBUILD RUN python app.py

则基于镜像A创建新的镜像时，新的Dockerfile中使用from A 指定基镜像时，会自动执行ONBBUILD指令内容，等价于在新的要构建镜像的Dockerfile中增加了两条指令：
FROM A
ADD ./app
RUN python app.py

14.docker build
创建好Dockerfile之后，通过docker build命令来创建镜像，该命令首先会上传Dockerfile文件给Docker服务器端，服务器端将逐行执行Dockerfile中定义的指令。
通常建议放置Dockerfile的目录为空目录。另外可以在目录下创建.dockerignore文件，让Docker忽略路径下的文件和目录，这一点与Git中的配置很相似。

通过 -t 指定镜像的标签信息，例如：docker build -t regenzm/first_image . ##"."指定的是Dockerfile所在的路径
```



## 实战测试

Docker Hub 中99% 镜像都是从这个基础镜像过来的Feom screatch ,然后配置需要的软件和配置来进行构建

> 创建一个自己的centos 



``` shell 
# 创建
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# mkdir dockerfile    # 创建文件
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# ls
ceshi  dockerfile  docker-test  mysql  project  test.java
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# cd dockerfile/
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# ls
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# vim mydockerfile-centos
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# ls
mydockerfile-centos
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# cd ../
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# cat dockerfile/
cat: dockerfile/: Is a directory
[root@iZ2zedq4zbdzwebsgsxi9bZ home]# cd dockerfile/
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# ls
mydockerfile-centos
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# cat mydockerfile-centos   # 查看dockersfile 文件内容
FROM centos
MAINTAINER zzy<634187436@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "---end---"
CMD /bin/bash

# 制作镜像
[root@iZ2zedq4zbdzwebsgsxi9bZ dockerfile]# docker build -f mydockerfile-centos -t mycentos:0.1 .


```



> 查看镜像制作过程

``` shell 
docker history 镜像id

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker history cd69e4304a6a
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
cd69e4304a6a   17 minutes ago   /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "/bin…   0B
1b9b46e5b33c   17 minutes ago   /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "echo…   0B
b33718ed2c44   17 minutes ago   /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "echo…   0B
b8695bc261f2   17 minutes ago   /bin/sh -c #(nop)  EXPOSE 80                    0B
66e94c9bd882   17 minutes ago   /bin/sh -c yum -y install net-tools             23.3MB
2d2c7f3f27b8   17 minutes ago   /bin/sh -c yum -y install vim                   58MB
4fca8418a888   19 minutes ago   /bin/sh -c #(nop) WORKDIR /usr/local            0B
78233c660eac   19 minutes ago   /bin/sh -c #(nop)  ENV MYPATH=/usr/local        0B
90c5c70c9933   19 minutes ago   /bin/sh -c #(nop)  MAINTAINER zzy<634187436@…   0B
300e315adb2f   5 months ago     /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>      5 months ago     /bin/sh -c #(nop)  LABEL org.label-schema.sc…   0B
<missing>      5 months ago     /bin/sh -c #(nop) ADD file:bd7a2aed6ede423b7…   209MB
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]#

```



> CMD  和 ENTRYPOINT对比

``` shell 
FROM centos 
CMD ["ls","-a"]
# 构建镜像
docker build -f dockerfild-cmd-test -t cmdtest .

# run  运行  发现 ls -a 命令生效
# 想追加 一个命令-l ls -al 
docker run 镜像id  -l

# cmd 的清理一下-l 替换了["ls","-a"] 命令，-l  不是命令所以报错

测试 ENTRYPOINT
vim dockerfile-cmd-enterpoint
FROM centos 
ENTRYPOINT ["ls","-a"]

docker build -f dockerfile-cmd-entrypoint -t entorypoint-test .


这个可以 是 追加在命令后面 可以执行

```



##  实战Tomcat  镜像

1. 准备镜像文件 tomcat 压缩包，jdk 压缩包！
2. 编写dockerfile文件 ，官方命名 Dockerfile ,build 会自动寻找这个文件，就不需要-f 指定了！

``` shell 
FROM centos
MAINTAINER zzy<634187436@qq.com>

COPY readme.txt /usr/local/readme.txt

ADD jdk-8u251-linux-x64.tar.gz /usr/local/
ADD apache-tomcat-9.0.46.tar.gz /usr/local/

RUN yum -y install vim

ENV MYPATH /usr/local
WORKDIR SMYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_251
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.46
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.46
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

EXPOSE 8080

CMD /usr/local/apache-tomcat-9.0.46/bin/startup.sh && tail -F /url/local/apache-tomcat-9.0.46/bin/logs/catalina.out

```



运行容器

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# clear
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker run -d -p 8003:8080 --name zzytomcat -v /home/zzy/tomcat/test:/usr/local/apache-tomcat-9.0.46/webapps/test -v /home/zzy/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.46/logs diytomcat



```



web.xml

``` shell 

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.4" 
    xmlns="http://java.sun.com/xml/ns/j2ee" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee 
        http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
</web-app>
```

index.jsp

``` shell 
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
Hello World!<br/>
<%
	System.out.println("hello log tomcat");
%>
</body>
</html>
```



##  发布自己的镜像



1. https://hub.docker.com/   注册登录

2. 登录

   ``` shell 
   [root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker login --help
   
   Usage:  docker login [OPTIONS] [SERVER]
   
   Log in to a Docker registry.
   If no server is specified, the default is defined by the daemon.
   
   Options:
     -p, --password string   Password
         --password-stdin    Take the password from stdin
     -u, --username string   Username
   [root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker login -u xiaozhi9826
   Password:
   
   ```

3.push 遇到问题

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker push zzy/diytomcat:1.0
The push refers to repository [docker.io/zzy/diytomcat]
An image does not exist locally with the tag: zzy/diytomcat

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED          SIZE
diytomcat             latest    2e7cfa4931fa   55 minutes ago   689MB
 
 #发现TAG 没有版本号
# 决绝

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker tag 2e7cfa4931fa  xiaozhi0826/tomcat:1.0

[root@iZ2zedq4zbdzwebsgsxi9bZ ~]# docker push xiaozhi0826/tomcat:1.0
The push refers to repository [docker.io/zzy/tomcat]
2c4843e5468d: Preparing
bab20ab78464: Preparing
af5ba248096f: Preparing
19e16755f156: Preparing
a37801a6743b: Preparing
可以提交了


```



## 发布阿里云镜像服务上

> 发布阿里云镜像服务上

1. 登录阿里云
2. 找到容器镜像服务 
3. 创建命名空间
4. 创建镜像仓库 ----》下一步时候选择本地仓库
5. 查看官方帮助文档





## Dockers 网络



理解Docker0

清空所有镜像 及容器

> 测试

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo		# 本机回环地址
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:34:54:aa brd ff:ff:ff:ff:ff:ff
    inet 172.17.159.16/20 brd 172.17.159.255 scope global dynamic eth0 #阿里云内网地址
       valid_lft 315181181sec preferred_lft 315181181sec
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:5b:2f:7d:53 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global docker0 #docker0 地址
       valid_lft forever preferred_lft forever
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```

三个网络

> 问题 docker 是如何处理容器网络访问的？



``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker run -d -P --name tomcat01 tomcat
Unable to find image 'tomcat:latest' locally
latest: Pulling from library/tomcat
d960726af2be: Pull complete
e8d62473a22d: Pull complete
8962bc0fad55: Pull complete
65d943ee54c1: Pull complete
da20b77f10ac: Pull complete
8669a096f083: Pull complete
e0c0a5e9ce88: Pull complete
f7f46169d747: Pull complete
42d8171e56e6: Pull complete
774078a3f8bb: Pull complete
Digest: sha256:10842dab06b5e52233ad977d4689522d4fbaa9c21e6df387d7a530e02316fb45
Status: Downloaded newer image for tomcat:latest
256544890ef009e1fb66525b2ae712420ca05d03620e41fc2b7f64f23e2967b0
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker ps
CONTAINER ID   IMAGE     COMMAND             CREATED              STATUS              PORTS                                         NAMES
256544890ef0   tomcat    "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:49155->8080/tcp, :::49155->8080/tcp   tomcat01
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it 256544890ef0 ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
46: eth0@if47: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:12:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.18.0.2/16 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#




```



``` shell 
# 我们发现这个容器带来网卡，都是一对一对的
# evth-pair  就是一对的虚拟设备接口，他们都是成对出现的，一段连着协议，一段彼此相连
# 正因为有这个特性，ecth-pair 充当一个桥梁，链接各种虚拟网络设备的
# OpenStace,Docker 容器之间的链接，OVS 的链接，都是使用 evth-pair 技术

```



3.测试tomcat 01 和tomcat 02是否可以pin 通

``` shell 
docker exec -it tomcat02 pin 172.18.0.1

# 结论 ：容器和容器之间是可以相互ping 通的

```



--link 

> 思考  我们编写了一个微服务，database url=ip; ,项目不重启，数据库ip换掉了.我们希望可以处理这个问题
>
> 名字来进行访问容器



``` shell
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker ps
CONTAINER ID   IMAGE     COMMAND             CREATED          STATUS          PORTS                                         NAMES
959e42be349e   tomcat    "catalina.sh run"   55 seconds ago   Up 54 seconds   0.0.0.0:49157->8080/tcp, :::49157->8080/tcp   tomcat03
23cf1e273fd3   tomcat    "catalina.sh run"   15 minutes ago   Up 15 minutes   0.0.0.0:49156->8080/tcp, :::49156->8080/tcp   tomcat02
256544890ef0   tomcat    "catalina.sh run"   2 hours ago      Up 2 hours      0.0.0.0:49155->8080/tcp, :::49155->8080/tcp   tomcat01
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it tomcat03 ping tomcat02
PING tomcat02 (172.18.0.3) 56(84) bytes of data.
64 bytes from tomcat02 (172.18.0.3): icmp_seq=1 ttl=64 time=0.101 ms
64 bytes from tomcat02 (172.18.0.3): icmp_seq=2 ttl=64 time=0.088 ms
64 bytes from tomcat02 (172.18.0.3): icmp_seq=3 ttl=64 time=0.085 ms
^C
--- tomcat02 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.085/0.091/0.101/0.010 ms
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```

 探究原理

``` shell 
# 查看hosts 文件 link tomcat03 链接 tomcat02 原理
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it tomcat03 cat /etc/hosts
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.18.0.3      tomcat02 23cf1e273fd3
172.18.0.4      959e42be349e
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```

docker0 问题:他不支持容器名链接访问



##  自定义网络

> 查看所有docker 网络

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
7126dadeb3c1   bridge    bridge    local
758f860d252f   host      host      local
8899fb47b822   none      null      local
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```

网络模式

brigbe ： 桥接docker(默认，自己创建也使用桥接模式)

none  : 不配置网络

host :  和宿主机共享网络

container：容器网络联通！(用的少，局限很大)



测试

 ``` shell 
# 我们直接启动的命令 --net bridge ,而这个就是我们的docker0
docker run -d -P --name tomcat01 tomcat
docker run -d -p --name --net bridge tomcat

# docker0特点， 默认，域名不能访问，--link 可以打通链接

#我们自定义一个网络
#--driver bridge  桥接
#--subnet 192.168.0.0/16 子网掩码 
#--gateway 192.168.0.1   网关（路由器）
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
b8e32c240c382a27e9f39e901da4d20ce076e6bd71d8381e01c00d8834a43d19
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
7126dadeb3c1   bridge    bridge    local
758f860d252f   host      host      local
b8e32c240c38   mynet     bridge    local
8899fb47b822   none      null      local
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#


 ```

> 查看我们自己的网络

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network inspect mynet
[
    {
        "Name": "mynet",
        "Id": "b8e32c240c382a27e9f39e901da4d20ce076e6bd71d8381e01c00d8834a43d19",
        "Created": "2021-05-19T13:50:54.503929827+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "192.168.0.0/16",
                    "Gateway": "192.168.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```



>  启动容器 引用自己的网络

``` shell 
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker run -d -P --name tomcat-net01 --net mynet tomcat
7288e07a235b7da45f9ebfe6a339e58ec1219f64d56ce520a58b066cc2d3a1d0
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker run -d -P --name tomcat-net02 --net mynet tomcat
b51912c8c90cc64d7dcb7ee407108f10b78c1fca5fbbde5547bcaf21bb018bc3
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker ps
CONTAINER ID   IMAGE     COMMAND             CREATED          STATUS          PORTS                                         NAMES
b51912c8c90c   tomcat    "catalina.sh run"   6 seconds ago    Up 5 seconds    0.0.0.0:49159->8080/tcp, :::49159->8080/tcp   tomcat-net02
7288e07a235b   tomcat    "catalina.sh run"   13 seconds ago   Up 12 seconds   0.0.0.0:49158->8080/tcp, :::49158->8080/tcp   tomcat-net01
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -li tmcat-net01 ping tomcat-net02
unknown shorthand flag: 'l' in -li
See 'docker exec --help'.
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it tmcat-net01 ping tomcat-net02
Error: No such container: tmcat-net01
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec --help

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Run a command in a running container

Options:
  -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a container
  -e, --env list             Set environment variables
      --env-file list        Read in a file of environment variables
  -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
  -t, --tty                  Allocate a pseudo-TTY
  -u, --user string          Username or UID (format: <name|uid>[:<group|gid>])
  -w, --workdir string       Working directory inside the container
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it mytomcat-net01 ping mytomcat-net02
Error: No such container: mytomcat-net01
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker exec -it tomcat-net01 ping tomcat-net02
PING tomcat-net02 (192.168.0.3) 56(84) bytes of data.
64 bytes from tomcat-net02.mynet (192.168.0.3): icmp_seq=1 ttl=64 time=0.090 ms
64 bytes from tomcat-net02.mynet (192.168.0.3): icmp_seq=2 ttl=64 time=0.081 ms
64 bytes from tomcat-net02.mynet (192.168.0.3): icmp_seq=3 ttl=64 time=0.114 ms
^C
--- tomcat-net02 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2ms
rtt min/avg/max/mdev = 0.081/0.095/0.114/0.013 ms
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]#

```

>  测试 打通  tomcat01 - mynet

``` shell
docker network connect mynet tomcat01
docker network inspect mynet
# 连通之后
```



## 实战部署Docker 集群

shell  脚本

``` shell 
# 创建网卡
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network create redis --subnet 127.38.0.0/16
255a181d2659fcdb6b6212be8fd85d155a00f8de94e44388c6806aae6d02983a
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# dcoker network ls
-bash: dcoker: command not found
[root@iZ2zedq4zbdzwebsgsxi9bZ tomcat]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
7126dadeb3c1   bridge    bridge    local
758f860d252f   host      host      local
b8e32c240c38   mynet     bridge    local
8899fb47b822   none      null      local
255a181d2659   redis     bridge    local

# 通过 脚本创建六个redis 配置

for port in $(seq 1 6); \
do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf
cat << EOF >>/mydata/redis/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 127.38.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done

```



``` shell
docker run -p 6371:6379 -p 16371:16379 --name redis-1 \
 -v /mydata/redis/node-1/data:/data \
 -v /mydata/redis/node-1/conf/redis.conf:/etc/redis/redis.conf \
 -d --net redis --ip 127.38.0.11 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf

```



Springboot 打包镜像

```` shell 
# Dockerfile
FROM java:8

COMPY *.java /app.jar

CMD ["--server.port=8080"]

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app.jar"]



````

![](F:\gitproject\demo\开发文档资料\images\Docker\04.png)



![](F:\gitproject\demo\开发文档资料\images\Docker\03.png)