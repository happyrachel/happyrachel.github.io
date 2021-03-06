---
title: 发请求
layout: linux
---

浏览器一般发出两类请求：GET ，POST 。GET 用来获取数据，POST 用来修改服务器数据。 GET 请求主体通常为空，那么如果用 GET 请求传递参数到服务器呢？

案例：传递用户 id 到服务器

现在我想请求一个具体的用户，通常会发这样的请求

GET /users/12345
我们要解决的问题是：如何把 12345 传递给服务器。

先给出后台代码

```
index.js

const express =  require('express');
const app = express();
const cors = require('cors');
app.use(cors());


app.get('/users/:id', function(req, res){
  console.log(req.params.id)
})

app.listen(3000, function(){
  console.log('running on port 3000...');
});
```

后台运行

node index.js
启动服务器。

前台发出请求

使用 curl 来发出请求
```
curl -X GET localhost:3000/users/12345
```
这样，到后台终端 log 中，可以看到 12345 被打印出来了，表示后台以及手到了前台的参数。

### 结语

GET 请求因为不涉及到 HTTP 请求主体（ body ）部分，所以传参数都是通过 url 中嵌入 参数的方式实现的。当然嵌入方式并不唯一，另外一种常见的格式是通过查询字符串的形式，这种形式我们本课程不介绍了，在 haoqicat.com/http-with-peter 课程中会有介绍。
