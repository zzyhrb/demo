# Vs code (基础篇)

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

  
