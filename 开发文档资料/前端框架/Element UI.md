## Element UI 引言

> 官网地址

* https://element.eleme.cn/#/zh-CN

## 一安装ElementUI

> 通过vue 脚手架创建项目

```bash
vue-cli init webpack element(项目名可自定义  ) 

? Project name element # 
? Project description A Vue.js project
? Author zzy <634187436@qq.com>
? Vue build standalone      
? Install vue-router? (Y/n)   # 是否构建vue路由  输入Y
? Use ESLint to lint your code? (Y/n)  # n
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recommended) npm


```

> 切换到项目根目录下运行

```
npm start 或者 npm run dev
```

>   在vue 脚手架项目中安装element

``` bash
# 1。下载elementui 依赖
npm i element-ui -S
# 2.引入组件  在main.js 下添加引用
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);

```

> 总结

<font color="red">	注意:</font>

* 在eement-ui 中所有组件都是el-组件名
* 组件属性都是写在组件标签上的

