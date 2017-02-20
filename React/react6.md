---
title: State  例子
layout: linux
---
## 咱们写一个关于State的例子，点击开始暂停，随机选取一个东西

比如一个今天吃什么的例子

仍然是新建几个文件
- index.js  作为入口文件
- EatWhat.js   写我们的小组件

### index.js的代码

```
import React from 'react';
import ReactDOM from 'react-dom';//只在入口用一次

import EatWhat from './EatWhat.js'
RenderDOM.render(
  <EatWhat/>,document.getElementById('box')
  )
```
### EatWhat.js的代码

```
import React from 'react';



let data=['白菜','巧克力','芒果','草莓','橙子','冰激凌']   //先定义一个数组，里面放需要不断改变的数据
class EatWhat extends React.Component{
  constructor(){
    super();
    this.state={
      start:false,
      data,       //因为属性值和属性名一样，所以可以写成属性值+,data表示的一个数组
      text:''     //这就是写的初始的状态
    }
  }
  select(){
  let result=this.state.data[Math.floor(Math.random()*this.state.data.length)]
  //定义一个result=从data里面随机抽取的一个数据
  this.setState({text:result})
  设置当年页面的状态变为选取的那个数据
  }
  handleClick(){
    if (this.state.start) {
      this.setState({start:false})
      clearInterval(this.interval)
      如果当前状态是true，则修改button为开始，然后关闭计时器
    } else {
      this.setState({start:true})
      点击button按钮之后，如果当前状态是false，则修改button为停止，然后开启计时器
      this.interval=setInterval(()=>this.select(),50);
    }
  }
  render(){
      return(
        <div>
          <p>今天吃什么:{this.state.text}</p>
          <br/>
          <button onClick={this.handleClick.bind(this)}>{this.state.start?'停止':'开始'}</button>
                                                        //这个意思就是如果此时的状态是true，则按钮显示的开始
                                                        如果此时状态是false，按钮现实的是停止
        </div>
      )
  }
}
export default EatWhat;
```
