## JDK  安装



1. 官网下载jdk  rpm  包

2. 安装java 环境

   ``` bash
   #  检查当前系统是否存在java 环境  java -version
   #  如果存在需要卸载
   	rpm -qa |grep jdk  # 检查jdk版本信息
   	rpm -e --nodeps  jdk_
   	
   #  卸载完毕后可以安装jdk
   # rpm -ivh rpm包
   [root@iZ2zecgcw2x546cmowlk5fZ zkr]# rpm -ivh jdk-8u291-linux-x64.rpm
   ```

3. 安装环境变量

   vim /etc/profile

   ``` bash
   unset i
   unset -f pathmunge
   JAVA_HOME=/usr/java/jdk1.8.0_291-amd64
   CLASSPATH=%JAVA_HOME%/lib;%JAVA_HOME%/jre/lib
   PATH=$JAVA_HOME/bin;$JAVA_HOME/jre/bin
   export PATH CLASSPATH  JAVA_HOME
   ```

   让配置文件生效 : source /etc/profile

> 查看当前开启的端口

``` ba
firewall-cmd --list-ports

需要开启防火墙即可

开启防火墙：systemctl start firewalld

关闭防火墙：systemctl stop firewalld

查看防火墙状态：systemctl status firewalld
```





## Tomcat  安装



1. 下载包

2. 解压 tar -zxvf 包名

   ``` bash
   [root@iZ2zecgcw2x546cmowlk5fZ zkr]# tar -zxvf apache-tomcat-8.5.68-fulldocs.tar.gz
   
   
   ## 遇到问题
   1、vi command not found ，输入任何命令都无法实现
   
   只要原因是因为环境变量的问题，编辑profile文件没有写正确，导致在命令行下 ls等命令不能够识别。
   
    
   解决办法：在命令行下打入下面这段就可以了 
   export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
   
   ```

   