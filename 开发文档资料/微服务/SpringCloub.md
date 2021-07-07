# SpringCloud

## 1. 系统架构

![](F:\gitproject\demo\开发文档资料\images\Springcloud\01.png) 



>参考书

* https://www.springcloud.cc/spring-cloud-netflix.html
* 中文API 帮助文档: https://www.springcloud.cc/spring-cloud-dalston.html
* SpringCloud 中国社区 ：



##  2.版本对照表

| spring-cloud-dependencies 版本 | spring-cloud 版本 | spring-boot 版本 | spring 版本    |
| :----------------------------- | :---------------- | :--------------- | :------------- |
| 2020.0.1                       | 3.0.1             | 2.4.2            | 5.3.3          |
| 2020.0.0                       | 3.0.0             | 2.4.1            | 5.3.2          |
| Hoxton.SR10                    | 2.2.7.RELEASE     | 2.3.8.RELEASE    | 5.2.12.RELEASE |
| Hoxton.SR9                     | 2.2.6.RELEASE     | 2.3.2.RELEASE    | 5.2.8.RELEASE  |
| Hoxton.SR8                     | 2.2.5.RELEASE     | 2.3.2.RELEASE    | 5.2.8.RELEASE  |
| Hoxton.SR7                     | 2.2.4.RELEASE     | 2.3.2.RELEASE    | 5.2.8.RELEASE  |
| Hoxton.SR6                     | 2.2.3.RELEASE     | 2.3.0.RELEASE    | 5.2.6.RELEASE  |
| Hoxton.SR5                     | 2.2.3.RELEASE     | 2.3.0.RELEASE    | 5.2.6.RELEASE  |
| Hoxton.SR4                     | 2.2.2.RELEASE     | 2.2.5.RELEASE    | 5.2.4.RELEASE  |
| Hoxton.SR3                     | 2.2.2.RELEASE     | 2.2.5.RELEASE    | 5.2.4.RELEASE  |
| Hoxton.SR2                     | 2.2.1.RELEASE     | 2.2.2.RELEASE    | 5.2.2.RELEASE  |
| Hoxton.SR1                     | 2.2.1.RELEASE     | 2.2.2.RELEASE    | 5.2.2.RELEASE  |
| Greenwich.SR6                  | 2.1.6.RELEASE     | 2.1.13.RELEASE   | 5.1.11.RELEASE |
| Greenwich.SR5                  | 2.1.5.RELEASE     | 2.1.10.RELEASE   | 5.1.11.RELEASE |
| Greenwich.SR4                  | 2.1.4.RELEASE     | 2.1.10.RELEASE   | 5.1.11.RELEASE |
| Greenwich.SR3                  | 2.1.3.RELEASE     | 2.1.7.RELEASE    | 5.1.9.RELEASE  |
| Greenwich.SR2                  | 2.1.2.RELEASE     | 2.1.5.RELEASE    | 5.1.7.RELEASE  |
| Greenwich.SR1                  | 2.1.1.RELEASE     | 2.1.3.RELEASE    | 5.1.5.RELEASE  |
| Finchley.SR4                   | 2.0.4.RELEASE     | 2.0.9.RELEASE    | 5.0.13.RELEASE |
| Finchley.SR3                   | 2.0.3.RELEASE     | 2.0.8.RELEASE    | 5.0.12.RELEASE |
| Finchley.SR2                   | 2.0.2.RELEASE     | 2.0.6.RELEASE    | 5.0.10.RELEASE |
| Finchley.SR1                   | 2.0.1.RELEASE     | 2.0.4.RELEASE    | 5.0.8.RELEASE  |
| Edgware.SR6                    | 1.3.6.RELEASE     | 1.5.21.RELEASE   | 4.3.24.RELEASE |
| Edgware.SR5                    | 1.3.5.RELEASE     | 1.5.16.RELEASE   | 4.3.19.RELEASE |
| Edgware.SR4                    | 1.3.4.RELEASE     | 1.5.14.RELEASE   | 4.3.18.RELEASE |
| Edgware.SR3                    | 1.3.3.RELEASE     | 1.5.10.RELEASE   | 4.3.14.RELEASE |
| Edgware.SR2                    | 1.3.2.RELEASE     | 1.5.10.RELEASE   | 4.3.14.RELEASE |
| Edgware.SR1                    | 1.3.2.RELEASE     | 1.5.9.RELEASE    | 4.3.13.RELEASE |
| Dalston.SR5                    | 1.2.5.RELEASE     | 1.5.9.RELEASE    | 4.3.13.RELEASE |
| Dalston.SR4                    | 1.2.4.RELEASE     | 1.5.7.RELEASE    | 4.3.11.RELEASE |
| Dalston.SR3                    | 1.2.3.RELEASE     | 1.5.4.RELEASE    | 4.3.9.RELEASE  |
| Dalston.SR2                    | 1.2.3.RELEASE     | 1.5.4.RELEASE    | 4.3.9.RELEASE  |
| Dalston.SR1                    | 1.2.2.RELEASE     | 1.5.3.RELEASE    | 4.3.8.RELEASE  |
| Camden.SR7                     | 1.1.9.RELEASE     | 1.3.8.RELEASE    | 4.3.4.RELEASE  |
| Camden.SR1                     | 1.1.4.RELEASE     | 1.3.7.RELEASE    | 4.2.7.RELEASE  |
| Brixton.SR7                    | 1.1.4.RELEASE     | 1.3.7.RELEASE    | 4.2.7.RELEASE  |
| Brixton.SR1                    | 1.1.1.RELEASE     | 1.3.5.RELEASE    | 4.2.6.RELEASE  |

> pom.xml 配置文件



``` xml
<groupId>com.sinosoft.yuebao</groupId>
<artifactId>platfrom</artifactId>
<packaging>pom</packaging> <!-- 打包方式-->
<version>1.0-SNAPSHOT</version>

<!--SpringBoot 启动器-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.0</version>
</dependency>


```



## 3. 注解

> **lombok @Accessors用法**



``` java
@Accessors(fluent = true)
fluent 若为true，则getter和setter方法的方法名都是属性名，且setter方法返回当前对象。
    
@Accessors(chain = true)  // 链式写法
chain 若为true，则setter方法返回当前对象
    例子: Dept  dept  =new Dept()
    	dept.setDeptNo(11).setDname('dd')
    
@Accessors(prefix = "f")
prefix 若为true，则getter和setter方法会忽视属性名的指定前缀（遵守驼峰命名）
```

