---
title: JSX语言
layout: linux
---

## JSX的使用
新建了一个文件之后，可以把之前配置的webpack文件配置都拷贝过来，也就是.babelrc  package.json   webpack.config.js   index.js(入口文件)拷贝过来即可,命令行输入

```
npm i
```


然后配置react    

找到http://babeljs.io/ 官网，往下翻，找到 JSX and Flow，命令行输入

```
npm install --save-dev babel-preset-react
```

之后配置.babelrc文件，添加react

> {
  "presets": ["env","react"]
}


注意每次配置文件之后，都要重新启动webpack，即npm run test2即可


之后在每个js文件中开头写上

> import React from 'react';
import ReactDOM from 'react-dom';

下面是JSX的例子

```
ReactDOM.render(       //render方法  就是把某个dom节点插入到指定的地方
   <div>hello</div>,   //这就是某个节点
   document.getElementById('box')//这就是指定的地方
 )
 let name='rachel';
 let age=18;
 let male=0;
 function fun(x,y){
   return x+y
 }
 class Fun{
   say(){
     return '明天要上课'
   }
 }
 let obj={
   name:'rachel',
   age:18,
   work:'engineer',
   say:function(){
     return '234'
   }
 }

 let a=<div>
   <h1>nihao,hahah</h1>
   <h1>今天真好</h1>  {/*我是注释*/}
   <h1 className='name'>{name}</h1>
   <h1>{age*4}</h1>
   <h1 className={male ? 'man' : 'lady'}>{male ? '男' : '女'}</h1>   {/*这里面可以写三目运算符，不可以写if判断语句*/}
   <h1>{fun(3,5)}</h1>{/*插入函数*/}
   <h1>{new Fun().say()}</h1>
   <h1>{obj.name} {obj.age} {obj.say()}</h1>
 </div>;

  ReactDOM.render(
   a,document.getElementById('box')
 )
```

### JSX(javascript xml)语法，允许我们在JS里直接去写标签
 其他的特点
 1.每一个标签必须有结束标签,像img这种标签，则需要写成<img src="" alt=""/>后面加一个/
 2.jsx元素必须包含在一个闭合的标签内，通常都是用一个<div></div>包含一下
 3.在div标签内如果要写注释的话需要这样写{/*我是注释*/}
 4.我们可以在jsx元素内嵌入变量用大括号包裹一下，比如{org}
 5.在jsx元素内如果要写class的话需要写成className  tabindex写成tabIndex， for写成htmlFor
 6.jsx语法会被编译通过React.creatElement()这个方法
