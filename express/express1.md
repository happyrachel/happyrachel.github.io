---
title: espress 基础
layout: linux
---

express就是一个后台（后端 back-end）框架。
express就是nodejs的一个框架，而且是node.js各种后台框架中最通用的。

nodejs是提供大家在服务器端运行javascript的可能，是js在后台运行的一种环境。

### express
express的官网是 http://www.expressjs.com.cn/
API （Application program interface）是**应用开发接口**，简称**接口** 。
Express 就是用来制作后台接口的，或者说叫制作后台 API 的.

那么之后，我们整个项目的架构，就是用 Express 来制作后台 API , 这些 API 的使用 者就是前台 React 代码。

### hello world
现在我们就动手来写一个最简单的 Express 小程序。

第一步，要新建文件夹，并把它初始化为一个 Nodejs 项目：
```
mkdir express-hello
cd express-hello
npm init -y
```
小贴士：一个常见装包错误，如果我们项目文件夹的名和要装的包名同名,是会出现报错信息，此时只需要修改文件夹的名字即可


### 补充知识

- 工具：就是完成特定的一个小功能的软件，比如 Babel
- 库： 英文叫 lib ，我们每天 import 的东西，都是库。库是把一系列相关工具，组织到一起。例如，lodash ，react 。库里面的东西虽然多，但是都是干一类工作的。
- 框架：英文是 framework ，是把很多类功能的工具和库集合到一起，目的是完成整个项目。 例如，RubyOnRails，react（这里react指的是react+friends，官网的react解释就是一个库）


这样 通过ls-a查看文件中是否生成了 package.json这个文件，有了这个文件，我们这个文件夹就可以 叫做一个 Nodejs 项目 了 。

用atom打开项目文件，创建
- index.js

### 写后台代码，用 ES6 ？

我们的前台代码，因为有 Babel 的支持，可以全部采用 ES6 来写。后台代码，我们会让它直接运行在 Nodejs 之上，不用 Babel （ 当然也可以用，但是配置比较麻烦，不值当的）。

如果我们到 Node.green 网站上，可以看到新版的 Nodejs (7.0 版本以上)对于 ES6 的支持已经到了99% 。所以， 不用 Babel 我们也可以直接使用 ES6 语法，但是唯一要 注意的就是不能用 import （ 也就是说 nodejs 是不支持 ES6 模块语法的），我们的后台代码暂时需要用 require 来替代 import 。require 用的是 commonjs 模块语法， 这个是 Nodejs 原生支持的。

最终结论：

```
ES6 可以用，别用 import 就好了。
```

到项目中，参考[官网教程](http://www.expressjs.com.cn/starter/hello-world.html)创建一个 index.js 文件，内容如下：

```
const express =  require('express');

let app = express();

app.listen(3000,function(){
  console.log('running on port 3000...');
});
```
之后在命令行中运行

```
node index.js
```

即输出一条语句  running on port 3000...
上面添加的无名函数 function(){...} 在这里 的作用是 **回调函数( callback function )** 。

### 小贴士：
什么是回调函数？ 回调函数是我们写 JS 程序，最常见的功能之一。程序会先执行一个操作， 执行完这个操作后，回过头来要调用的那个函数，就叫回调函数。
一般回调函数的使用场合就是，之前的一个操作耗时比较长（或者是异步操作） 这样的情况下才使用回调函数。

### Express 服务器运行起来了，so what ？
服务器监听端口后，唯一的作用就是来根据端口传入的请求，来执行特定代码。

比如，我们在上面的 index.js 中，app.listen 语句的上面，添加如下代码：

```
app.get('/title',function(){
  console.log('my title')
})
```
上面代码中 get('/title') 这是什么？
- get 是一个 http 请求的动词 ，类似的还有 post/delete/put 。
- /title 是一个路径 ，英文 path

一个动词加一个路径，这样就组成一个 HTTP 请求 ，公式如下
```
request = verb + path + data
```

但是，这里的请求，不是 **发出请求** ，而是 **接收请求** 。

### 现在来发客户端请求

可以发请求的方式不唯一，可以用浏览器地址栏，可以用页面的 form 发， 也可以用 axios 发，后者使用专门的 API 调试工具 curl/postman 来发。

Postman 是一个辅助工具，用它的目的就是美观方便。但是 Postman 需要 用到谷歌的服务，所以需要我们的机器可以翻墙才行。

小贴士：翻墙方式：

- 免费的：https://laod.cn
- Peter 自己用：https://agentwho.rocks 小贴士结束。
现在，我们就用浏览器的地址栏来发请求。地址栏中输入
```
http://localhost:3000/title
```

上的请求，默认动词就是 GET ，同时 :3000 用来指定端口号。

请求之后，会发现浏览器里没有任何输出，这是因为，我们的 express 服务器根本就没有给前台返回任何字符串，回调函数中的 console.log() 只能把字符串打印到后台。回到命令行就可以看到 输出了
```
my title
```
