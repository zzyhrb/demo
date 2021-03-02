##  Es6(入门)

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

  