---
title: React组件
layout: linux
---

## 组件（component）

定义一个组件有三种方式 首字母必须大写 自定义标签，可以包含一系列的标签

###第一种写法，1.React.createClass({})  基本不用这种写法基本不怎么使用

例子：

```
 let  Dom = React.createClass({
   render:function () {
     return(
       <div> aaaaa</div>
    )
   }
 });
 ReactDOM.render(
   <Dom/>,document.getElementById('box')
 )
```

###第二种写法

2.function Greeting(){    Greeting必须要首字母必须大写，这样react就知道这是你自己写的标签，而不是浏览器自带的标签
// return (<h1>aaa</h1>)   使用时是<Greeting/>自定义标签，function必须要有return，return()括号里面必须是一个标签dom结构
// }

例子

```
function Greeting(){
   return (<h1>hello</h1>)
 }
 ReactDOM.render(
   <Greeting/>,document.getElementById('box2')
 )
 ```

###第三种写法

3.class Welcome extends React.Component {
//   render() {
//     return (<h1>Hello, {this.props.name}</h1>)
//   }
// }

例子：

```
 class Welcome extends React.Component {
   render() {
     return (<h1>byebye</h1>)
   }
 }
 ReactDOM.render(
   <Welcome/>,document.getElementById('box3')
 )
```
