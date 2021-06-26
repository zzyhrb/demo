# 数据可视化项目搭建

## 一 .前端项目准备

	### 1.脚手架创建项目

 * 在全局环境中安装 vue-cli 脚手架

   ``` vue
   npm install  @vue/cli -g
   ```

* 工程创建

  ``` vue
  vue create vision
  ```

* 具体的配置项如下：

  ![](F:\gitproject\demo\开发文档资料\images\数据可视化\01.png)

  ![](F:\gitproject\demo\开发文档资料\images\数据可视化\02.png)

  

  ![](F:\gitproject\demo\开发文档资料\images\数据可视化\03.png)

	### 2. 删除无关代码



* 修改 App.vue 中的代码,将布局和样式删除, 变成如下代码:

  ``` vue
  <template>
  <div id="app">
  <router-view/>
  </div>
  </template>
  <style lang="less">
  </style>
  ```

* 删除 components/HelloWorld.vue 这个文件

* 删除 views/About.vue 和 views/Home.vue 这两个文件

* 修改 router/index.js 中的代码,去除路由配置和 Home 组件导入的代码

  ```vue
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  Vue.use(VueRouter)
  const routes = []
  const router = new VueRouter({
  routes
  })
  export default router
  
  ```



### 3.静态资源引入

> 将静态文件放在/ public  根目录下

![](F:\gitproject\demo\开发文档资料\images\数据可视化\04.png)

### 4.项目基本配置

* 项目根目录想创建vue.config.js

``` js
// 使用vue-cli创建出来的vue工程, Webpack的配置是被隐藏起来了的
// 如果想覆盖Webpack中的默认配置,需要在项目的根路径下增加vue.config.js文件
module.exports = {
    devServer: {
    port: 8999, // 端口号的配置
    open: true // 自动打开浏览器
    }
}
```

 * 全局引入echarts.js  

   1. 在 index.html 中引入echarts.js 文件

      ![](F:\gitproject\demo\开发文档资料\images\数据可视化\05.png)



   2.挂载到 Vue 原型上

					* 在 src/main.js 文件中挂载
					* 由于在 index.html 中已经通过script标签引入了 echarts.js 文件夹, 故在 window 全局对象中是 存在 echarts 全局对象, 将其挂载到 Vue 的原型对象上

``` js
......
// 将全局echarts对象挂载到Vue的原型对象上
Vue.prototype.$echarts = window.echarts
......
```

3.  使用全局 echarts 对象

* 在其他组件中使用

  ``` js 
  this.$echarts
  ```

### 5.asios 封装与挂载

* 在 src/main.js 文件中配置 axios 并且挂载到Vue的原型对象上

``` js 
......
import axios from 'axios'
axios.defaults.baseURL = 'http://127.0.0.1:8888/api/'
// 将axios挂载到Vue的原型对象上
Vue.prototype.$http = axios
......

```

![](F:\gitproject\demo\开发文档资料\images\数据可视化\06.png)





## 二 单独组件开发

### 1. 商家销量统计（横向柱详图）

* 组件设计

  （1）在 src/components/ 目录下建立 Seller.vue , 这个组件是真实展示图表的组件

  * 给外层div增加类样式 com-container
  * 建立一个显示图表的div元素 
  * 给新增的这个div增加类样式 com-chart

``` vue
<!-- 显示商家销量统计的图表 -->
<template>
<div class="com-container">
Seller组件
<div class="com-chart"></div>
</div>
</template>
<script>
export default {
data () {
return {}
},
methods: {}
}
</script>
<style lang="less" scoped>
</style>

```

* 在 src/views/ 目录下建立 SellerPage.vue ,这个组件是对应于路由 /seller 而展示的
  * 给外层div元素增加样式 com-page 
  * 在 SellerPage 中引入 Seller 组件,并且注册和使用

``` vue
<!-- 这个组件是对应于路由规则中 /seller 这条路径的
在这个组件中,需要展示Seller.vue这个组件
Seller.vue才是真正显示图表的组件
-->
<template>
<div class="com-page">
<seller></seller>
</div>
</template>
<script>
import Seller from '@/components/Seller'
export default {
data () {
return {}
},
methods: {},
components: {
seller:Seller
}
}
</script>
<style lang='less' scoped>
</style>

```

* 增加路由规则, 在 src/router/index.js 文件中修改

``` js 
......
import SellerPage from '@/views/SellerPage'
......
const routes = [
{
path: '/sellerpage',
component: SellerPage
}
]
```

* 新建 src/assets/css/global.less 增加宽高样式 原则就是将所有的容器的宽度和高度设置为占满父容器

``` css
: 100%;
height: 100%;
padding: 0;
margin: 0;
overflow: hidden;
}
.com-page {
width: 100%;
height: 100%;
overflow: hidden;
}
.com-container {
width: 100%;
height: 100%;
overflow: hidden;
}
.com-chart {
width: 100%;
height: 100%;
overflow: hidden;
}

```

在 main.js 中引入样式

import './assets/css/global.less'









### 2.







