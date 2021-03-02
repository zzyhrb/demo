





























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















## 19. java8 Lambda  





































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
  
* 代码整理

  ```java
  Alt + Shift +F
  ```

* 自定义模板

  ```javascript
  {
      "Print to console": {
          "prefix": "vue",
          "body": [
              "<!-- $1 -->",
              "<template>",
              "<div class='$2'>$5</div>",
              "</template>",
              "",
              "<script>",
              "//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）",
              "//例如：import 《组件名称》 from '《组件路径》';",
              "",
              "export default {",
              "//import引入的组件需要注入到对象中才能使用",
              "components: {},",
              "data() {",
              "//这里存放数据",
              "return {",
              "",
              "};",
              "},",
              "//监听属性 类似于data概念",
              "computed: {},",
              "//监控data中的数据变化",
              "watch: {},",
              "//方法集合",
              "methods: {",
              "",
              "},",
              "//生命周期 - 创建完成（可以访问当前this实例）",
              "created() {",
              "",
              "},",
              "//生命周期 - 挂载完成（可以访问DOM元素）",
              "mounted() {",
              "",
              "},",
              "beforeCreate() {}, //生命周期 - 创建之前",
              "beforeMount() {}, //生命周期 - 挂载之前",
              "beforeUpdate() {}, //生命周期 - 更新之前",
              "updated() {}, //生命周期 - 更新之后",
              "beforeDestroy() {}, //生命周期 - 销毁之前",
              "destroyed() {}, //生命周期 - 销毁完成",
              "activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发",
              "}",
              "</script>",
              "<style scoped>",
              "//@import url($3); 引入公共css类",
              "$4",
              "</style>"
          ],
          "description": "生成vue模板"
      },
      "http-get请求": {
  	"prefix": "httpget",
  	"body": [
  		"this.\\$http({",
  		"url: this.\\$http.adornUrl(''),",
  		"method: 'get',",
  		"params: this.\\$http.adornParams({})",
  		"}).then(({ data }) => {",
  		"})"
  	],
  	"description": "httpGET请求"
      },
      "http-post请求": {
  	"prefix": "httppost",
  	"body": [
  		"this.\\$http({",
  		"url: this.\\$http.adornUrl(''),",
  		"method: 'post',",
  		"data: this.\\$http.adornData(data, false)",
  		"}).then(({ data }) => { });" 
  	],
  	"description": "httpPOST请求"
      }
  }
  ```

  

> Node Js 安装

* http://nodejs.cn/download/ 

```shell
C:\Users>node -v  # 查看版本号及是否安装完成
v14.0.0

C:\Users>npm -v   # 查看包管理器
6.14.4
```

> 淘宝镜像

```
npm install -g cnpm -registry=https://registry.npm.taobao.org
```

> Babel 的使用

```bash
npm install -g babel-cli

cnpm install -g babel-cli  # 这个执行下载更快
```

>webpack 安装

```bash
npm install -g webpack webpack-cli  安装webpack 依赖
webpack -v  # 查看是否安装


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

 >总结：

* let 声明的变量不能重复
* const 声明变量不能修改

> 结构表达式

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
  console.log(str.startsWith("Hello"));  #判断以Hello 开始的 是返回true
  console.log(str.endsWith("rd"));    #判断以rd结束的 是返回true
  console.log(str.includes("llo"));  #是否包含llo 包含返回true
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

```js
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

=======================================================
    const persion ={
        name:"zy",
        age:18
    }

// function hello(persion){
//     console.log(persion.name)
// }

var hello2 =({name})=>console.log(name);

hello2(persion);
```

> 对象优化















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
=============================================================
    1.拷贝对象
    let p1={name:"Amy",age:15}
    let someone={...p1}
    consone.log(someone) // {name:"Amy",age:15}
=====================================================
        
        const persion ={
                name:"zy",
                age:18,
                language:['java','js','css']
        }

        console.log(Object.keys(persion)); //["name", "age", "language"]
        console.log(Object.values(persion)); //["zy", 18, Array(3)]
        console.log(Object.entries(persion)); //[Array(2), Array(2), Array(2)]
      
     
        //对象合并
        const target ={a:1}
        const source1 ={b:2}
        const source2 ={c:3}

        Object .assign(target,source1,source2)
        console.log(target)
================================================
    


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

## 2. Vue 声明式渲染

```javascript
<div id="box">
    <h1> {{name}},你好</h1>
</div>
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    let vm =new Vue({
        el:"#box",
        data:{
            name:"测试"
        }
    });
</script>


//2.双向绑定
 <div id="box">
        <input type="text" v-model="num">
        <h1> {{name}},你好。有{{num}}个人点赞</h1>
    </div>

    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        let vm =new Vue({
            el:"#box",
            data:{
                name:"测试",
                num:1
            }
        });
//指令（v-on:）
<div id="box">
        <input type="text" v-model="num">
        <button v-on:click="num++">点赞</button>
        <h1> {{name}},你好。有{{num}}个人点赞</h1>
    </div>

    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        let vm =new Vue({
            el:"#box",
            data:{
                name:"测试",
                num:1
            }
        });

```

## 3.指令

### 1.v-text  and v-html

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        {{msg}}
        <span v-html="msg"></span>
        <span v-text="msg"></span>
    </div>
    <script src="../../../node_modules/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                msg:"<h1>Hello Word</h1>"
            }
        })
    </script>
</body>
</html>
```

### 2.v-bind

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=\, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id="app">
        <a v-bind:href="link">go</a>
        <span v-bind:class="{active:isActive,'text-danger':hasError}"
        v-bind:style="{color:color1,fontSize:size}">你好</span>
    </div>

    <script src="../dist/vue.js">go</script>
    <script>
      let nm = new Vue({
            el:"#app",
            data:{
                link:"http://www.baidu.com",
                isActive:true,
                hasError:true,
                color1:'red',
                size:'80px'
            }
        })

    </script>
</body>
</html>
```

### 3.v-model

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>


    <!--表单项，自定义组件-->
    <div id="app">
        精通的语言:
        <input type="checkbox" v-model="lange" value="java">java<br />
        <input type="checkbox" v-model="lange" value="python">python<br />
        <input type="checkbox" v-model="lange"  value="C++"> C++ <br />
        选择了{{lange.join(",")}}

    </div>

    <script src="../dist/vue.js"></script>
    <script>
        let vm =new Vue({
            el:'#app',
            data:{
                lange:[]
            }
        })

    </script>
</body>
</html>
```



### 4.v-on

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">

        <button v-on:click="num++">点赞</button>
        <button @click="remove">取消点赞</button>
        <h1>有{{num}}个赞</h1>

        <!--事件修饰符-->
        <div style="border: 1px solid red;padding:20px;" v-on:click="hello">
            <div style="border: 1px solid blue;padding:20px;" @click,stop="hello">
                <a href="http://www.baidu.com" @click.prevent.stop="hello">go百度</a>
            </div>
        </div>


        <!--按键修饰符:-->
        <input type="text" v-model="num" v-on:keyup.up="num+=1" v-on:keyup.down="num-=1" @click.ctrl="num=10">
    </div>


    <script src="../dist/vue.js"></script>
    <script>
         let vm =new Vue({
            el:'#app',
            data:{
                num:1
            },
            methods:{
                remove(){
                    vm.num--;
                },
                hello(){
                    alert("hello");
                }
            }

         })

    </script>
</body>
</html>
```



### 5.v-for

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
  
    <div id="app">
        <ul>
            <li v-for="(user,index) in users">
                    当前索引:{{index}}==>>{{user.name}}==>>{{user.gender}}==>>{{user.age}}
                    <br />
                    对象信息:
                    <span v-for="(v,k,i) in user">{{k}}=={{v}}=={{i}}</span>

            </li>
        </ul>

    </div>
    

    <script src="../dist/vue.js"></script>
    <script>
        let vm =new Vue({
            el:"#app",
            data:{
                users:[{name:'刘德华',gender:'女',age:21},
                {name:'刘德华0',gender:'女1',age:21},
                {name:'刘德华1',gender:'女2',age:21},
                {name:'刘德华2',gender:'女3',age:21},
                {name:'刘德华3',gender:'女4',age:21}]
            }

        })

    </script>
</body>
</html>
```



### 6.v-if and v-show

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!---
        v-if   故名思意，条件判断，当得到结果为ture 时，所在的元素才会渲染
        v-show 当得到的结果为true 时，所在的元素才会呗显示。
    -->
    <div id="app">
        <button v-on:click="show = !show">点我啊</button>
        <button v-on:click="random=Math.random()">随机数</button>
        <!--使用if 显示-->
        <h1 v-if="show">if ===ok.....</h1>
        <!--使用show 显示-->
        <h1 v-show="show">show -===ok</h1>


        <span>{{random}}</span>
        <h1 v-if="random>=0.75">是我！！&gt;=0.75</h1>

        <h1 v-else-if="random>=0.5">是我！！&gt;=0.5</h1>

        <h1 v-else="random>=0.2">是我！！&gt;=0.2</h1>







    </div>

    <script src="../dist/vue.js"></script>
    <script>
        let vm = new Vue({
            el: "#app",
            data: {
                show: true,
                random: 1
            }


        })

    </script>
</body>

</html>
```

## 4.计算属性 和侦听器

### 1.过滤器

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <ul>
            <li v-for="(user,index) in users">
                当前索引:{{index}}==>>{{user.name}}==>>==>>{{user.id}}==>>
                {{user.gender | gendegFilter}}==>>{{user.gender | gFilter}}
        </li>

        </ul>

    </div>


    <script src="../dist/vue.js"></script>

    <script>
        //全局过滤器
        Vue.filter("gFilter",function(val){
            if(val ==1){
                return "男";
            }else{
                return "女";
            }
        })


        let vm= new Vue({
            el:"#app",
            data:{
                users:[
                    {id:1,name:'jack',gender:0},
                    {id:2,name:'刘德华1',gender:1}
                ]
            },
            filters:{
                    //局部过滤器
                    gendegFilter(val){
                        if(val==1){
                            return "男";
                        }else{
                            return "女";
                        }
                    }
                }
        })

    </script>
</body>
</html>
```

### 2.计算属性和侦听器

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <ul>
            <li>西游记: 价格:{{xyjg}} ,数量{{xysl}} <input type="number" v-model="xysl"></li>
            <li>水浒传: 价格:{{shjg}} ,数量{{shsl}} <input type="number" v-model="shsl"></li>
            <li>总价:{{total}}</li>
        </ul>
        {{msg}}
    </div>
    <script src="../dist/vue.js"></script>
    <script>

        let vm = new Vue({
            el:"#app",
            data:{
                xyjg:10,
                shjg:20,
                xysl:1,
                shsl:1,
                msg:""
            },
            computed: {
                total :function(){
                    return this.xyjg*this.xysl+this.shjg*this.shsl
                }
            },
            watch: {
                xysl: function(newVal,oldVal){
                    if(newVal >=3){
                        this.msg="库存超出限值";
                        this.xysl=3;
                    }else{
                        this.msg=''
                    }
                }
            },  

        })

    </script>
</body>

</html>
```

### 3.组件化

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id="app">
        <button v-on:click="count++">点击了{{count}}次</button>

        <!--全局组件-->
        <counter></counter>

        <!--局部组件-->
        <button-conter></button-conter>
    </div>
   
    <script src="../dist/vue.js"></script>
    <script>
        //全局组件
        Vue.component("counter",{
            template:'<button v-on:click="count++">点击了{{count}}次</button>',
            data(){
                return {
                    count:1
                }
            }
        })

        //局部组件
        const buttonCounter ={
            template:'<button v-on:click="count++">点击了{{count}}次</button>',
            data(){
                return {
                    count:1
                }
            }
        }

        let vm =new Vue({
            el:"#app",
            data:{
                count:1
            },
            components:{
                'button-conter':buttonCounter
            }

        })
    </script>
</body>
</html>
```

## 5.声明周期和钩子函数

### 1.生命周期

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <span id="num">{{num}}</span>
        <button @click="num++">赞！！</button>
        <h2>{{name}},有{{num}}个人点赞</h2>

    </div>

    <script src="../dist/vue.js"></script>
    <script>
        let vm=new  Vue({
            el:"#app",
            data:{
                name:'张三',
                num:100
            },
            methods: {
                show(){
                    return this.name;
                },
                add(){
                    this.num++;
                }
            },
            beforeCreate() {
                console.log("===========beforeCreate==========");
                console.log("数据模型未加载:"+this.name,this.num);
                console.log("方法未加载:"+this.show());
                console.log("html模块未加载:"+document.getElementById("num"))

            },
            created:function(){
                console.log("=============created=========");
                console.log("数据模型已加载:"+this.name,this.num);
                console.log("方法已加载:"+this.show());
                console.log("html模板已加载:"+document.getElementById("num"));
                console.log("html模板未渲染:"+document.getElementById("num").innerText)
            },
            beforeMount() {
                console.log("=========beforeMount==========");
                console.log("html模板未渲染:"+document.getElementById("num").innerText);
            },
            mounted() {
                console.log("==========mounted==========");
                console.log("html模板已渲染:"+document.getElementById("num".innerText));

            },
            beforeUpdate() {
                console.log("=====beforeUpdate=====");
                console.log("数据模型已更新:"+this.num);
                console.log("html模板未更新:"+document.getElementById("num").innerText)
            },
            updated() {
                console.log("============updated===============");
                console.log("数据模型已更新:"+this.num);
                console.log("html模板已更新:"+document.getElementById("num").innerText)
            },

        })


    </script>

</body>
</html>
```



## 二.事件绑定

### 1.父子组件传递数据

* 子组件给父组件传递数据，事件机制

* 子组件给父组件发送一个事件携带数据

  ```java
  //向父组件发送事件
  this.$emit("tree-node-click",data,node,comment);
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

## 3.[Centos7中yum安装jdk及配置环境变量](https://www.cnblogs.com/52lxl-top/p/9877202.html)

```javascript
系统版本

[root@localhost ~]# cat /etc/redhat-release 
CentOS Linux release 7.4.1708 (Core) 
#安装之前先查看一下有无系统自带jdk

rpm -qa |grep java

rpm -qa |grep jdk

rpm -qa |grep gcj
#如果有就使用批量卸载命令

rpm -qa | grep java | xargs rpm -e --nodeps 
 

直接yum安装1.8.0版本openjdk

[root@localhost ~]# yum install java-1.8.0-openjdk* -y
查看版本

[root@localhost ~]# java -version
openjdk version "1.8.0_161"
OpenJDK Runtime Environment (build 1.8.0_161-b14)
OpenJDK 64-Bit Server VM (build 25.161-b14, mixed mode)
默认jre jdk 安装路径是/usr/lib/jvm 下面



 

JAVA_HOME指向一个含有java可执行程序的目录(一般是在 bin/java中,此目录为/bin/java的上级目录),用cd 命令进入到 jvm下唯一的一个目录中 java-1.8.0-openjdk-1.8.0.161-0.b14.el7_3.x86_64,发现其下目录为 

/jar/bin/java.jre-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64 这个链接是指向 java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/jre 这个文件夹，所以，可以直接用export命令将 JAVA_HOME 指向
 jre-1.8.0-openjdk-1.8.0.121-0.b14.el7_4.x86_64这个链接.
 
#临时生效
[root@localhost ~]#  export JAVA_HOME=/usr/lib/jvm/<span style="font-family: Arial;">jre-1.8.0-openjdk-1.8.0.121-0.b13.el7_3.x86_64</span> 
#当前用户生效的配置

vim ~/.bashrc
#在文件底部加入下面一句
export  JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64
#如果使所有用户生效的配置

复制代码
vim /etc/profile
 #set java environment  

export JAVA_HOME=/usr/lib/jvm/java

export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/jre/lib/rt.jar

export PATH=$PATH:$JAVA_HOME/bin
复制代码
 

#使得配置生效

. /etc/profile
 

#查看变量

复制代码
[root@localhost ~]#  echo $JAVA_HOME  
/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64

 [root@localhost ~]# echo $CLASSPATH
.:/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/lib/dt.jar:/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/lib/tools.jar

复制代码
 javac 和java 命令都有输出设置提示就表示安装和环境配置成功了

案例如下：

[root@instanc]# yum -y list java  

Loaded plugins: langpacks, versionlock

Error: No matching Packages to list

[root@instanc]# rpm -qa |grep java

[root@instanc]# rpm -qa |grep jdk

[root@instanc]# rpm -qa |grep gcj

[root@instanc]# yum install java-1.8.0-openjdk* -y

--------中间有安装过程，最后complete

Complete!

[root@instance-ozyu8y37 ~]# java -version

openjdk version "1.8.0_191"

OpenJDK Runtime Environment (build 1.8.0_191-b12)

OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)

[root@instance-ozyu8y37 ~]# cd /usr

[root@instance-ozyu8y37 usr]# ls

bin  etc  games  include  lib  lib64  libexec  local  sbin  share  src  tmp

[root@instance-ozyu8y37 usr]# cd lib

[root@instance-ozyu8y37 lib]# cd jvm

[root@instance-ozyu8y37 jvm]# ls

java

java-1.8.0

java-1.8.0-openjdk

java-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64

java-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64-debug

java-openjdk

jre

jre-1.8.0

jre-1.8.0-openjdk

jre-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64

jre-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64-debug

jre-openjdk

[root@instance-ozyu8y37 jvm]# vim /etc/profile   # 配置java环境变量（所有用户）

# System wide environment and startup programs, for login setup

# Functions and aliases go in /etc/bashrc

 

# It's NOT a good idea to change this file unless you know what you

# are doing. It's much better to create a custom.sh shell script in

# /etc/profile.d/ to make custom changes to your environment, as this

# will prevent the need for merging in future updates.

 

pathmunge () {

    case ":${PATH}:" in

        *:"$1":*)

            ;;

        *)

            if [ "$2" = "after" ] ; then

                PATH=$PATH:$1

            else

                PATH=$1:$PATH

            fi

    esac

}

 

 

if [ -x /usr/bin/id ]; then

    if [ -z "$EUID" ]; then

        # ksh workaround

        EUID=`/usr/bin/id -u`

        UID=`/usr/bin/id -ru`

    fi

    USER="`/usr/bin/id -un`"

    LOGNAME=$USER

    MAIL="/var/spool/mail/$USER"

fi

#set java environment  

 

export JAVA_HOME=/usr/lib/jvm/java

 

export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/jre/lib/rt.jar

 

export PATH=$PATH:$JAVA_HOME/bin

 

# Path manipulation

if [ "$EUID" = "0" ]; then

    pathmunge /usr/sbin

    pathmunge /usr/local/sbin

else

    pathmunge /usr/local/sbin after

    pathmunge /usr/sbin after

fi

 

HOSTNAME=`/usr/bin/hostname 2>/dev/null`

HISTSIZE=1000

if [ "$HISTCONTROL" = "ignorespace" ] ; then

    export HISTCONTROL=ignoreboth

else

    export HISTCONTROL=ignoredups

fi

 

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

 

# By default, we want umask to get set. This sets it for login shell

# Current threshold for system reserved uid/gids is 200

# You could check uidgid reservation validity in

# /usr/share/doc/setup-*/uidgid file

if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then

    umask 002

else

    umask 022

fi

 

for i in /etc/profile.d/*.sh /etc/profile.d/sh.local ; do

    if [ -r "$i" ]; then

        if [ "${-#*i}" != "$-" ]; then 

            . "$i"

        else

            . "$i" >/dev/null

        fi

    fi

done

 

unset i

unset -f pathmunge

setterm -blank 0 &> /dev/null

setterm -powersave off &> /dev/null

setterm -powerdown 0 &> /dev/null

ulimit -SHn 65535

[root@instance-ozyu8y37 jvm]# . /etc/profile    #使配置生效

[root@instance-ozyu8y37 jvm]# java

Usage: java [-options] class [args...]

           (to execute a class)

   or  java [-options] -jar jarfile [args...]

           (to execute a jar file)

where options include:

    -d32   use a 32-bit data model if available

    -d64   use a 64-bit data model if available

    -server   to select the "server" VM

                  The default VM is server.

 

    -cp <class search path of directories and zip/jar files>

    -classpath <class search path of directories and zip/jar files>

                  A : separated list of directories, JAR archives,

                  and ZIP archives to search for class files.

    -D<name>=<value>

                  set a system property

    -verbose:[class|gc|jni]

                  enable verbose output

    -version      print product version and exit

    -version:<value>

                  Warning: this feature is deprecated and will be removed

                  in a future release.

                  require the specified version to run

    -showversion  print product version and continue

    -jre-restrict-search | -no-jre-restrict-search

                  Warning: this feature is deprecated and will be removed

                  in a future release.

                  include/exclude user private JREs in the version search

    -? -help      print this help message

    -X            print help on non-standard options

    -ea[:<packagename>...|:<classname>]

    -enableassertions[:<packagename>...|:<classname>]

                  enable assertions with specified granularity

    -da[:<packagename>...|:<classname>]

    -disableassertions[:<packagename>...|:<classname>]

                  disable assertions with specified granularity

    -esa | -enablesystemassertions

                  enable system assertions

    -dsa | -disablesystemassertions

                  disable system assertions

    -agentlib:<libname>[=<options>]

                  load native agent library <libname>, e.g. -agentlib:hprof

                  see also, -agentlib:jdwp=help and -agentlib:hprof=help

    -agentpath:<pathname>[=<options>]

                  load native agent library by full pathname

    -javaagent:<jarpath>[=<options>]

                  load Java programming language agent, see java.lang.instrument

    -splash:<imagepath>

                  show splash screen with specified image

See http://www.oracle.com/technetwork/java/javase/documentation/index.html for more details.

[root@instance-ozyu8y37 jvm]# javac

Usage: javac <options> <source files>

where possible options include:

  -g                         Generate all debugging info

  -g:none                    Generate no debugging info

  -g:{lines,vars,source}     Generate only some debugging info

  -nowarn                    Generate no warnings

  -verbose                   Output messages about what the compiler is doing

  -deprecation               Output source locations where deprecated APIs are used

  -classpath <path>          Specify where to find user class files and annotation processors

  -cp <path>                 Specify where to find user class files and annotation processors

  -sourcepath <path>         Specify where to find input source files

  -bootclasspath <path>      Override location of bootstrap class files

  -extdirs <dirs>            Override location of installed extensions

  -endorseddirs <dirs>       Override location of endorsed standards path

  -proc:{none,only}          Control whether annotation processing and/or compilation is done.

  -processor <class1>[,<class2>,<class3>...] Names of the annotation processors to run; bypasses default discovery process

  -processorpath <path>      Specify where to find annotation processors

  -parameters                Generate metadata for reflection on method parameters

  -d <directory>             Specify where to place generated class files

  -s <directory>             Specify where to place generated source files

  -h <directory>             Specify where to place generated native header files

  -implicit:{none,class}     Specify whether or not to generate class files for implicitly referenced files

  -encoding <encoding>       Specify character encoding used by source files

  -source <release>          Provide source compatibility with specified release

  -target <release>          Generate class files for specific VM version

  -profile <profile>         Check that API used is available in the specified profile

  -version                   Version information

  -help                      Print a synopsis of standard options

  -Akey[=value]              Options to pass to annotation processors

  -X                         Print a synopsis of nonstandard options

  -J<flag>                   Pass <flag> directly to the runtime system

  -Werror                    Terminate compilation if warnings occur

  @<filename>                Read options and filenames from file

 

至此jdk安装成功
```



## 4. 运行springboot 项目

```java


&代表在后台运行，使用ctrl+c不会中断程序的运行，但是关闭窗口会中断程序的运行。
三、nohup java -jar XXX.jar
    
&使用这种方式运行的程序日志会输出到当前目录下的nohup.out文件，使用ctrl+c中断或者关闭窗口都不会中断程序的执行。
四、nohup java -jar XXX.jar >temp.out &
    
五、停止项目
linux 只能通过杀死线程才能关闭某个程序，可以通过ps -ef | grep java 的方式查看运行的java项目

也可以通过pgrep -f 'java -jar demo-0.0.1-SNAPSHOT.jar'这种方式查看该项目的进程号

并使用kill -9 杀死进程号

```

![图片](F:\gitproject\demo\开发文档资料\images\java\linux发布1.png)











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





# 一五零 其他

### 1.win10 端口占用

```
1.查看端口只用情况
netstat -ano | findstr 端口号

2.执行此命令强制关闭指定进程号的进程
taskkill -PID 进程号 -F 
```

