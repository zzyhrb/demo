# Vue2 

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

  

