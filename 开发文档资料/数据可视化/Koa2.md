#  KOA2的使用



## 1.KOA2的介绍



* 基于Node.js 平台的web 服务器框架



 



## 2.快速上手

* 检查Node环境

  node -v 

* 安装Koa 

​       npm init -y

​		npm install koa

* 创建并编写app.js

  > 创建koa 实例对象

 ```vue
// 1.创建koa对象
const Koa = require('koa') // 导入构造方法
const app = new Koa() // 通过构造方法, 创建实例对象
 ```

> 编写响应函数(中间件) 响应函数是通过use的方式才能产生效果,
>
>  这个函数有两个参数, 一个是 ctx ,一个是 next ctx : 上下文, 指的是请求所处于的Web容器,我们可以通过 ctx.request 拿到请求对象, 也可 以通过 ctx.response 拿到响应对象 next : 内层中间件执行的入口

``` vue 
// 2.编写响应函数(中间件)
app.use((ctx, next) => {
console.log(ctx.request.url)
ctx.response.body = 'hello world'
})
```

> 指明端口号  》通过 app.listen 就可以指明一个端口号

```  vue 
// 3.绑定端口号 3000
app.listen(3000)

```

> 启动服务器

```` vue 
node app.js 就可以启动服务器
````

