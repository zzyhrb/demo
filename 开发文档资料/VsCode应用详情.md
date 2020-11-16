

# [第一次运行前端项目](https://www.cnblogs.com/wuyicode/p/13143424.html)



首先node 和 npm 环境就不说了，是肯定准备好了的。

 

比如 renren-fast-vue 这个开源项目，clone 下来后，就会做 npm install，让它下载 package.json 文件的各个 module。

通常会遇到的问题如下。

 

### 1、没有Python的环境

之前没有装过这个 python，而且要求是 2.7 版本 。

自己来安装吧。给Path添加两个环境变量。

```
C:\Python27
C:\Python27\Scripts
```

 

### 2、node-sass报错

```
npm ERR! node-sass@4.9.0 postinstall: `node scripts/build.js`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the node-sass@4.9.0 postinstall script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
```

解决办法是，先删除 ，再安装 。

```
npm uninstall node-sass
npm install node-sass
```

 

### 3、windows的编译环境问题

```
#npm install# MSBUILD : error MSB4132: 无法识别工具版本“2.0”。可用的工具版本为 "4.0"。
```

解决办法是，自己去下载安装 Visual C++ 2015 Build Tools 这个工具。再去执行 npm install --msvs_version 2015。

这个步骤，做好后，我重启了电脑。

 

成功的结果

PS D:\appdev\www\atguigu\renren-fast-vue> npm install
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.9 (node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.9: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})

```

```

up to date in 8.703s

```

```

 

npm run dev 的正常结果