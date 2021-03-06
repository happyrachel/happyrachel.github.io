---
title: espress 基础
layout: linux
---

仅仅有了 API ，功能还不完全。需要有前端来调用 API ，完成 整个小功能。

在我们《JS 独孤求败》课程体系里面，前端代码我们都是用 React 来写， 所以前端和后端都是用 JS 来写。但是这里要提醒大家的是，前端和后端是 完全独立的两个项目，通过 API 来作为桥梁。其实，我们后端虽然是 Nodejs 写的，但是也可以用 PHP/JAVA 也能写。

### 前段准备工作

创建新的文件夹，cd到当前文件夹

npm init -y
npm i --save  webpack babel-core babel-preset-env babel-loader react react-dom babel-preset-react

这就搭建了基本的环境

src/index.js
```
import React, { Component } from 'react';
import ReactDOM from 'react-dom';


class App extends Component {
  constructor(){
    super();
    this.state = {
      username: ''
    };
  }
  componentWillMount() {
    this.setState({username: 'happypeter'});
  }
  render(){
    return(
      <div>
        {this.state.username}
      </div>
    )
  }
}

ReactDOM.render(<App/>,document.getElementById('app'));
```

package.json
```js
{
  "name": "react-frontend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "babel-core": "^6.23.1",
    "babel-loader": "^6.4.0",
    "babel-preset-env": "^1.2.1",
    "babel-preset-react": "^6.23.0",
    "react": "^15.4.2",
    "react-dom": "^15.4.2",
    "webpack": "^2.2.1"
  }
}
```
webpack.config.js
```js
var path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src/index.js'),
  output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader'
      }
    ]
  }
};
```

.babelrc

```
{
  "presets": ["env", "react"]
}
```
index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>

  <div id="app"></div>
  <script src="./build/bundle.js" charset="utf-8"></script>
</body>
</html>
```

### 安装http-server
前端代码其实最好也跑在一个 http 服务器之上，最简单的方法是：
```
npm install -g http-server
```

这样，我们就有了一个简单的系统工具叫 http-server

```
cd react-frontend/
http-server .
```
就能把我们的前端项目启动到一个 http 服务器上了。

### 实现API
开发一个功能，首先要写好后台的代码，也就是先实现API。下一步就是用curl这样的命令，测试一下API。
发现API没毛病之后在写前端的代码。

打开后台文件中的index.js文件，里面书写如下形式的API：

```
app.get('/username',function(req, res){
  res.send({username:'happyrachel'})
})
```

### 用curl来测试API
curl是安装在系统上的一个命令，可以用来发http请求

测试API，
```
curl -X GET  'http：//localhost：3000/username'
```

如果出现以下结果：
curl: (7) Failed to connect to localhost port 3000: 拒绝连接
说明你的后端没有启动，然后cd到后台文件夹，启动项目
```
nodemon index.js
```
启动之后在运行curl命令，则可以看到运行结果。

### 安装 axios 发送 http 请求
现在我们来到前端代码中。引入 axios 。axios 按照[官网](https://github.com/mzabriskie/axios)的说法，它是一个 http client （ http 的客户端），换句话说，它是专门用来发 http 请求的。

axios 是常用的发 http 请求的工具（现在一般不提发 ajax 请求这个说法了）。

首先来进行装包：

```
npm install --save axios
```
把 axios 安装到 react-frontend 这个项目中。

装包之后，就可以到 src/index.js 中去使用了，代码如下

```
import axios from 'axios';
```

我们当前的请求不希望是通过按钮来触发，而是希望，页面加载的时候，自动发出 http 请求，向服务要数据，所以，代码非常适合写到生命周期函数中：

```
componentWillMount() {
  axios.get('http://localhost:3000/username').then(function(response){
      return console.log(response);
    }
  )
}
```
代码进行到上面，浏览器中用前台请求后台，会在 chrome console 中看到，如下 错误：

```
XMLHttpRequest cannot load http://localhost:3000/.
No 'Access-Control-Allow-Origin' header is present on the requested resource.
Origin 'null' is therefore not allowed access.
```
这就是跨域请求的问题

### 跨域请求 Access-Control-Allow-Origin
XMLHttpRequest 是发 HTTP 请求的底层机制，是浏览器自带功能。上面的报错翻译如下：

```
无法加载后台 http://localhost:3000 .
被请求的资源中没有设置 Access-Control-Allow-Origin 头部。源头设置为 Null ，所以不允许
访问。
```
Access-Control-Allow-Origin 字面意思：访问控制允许来源。
服务器上的默认是不允许其他网址（或者网址相同，但是端口号不同）的网站请求资源的，
如果需要开通权限，就需要在服务器上做下面的设置。
```
Access-Control-Allow-Origin ：*
```

### 跨域请求的解决方案

解决方案采用： https://github.com/expressjs/cors

cors 是 Cross Origin Resource Share ，安装了这个包就可以完成

保证后台启动状态，现在我们看看当前后台资源的 header 设置，可以用下面的 curl 命令
```
$ curl -I http://localhost:3000/
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
Content-Length: 11
ETag: W/"b-sQqNsWTgdUEFt6mb5y4/5Q"
Date: Thu, 08 Dec 2016 01:51:44 GMT
Connection: keep-alive
```
curl 是专门用来测试 API 的一个命令行工具，-I 选项用来专门活动服务器 返回的 header 。
命令返回的信息，就是服务器端被请求资源的的 header 。
很明确是没有 Access-Control-Allow-Origin 这一项的。
下面我们安装 cors 这个包，就可以解决这个问题。

具体步骤如下：

到 https://www.npmjs.com/package/cors 可以看到装包命令如下：
```
npm install --save cors
```
再次提醒：这个包要安装到后台代码中。

在次通过curl -I http://localhost:3000/  命令，就可以看到
Access-Control-Allow-Origin: *
这一项了。


然后去后台的index.js文件中添加两行代码
```
const cors = require('cors')
app.use(cors());
```

下面进一步调整 componentWillMount 如下：
```
componentWillMount() {
    let _this=this;
    axios.get('http://localhost:3000/username').then(function(res){
       _this.setState({username:res.data.username})
      // return console.log(res.data.username);
    })
  }
```

前台再次重启前端，既可以看到对应的数据了。

### 总结
这样，前后端分离的架构我们就已经完成了。
