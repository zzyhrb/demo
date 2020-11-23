





























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

  

## 4.变量

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
​     
​     
## 5.常量

* 常量：初始化后不能在修改变直！不会变动的值。
* 所谓常量可以理解成一种特殊的变量， 它的值被设定后，在程序执行过程中不允许被修改。

```java
 final 常量名  =值；
 final bouble PI =3.14;
```

​       

* 常量名一般使用大写字符。

## 6.运算符

   * Java 语言支持如下运算符
     
       1.算数运算符：+，-，*，/,%,++,--
       
       2.赋值运算符 =
       
       3.关系运算符：>,<,>=,<=,==,!= instanceof
       
       4.逻辑运算符：&&，||，！
       
       5.位运算符：&，|，^,~,>>,<<,>>>(了解)
       
       6.条件运算符：？ ：
       
       7.扩展运算符：+=,-=,*=,/=


​     
​     
```java
     public static void main(String[] args) {
     		long  a=1231231313L;
     		int b= 10;
     		short c=1;
     		byte d=2;
     		
     		System.out.println(a+b+c);//long
     		System.out.println(b+c); //Int
     		System.out.println(c+d);//Int

         
         	int a =3;
     		int b= a++; //先执行完这行代码后,给b复制在自增
     		//a = a+1
     		System.out.println(a);//4
     		//a =a+1
     		int c= ++a;//执行代码前，先自增在给C 赋值
     		System.out.println(a);//5
     		System.out.println(b);//3
     		System.out.println(c);//5
     		
     		//幂运算  用工具来操作
     		double pow =Math.pow(3, 2);
     		System.out.println(pow);

      
         	//与 （and） 或 （or） 非 (取反)
     		boolean a= true;
     		boolean b=false;
     		
     		System.out.println("a && b :"+(a && b));//逻辑与运算：两个变量都为真，结果才为真
     		System.out.println("a || b :"+(a || b));//逻辑或运算:两个变量有一个为真，结果才为真
     		System.out.println("!(a && b) :"+!(a &&b));//如果是真 则为假 ， 如果是假则为真。
     		
     		//短路运算
     		int c =5;
     		boolean d =(c<4)&&(c++ < 4);
     		System.out.println(c); //5
     		System.out.println(d); //false
     	}


		
```

**总结：如果有一个整数类型相加有一个是long 结果就会转成long 类型，没有long  结果否是int类型**  



​     ![位运算符](D:\gitProject\demo\开发文档资料\images\java位运算符.png)


​     

## 7.流程控制

### 1.用户输入(scanner)

* 基础语法

  

```java
       	Scanner scanner =new Scanner(System.in);
       	System.out.println("使用next方式接受:");
       	//判断用户有没有输入字符串
       	if(scanner.hasNext()){
       		//使用next方式接收
       		String str =scanner.next();
       		System.out.println("输出的结果为:"+str);
       		
       	}
       	scanner.close();
       
       	//判断语句
       
       	int i=0;
       	float f= 0.0f;
       	System.out.println("请输入整数");
       	Scanner scanner =new Scanner(System.in);
       	//判断用户有没有输入字符串
       	if(scanner.hasNextInt()){
       		//使用next方式接收
       		i =scanner.nextInt();
       		System.out.println("输出的结果为:"+i);
       	}else{
       		System.out.println("输入的不是数字");
       	}
       	scanner.close();
       
       	//输入多个数字，求和与平均数
       
       	System.out.println("请输入需要计算的数字");
       	Scanner scanner =new Scanner(System.in);
       	//总和
       	double sum=0;
       	//记录数
       	int count=0;
       	
       	while(scanner.hasNextInt()){
       		 double x =scanner.nextInt();
       		 sum +=x; //sum =sum+x
       		 count+=1;//count=count +1
       	}
       	System.out.println("总和是"+sum +"记录次数"+count+"评价数是"+sum/count);
       	
       	scanner.close();
```


  * **总结**：如果输入的有空格 用next()接收不显示空格后面内容，用nextLine() 会都显示







## 8.顺序结构



```java
System.out.println("1");
System.out.println("2");
System.out.println("3");

```

## 9.选择结构

* if 但选择结构

  ```java
  if(布尔表达式){
      //如果布尔值为true 执行
  }
      
  ```

  

* switch 多选择结构

  1. 多选择结构还有一个实现饿方式就是switch case 语句。

  2. switch case 语句判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。

  3. switch 语句中的变量类型可以是：

     * byte,short.int 或者 char.
     * 从java 7 开始
     * switch 支持字符串String 类型
     * 同时case 标签必须为字符串常量或字面量。

     ![switch图片](F:\gitproject\demo\开发文档资料\images\java\switch-01.png)



 	## 10.循环结构

* while 循环 
* do.....while 循环
* for 循环
* 在java5中引入了一种主要用于数组增强的for循环。

![图片](F:\gitproject\demo\开发文档资料\images\java\while循环-01.png)

```java 
		int i=0;
		int sum=0;
		while(i<=100){
			sum +=i;
			System.out.println(i+"=="+sum);
            i++;
		}
```

 ![do...while循环图片](F:\gitproject\demo\开发文档资料\images\java\dowhile-01.png)

```java
    int i=0;
    int sum=0;
    do{
        sum =sum+i;
        i++;
    }while(i<=100);
    System.out.println(sum);
```

* for 循环

  ```java
  		//联系1，计算0-100之间的奇数和偶数的和
  		int jsum=0;
  		int osum=0;
  		
  		for(int i=0;i<=100;i++){
  			if(i%2 !=0){
  				jsum +=i;
  			}
  			if(i%2 ==0){
  				osum +=i;
  			}
  			
  		}
  		System.out.println("奇数和是="+jsum+"偶数和是="+osum+"总和是="+(jsum+osum));
  
  
  
  		//打印三角形
  		for(int i=1;i<=5;i++){
  			for(int j=5;j>=i;j--){
  				System.out.print(" ");
  			}
  			for(int j=1;j<=i;j++){
  				System.out.print("*");
  			}
  			for(int j=1;j<i;j++){
  				System.out.print("*");
  			}
  			System.out.println();
  		}
  		
  ```

* 增强for循环

  ```java
  
  ```

* brean contione

  ```java
  
  ```

  

## 11.方法



​	![图片](F:\gitproject\demo\开发文档资料\images\java\方法重载-01.png)

### 1.重载

​		

```
	public  int sums(int a,int b){
		return a+b;
	}
	public  int sums(int a,int b,int c){
		return a+b+c;
	}
```



### 2.可变参数

* JDK 1.5开始，java 支持传递同类型的可变参数给一个方法
* 在方法声明中，在指定参数类型后加一个省略号(...).
* 一个方法中只能指定一个可变参数，它必须是方法的最后一个参数。任何普通的参数必须在它之前声明。

​	

​	![图片](F:\gitproject\demo\开发文档资料\images\java\可变参数-01.png)



​	



## 12.数组

	### 1.数组概述

 * 相同数据类型数据的有序集合

   

### 2.数组声明  创建

​	![图片](F:\gitproject\demo\开发文档资料\images\java\数组声明-01.png)



```java 
    int[] unms;  //数组声明
    unms =  new int[3]; //数组创建
    int [] nums =new int [10];  // 简写
    unms[0]=1;
    unms[1]=2;
    unms[2]=3;
    //System.out.println(unms[2]);
    int sum =0;
    for(int i=0;i<unms.length;i++){
        sum = sum+unms[i];
    }
    System.out.println(sum);
```

* 内存分析

  ![图片](F:\gitproject\demo\开发文档资料\images\java\内存分析-01.png)

* 初始化数组

  ![图片](F:\gitproject\demo\开发文档资料\images\java\数组声明-01.png)

  

* 数组的基本特点

  1. **其长度是确定的。数组一旦被创建，它的大小就是不可改变的。**
  2. **其元素必须是相同类型，不允许出现混合类型，**
  3. **数组中的元素可以是任何数据类型，包括基本数据类型和引用数据类型。**
  4. **数组变量属性引用数据类型，数组也可以看成是对象。数组中的每一个元素相当于该对象的成员变量。数组本身就是对象，java中的对象就是在堆中的。**

  

### 3.数组使用

```java
		//查询显示最大数
		int [] arrays ={91,2,34,4,9};
		int  max= arrays[0];
		System.out.println("=="+max);
		for(int i=1;i<arrays.length;i++){
			if(arrays[i] > max){
				max =arrays[i];
			}
		}
		System.out.println("最大数是："+max);
```



```
public static void main(String[] args) {
		
		int [] arrays ={91,2,34,4,9};
		//打印数组
		Test test=new Test();
		//test.printArray(arrays);
		//printArrays(arrays);
		int [] rever = revers(arrays);
		test.printArray(rever);
	}
	//打印数组1
	public void printArray(int [] arrays){
		for(int i=0;i<arrays.length;i++){
			System.out.println(arrays[i]);
		}
	}
	//打印数组 2
	public static void printArrays(int [] arrays){
		for(int arr:arrays){
			System.out.println(arr);
		}
	}
	//翻转数组
	public static int [] revers(int [] arrays){
		int [] revers=new int [arrays.length];
		for(int i=0,j=revers.length-1;i< arrays.length;i++,j--){
		   revers[j]=arrays[i];
		}
		return revers;
	}
```



### 4.多维数组

### 5.Arrays 类

### 6.稀疏数组



## 13. java 面向对象

### 1. 什么是面向对象

![图片](F:\gitproject\demo\开发文档资料\images\java\面向对象01.png)



![图片02](F:\gitproject\demo\开发文档资料\images\java\面向对象02.png)

### 2.构造器





## 14.封装

​	![图片](F:\gitproject\demo\开发文档资料\images\java\封装01.png)



## 15.继承

 ![图片](F:\gitproject\demo\开发文档资料\images\java\继承01.png)



	### 1.supper注意点

* supper 调用父类的构造方法，必须在构造方法的第一个
* supper 必须只能出现在子类的方法或构造方法中
* supper 和 this 不能同时调用构造方法



### 2.this:

* 代表对象不同：
  1. this :本身调用这个对象
  2. supper : 代表父类对象应用
* 前提
  1. this : 没有继承也可以使用
  2. supper : 只能在继承条件下才能使用
* 构造方法
  1. this() : 本类的构造
  2. supper(): 父类的构造







## 16.重写

### 1. 注解

*  重写是方法的重写，和属性无关。

* 需要有继承关系，子类重写父类的方法

  1. 方法名必须相同
  2. 参数列表必须相同
  3. 修饰符： 范围可以扩大不能缩小，
  4. 抛出的异常：范围，可以被缩小，但不能扩大。

* 快捷键

  ​	Alt + Insert

## 17.多态

### 1.多态

 ![图片](F:\gitproject\demo\开发文档资料\images\java\多态01.png)

### 2. 多态注意事项

* 多态是方法的多态，属性没有多态
* 父类和子类，有联系，类型转换异常！
* 存在条件：继承关系，方法需要重写，父类引用指向子类对象！ father  f1 =new son()
  1. static 方法 属于类，它不属于实例。
  2. final  常量
  3. private 方法：

## 18.接口

![图片](F:\gitproject\demo\开发文档资料\images\java\接口01.png)











































# 三 java多线程

## 1 .







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

* 插件

  ![插件安装](F:\gitproject\demo\开发文档资料\images\Vscode-01.png)



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

* 遇到问题没有Python的环境

  1. 之前没有装过这个 python，而且要求是 2.7 版本 。

  2. 自己来安装吧。给Path添加两个环境变量。

     

  ```java
  C:\Python27
  C:\Python27\Scripts
  ```

* node-sass报错

  ```java
  npm ERR! node-sass@4.9.0 postinstall: `node scripts/build.js`
  npm ERR! Exit status 1
  npm ERR!
  npm ERR! Failed at the node-sass@4.9.0 postinstall script.
  npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
  ```

* 解决办法是，先删除 ，再安装 。

  ```
  npm uninstall node-sass
  npm install node-sass
  
  npm run dev 的正常结果
  ```

  


## 3. Es6(入门)

### 1.快捷键

* 新建页面快捷键(快速生成html模板页)

  ```jav 
  Shift + !    
  ```



### 2.变量声明

* let使用

* 对象属性简写：

  ```javascript
  var json={"name":name,"age":age}
  var json={name,age
  
  //获取数组
  let arr =[1,2,3];
  let [a,b,c] = arr;
  console.log(a,b,c);
  
  //对象
  const person ={
           name : "zzy",
           age: 13,
           language:['java','js','css']
  
      }
      //对象解构  
      const {name:abc,age,language} = person;
      console.log(name,age,language);
  
  
  
  ```
  
* 对象扩展

  ```javascript
  let str ="Hello Word";
  console.log(str.startsWith("Hello"));  
  console.log(str.endsWith("rd"));  
  console.log(str.includes("llo"));  
  ```

* 字符串模板

  ```javasc
  //字符串模板
     let ss =`<div>
                  <span>dfkjfks</span>
              </div>
              `
      console.log(ss);
  ```

  

* 字符串插入变量表达式。变量名写在${} 中，

  ```javascript
  let  names='今天';
  function run(){
      return "你好";
  }
  let info =`我叫,${names},我说${run()}`
  console.log(info)
  ```

## 3. 函数

 ### 1.使用

```javascript
//在Es6 以前，我们无法给一个函数参数设置默认值，只能采用变通的写法。
function add(a,b){
    //判断b 是否为空，为空就给默认值
    b =b || 1;
    return a +b ;
}
console.log(add(3));

//现在可以这么写 直接给参数写上默认值，没传就自动使用默认值
function add4(a,b=1){
    return a + b;
}
console.log(add4(2))

//不定参数
function fun(... values){
    console.log(values.length)
}
fun(1,2,4)
fun(1)


//箭头函数
var sum =function (a,b){
    return a +b;
}

var sum2 =(a,b) => a+b;

console.log(sum2(1,2));

```



### 2.对象函数属性简写

```javascript
  let persion ={
      name :'测试',
      //以前
      eat: function(food){
          console.log(this.name+"在吃"+food);
      },
      //箭头函数不能有this
      eat2:food =>console.log(persion.name+"在吃"+food),

      eat3 (food){
          console.log(this.name+"在吃"+food);
      }
  }

persion.eat("烧烤");
persion.eat2("火锅");
persion.eat3("水果");



//数组中新增了map 和 reduce 方法
//map();接受一个函数,将原来数组中的所有元素用这个函数处理后放入新数组返回；
let  arr =[1,4,5,6];
arr =arr.map((item) =>{
    return item *2;
})

//简写 
arr =arr.map(item => item * 2);
console.log(arr);



//reduce() 为数组中的每一个元素依次执行回调的函数，不包含数组中呗删除或从未被复制的元素
        /**
        1.previousValue(上次调用回调返回的值，或者是提供的初始值(initialValue))
        2.currentvalue (数组中当前被处理的元素)
        3.index （当前元素在数组中的索引）
        4.array (调用reduce 的数组)
        */
        let arr = [1,3,45,5];
        let result =arr.reduce((a,b) =>{
            console.log("上次处理后:"+a);
            console.log("当前处理: "+b);
            return a +b;
        },100)
        console.log(result)
```



### 3.Promise  使用

```javascript
  //1.查处当前用户信息
        //2.按照当前用户id 查处它的课程
        //3.按照课程id 查出来分出
   

        //1.promise 可以封装异步操作
        // let p = new Promise((resolve,reject)=>{
        //     //1.异步操作
        //     $.ajax({
        //           url:"mock/user.json",
        //           success:function(data){
        //               console.log("查询用户信息成功",data)
        //                 resolve(data);
        //           },
        //           error:function(err){
        //                 reject(err);
        //           }  

        //     })
        // });
        // p.then((obj)=>{
        //     return new Promise((resolve,reject)=>{

        //    $.ajax({
        //        url:`mock/user_corse_${obj.id}.json`,
        //        success:function(data){
        //            console.log("查询课程成功",data);
        //            resolve(data);
        //        },
        //        error(err){
                   
        //        }
        //    })
        // })
        // }).then((data)=>{
        //     console.log("上一步结构是"+data);
        //     $.ajax({
        //        url:`mock/corse_score_${data.id}.json`,
        //        success:function(data){
        //            console.log("查询课程成功",data);
                  
        //        },
        //        error(err){
                   
        //        }
        //    })
        // });





        function get(url,data){
           return  new Promise((resolve,reject)=>{
             $.ajax({
                url:url,
                success:function(data){
                    resolve(data);
                },
                error:function(err){
                    reject(err);
                }
             })
            });
        }

        get("mock/user.json")
        .then((data)=>{
            console.log("用户查询成功111",data)
            return get(`mock/user_corse_${data.id}.json`);
        })
        .then((data)=>{
            console.log("课程查询成功111",data);
            return get(`mock/corse_score_${data.id}.json`)
        })
        .then((data)=>{
            console.log("课程成绩查询成功11",data)
        })
        .catch((err)=>{
            console.log("异常")
        })


```



### 4.模块化

* 导入导出

  ```javascript
  //导出
  const util={
      sum(a,b){
          return a +b;
      }
  }
  
  export {util}
  
  //导入
  inport  util from  "./xxx.js"
  ```

  



# 六十五 Vue2 

## 1.Vue2 入门安装

```java
# 1.初始化项目
 $ npm init -y
# 2.安装vue 依赖
 $ npm install vue
```













































































# 七十 Git 基础

## 1. 密钥 

* 生成RSA密钥对

```
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

  

# 一一零 Redis 安装配置

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

## 3.配置Redis 持久化

```javascript
1.查看挂载路径 【root】# pwd
2.修改配置文件 【root】# vi redi.conf 
3.如下图【root】# appendonly yew
```

![图片](F:\gitproject\demo\开发文档资料\images\redis-02.png)





# 一二零 Mysql 配置

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



# 一三零 ElasticSearch

## 1. ElasticSearch 课程简介

 * 版本ElasticSearch 7.6.1

 * 6.X  7.x 的区别十分大，6.x 的API(原生API,RestFul 高级)

   

***

> wo

