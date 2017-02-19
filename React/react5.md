---
title: 组件的状态
layout: linux
---

## 组件的状态State， State是组件内的状态  必须要通过setState才能修改页面的状态

代码：

```
import React from 'react';


class App extends React.Component{
  constructor(){            //给class  APP添加了自带属性，this.state就表示目前这个类的状态
    super();
    this.state={
      num:0,
      show:false
    }
  }
  handleAdd(){
    this.setState({num: this.state.num+1})
  }
  handleCut(){
    this.setState({
      num:this.state.num -1,
      show: !this.state.show})
  }
  render(){
      return(
        <div>
          数字是：{this.state.num}<br/>
          <button onClick={this.handleAdd.bind(this)}>+1</button>
          <button onClick={this.handleCut.bind(this)}>{this.state.show?'隐藏':'显示'}</button>
          <p style={{display:this.state.show?'block':'none'}}>显示</p>
        </div>
      )
  }
}
export default App;
```

在类里面写事件的时候，要写成  this.方法名.bind(this)

方法都在类中写明，例如以上代码中的

```
handleCut(){
  this.setState({属性名：属性值，属性名：属性值})
}
```
this.setState({})这里面写的是一个对象
this.state  在类里面任何地方都可以进行使用
