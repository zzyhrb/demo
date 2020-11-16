



# 一 MarkDown学习

## 1.标题



## 2.字体

- **Helllo Word**
- ***Hello Word***
- ~~Hello Word~~



## 3.引用

> 引内容



## 4.分割线



***



## 5.图片

![截图](F:\gitproject\demo\开发文档资料\images\20200729182438315.png)

## 6.超链接

[地址](https://spring.io/projects/spring-cloud)



## 7.列表

### 7.1有序列表

 1. A

 2. B

 3. C

### 7.1无序列表
    * 1
    
    * 2
    
    * 3
    
    * 4


​      

## 8.列表

| 名字 | 年龄 |
| ---- | ---- |
|      |      |
|      |      |



## 9.代码

```java 
  public static void main(String []ags){
        int [] array ={1,2,3,4,5};
        for(int i=0;i<array.length;i++){
        }
    }
```

 



# 二 java 基础语法

## 0.java环境变量配置

### 0.1 JDK 环境变量配置

  ```java
1.JAVA_HOME    C:\Program Files\Java\jdk1.8.0_144   
2.CLASSPATH    .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
3.编辑Path      %JAVA_HOME%\bin       %CLASSPATH%
  ```

### 0.2 MAVEN 环境变量配置   

  ```java 
1.MAVEN_HOME   E:\tools\apache-maven-3.3.3  
2.Path         %MAVEN_HOME%\bin    
  ```

### 0.3MySql  

  ```java
1. MYSQL_HOME    E:\tools\mysql-5.7.21-winx64
2. Path          %MYSQL_HOME%\bin          
  ```

​    

## 1.数据类型

* Java 是强数据类型语言
* Java 数据类型分为两类
  1. 基础数据类型
  2. 引用数据类型

## 2.什么是字节

![图片](F:\gitproject\demo\开发文档资料\images\java\20201116135951.png)

## 3.类型转换

​	![类型转换](F:\gitproject\demo\开发文档资料\images\java\类型转换.png)



### 3.1类型转换详解

 * 强制类型转换  

   （类型）变量名     高---低

   ```java 
   int  a=100;
   bate b=a;
   ```

* 自动类型转换

  ​	低---高

* 注意点

  ```txt
  1.不能对布尔值进行转换
  2.不能吧对象类型转为不相干的类型
  3.在把高容量转换到低容量的时候，强制转换
  4.转换的时候可能存在内存溢出，或者精度问题。
  
  System.out.print((int)23.7); //23
  System.out.print((int)-45.89f); //-45
  ```

* 操作比较大数字是注意溢出问题

  ```java
  //JDK7 新特性，数字之间各异用下环线分割
  int money = 10_0000_0000;
  int year =20;
  int total= money*year; //-1474836480，计算的时候溢出了
  long total2=money*((long)year);//先把一个数字转换为long
  ```

  

## 变量

![变量](F:\gitproject\demo\开发文档资料\images\java\变量.png)

### 1.变量作用域

   * 类变量

   * 实列变量

   * 局部变量

     ```java
     public class TestDemo {
         static int allclicks=0;//类变量
         String str ="你好"; //实例变量
         public  void method(){
             int i=0; //局部变量
         }
     }
     ```

     





​	













# 五十 SpringBoot （篇）

## 1.Windows 系统发布（jar包）

* 创建文件：xxxxx.bat (创建一个.bat文件。**例如:Battery.bat**)

* 文件内容

  ```java
  @echo off
  set path=C:\Program Files\Java\jdk1.8.0_144\jre\bin
  START "Battery" "%path%\javaw" -jar C:\project\Ba.jar
  ```

  

## 2. kas



# 六十 Vs code (基础篇)

## 1.快捷键

* 控制台显示

  ```java 
  ctrl + shift + y 
  ```

## 2. 初始化项目

 * 初始化项目

   ```jav
   >npm install
   ```

   

* 运行项目

  ```java 
  npm  run dev
  ```

  

# 七十 Git 基础

## 1. 密钥

 * 生成RSA密钥对

   ```java
   ssh-keygen -t rsa -C "你的邮箱@xxx.com"
   ```

* 查看  公钥内容

  ```java 
  cat ~/.ssh/id_rsa.pub
  ```

  

# 八十 Linux 基础

## 1.查看文件命令

```kotlin
># ls -a
```

## 2.Linux MySQL 无线延续

```java
1.切换文件到　.navaicat64/
2.删除文件　rm -rf user.reg
```

# 九十 Docker 基础

## 1.安装Docker

```java
1.》 yum  update 
2.>  yum install docker-ce -y
3.>  docker -v
```



## 2.启动Docker

```java
》systemctl start docker
2.重启Docker 
》systemctl restart docker
3.停止Docker
》systemctl stop docker
# 查看docker状态：
systemctl status docker
```

# 一零零 Node.js

## 1.下载安装

* 官网下载安装node.js,并使用node-v 检查版本

* 配置npm 使用淘宝镜像

  ```java 
  npm config set registry " https://registry.npm.taobao.org "
  ```

  



