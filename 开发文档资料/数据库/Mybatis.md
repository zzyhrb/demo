# Mybatis

## 1.  地址

> https://mybatis.org/mybatis-3/zh/index.html

## 2. 简介



### 2.1 什么是MyBatis？

* MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。
* MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
* MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

### 2.2 持久化

数据持久化

* 持久化就是将程序的数据在持久状态 和瞬时状态转化的过程
* 内存: 断电既失
* 数据库（JDBC）,Io 文件持久化
* 生活：冷藏

为啥需要持久化？

* 有一些对象，不能让他丢失(存钱)
* 内存太贵

### 2.3 持久层

Dao  层   Service 层  ，Controller 层

* 完成持久化工作的代码块
* 层界限十分明显

### 2.4 为啥需要Mybatis 

* 传统JDBC  太复杂，简化 ，框架，自动化
* 帮助程序员将数据存到数据库中
* 优点
  - 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
  - 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  - 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql



## 3.第一个Mydatis 程序

### 3.1 环境搭建

	* 新建一个Maven 项目 删除项目中的src 文件夹 （作为父工程项目）
	* 导入依赖

``` java 


```



### 3.2 创建第一个模块



 

## 4. 配置解析

### 4.1 核心配置文件



* Mybatis-config.xml
* Mybatis 的配置文件包含了会深深影响的Mybatis 行为的设置和属性信息

``` java 
configuration（配置）
properties（属性）
settings（设置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境配置）
environment（环境变量）
transactionManager（事务管理器）
dataSource（数据源）
databaseIdProvider（数据库厂商标识）
mappers（映射器）
```



### 4.2 环境配置 （environments）

MyBatis 可以配置成适应多种环境

**过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

Mybatis 默认的事务管理器就是JDBC   ，链接池：POOLED 



1.编写一个配置文件

db.properties

``` xml
driver = com.mysql.jdbc.Driver
url = jdbc:mysql://localhost:3306/tzms?useUnicode=true&;characterEncoding=utf8&;nullCatalogMeansCurrent=true&;useSSL=false&;useLegacyDatetimeCode=false&;serverTimezone=UTC
username = root
password = root
```

2.在mybatis-config.xml  引入外部配置文件

``` xml
 <!--引入外部配置文件-->
    <properties resource="db.properties">
        <property name="username" value="root"/>
    </properties>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

```



### 4.3 typeAliases（类型别名）

``` xml
<!-- 1-->
  <typeAliases>
        <typeAlias type="com.zzy.pojo.User" alias="User"></typeAlias>
  </typeAliases>
<!-- 也可以使用实体类起别名-->
    <typeAliases>
   		 <package name="com.zzy.pojo"/>
	</typeAliases>
```

> 注意:

在实体类比较少的时候使用第一种

如果实体类十分多使用第二种

第一种可以DIY 别名，的二种则不行，如非要改 需要在实体类加注释

``` java 
@Alias("user")
public class User {
    
}
```



### 4.5 解决属性名和字段名不一致

​	**resultMap**

``` xml
<resultMap id="UserMap" type="user">
        <!--column 数据库中的字段  property 实体类中的属性 -->
        <result column="id" property="id"></result>
        <result column="username" property="username"></result>
        <result column="email" property="email"></result>
        <result column="mobile" property="mobile"></result>
    </resultMap>

    <select id="getUserById" parameterType="int" resultMap="UserMap">
        select * from  sys_users where id=#{id}
    </select>

```

### 4.6 日志工厂

``` xml

    <!--引入外部配置文件-->
    <properties resource="db.properties">
        <property name="username" value="root"/>
    </properties>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="com/zzy/dao/UserMapper.xml"/>
    </mappers>
```

