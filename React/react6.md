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


## 选项卡例子

五个文件
- index.js
- Select.js
- Tab1.js
- Tab2.js
- Tab3.js

## index.js

```
import React from 'react';
import ReactDOM from 'react-dom';//只在入口用一次

import Select from './Select.js'
RenderDOM.render(
  <Select/>,document.getElementById('box')
  )
```

## Select.js

```
import React from 'react';
import Tab1 from './Tab1'
import Tab2 from './Tab2'
import Tab3 from './Tab3'

class SelectBar extends React.Component{
  constructor(){
    super();
    this.state={
      show:0
    }
  }
  handleClick(num){
    console.log(num)
    this.setState({show:num})  //根据传进来的参数修改当前的状态
  }
  render(){
    return(
      <div>
        <button onClick={this.handleClick.bind(this,0)}>选项卡一</button>
      {/*this,0其中的0 是给handleClick(num)传的参数*/}
        <button onClick={this.handleClick.bind(this,1)}>选项卡二</button>
        <button onClick={this.handleClick.bind(this,2)}>选项卡三</button>
        <br/>
        {this.state.show===0?<Tab1/>:  //这个意思就是如果当前state下show这个属性值是0，则
                                        下面显示Tab1的内容，如果是1，显示Tab2的内容
          this.state.show===1?<Tab2/>:
          <Tab3/>
        }
      </div>
    )
  }
}
export default SelectBar;
```

### Tab1.js

```
import React from 'react';

class Tab1 extends React.Component{
  render(){
    return(
      <div>
        <p>商品</p>
        <p>电脑</p>
        <p>家具</p>
        <p>衣服</p>
      </div>
    )
  }
}
export default Tab1;
```

其他几个Tab跟这个是一样的



###  过渡Transition 在react中的一个体现，可以参考阮一峰的个人网站  
### http://www.ruanyifeng.com/home.html 查看效果，点击黑色三角按钮的效果

还是新建文件
- index.js
- Trans.js
- main.css  根据自己的布局去写样式，这里就不详细说了

index.js里面的东西仍然是那些，参考以上写的即可

Trans.js

```
import React from 'react';

class Trans extends React.Component{
  constructor(){
    super();
    this.state={
      //展示就是true
      show:true
    }
  }
  handleClick(){
    this.setState({show:!this.state.show})
  }
  render(){
    let styles={
      top:this.state.show?'30%':'5%',
      height:this.state.show?'100px':'20px'
    }
      return(
          <div className='container' style={styles}>
            <button className='btn' onClick={this.handleClick.bind(this)}>{this.state.show?'上':'下'}</button>
            <h3>今天天气不错</h3><hr/>
            <h3>一起出去玩吧</h3>
          </div>
      )
  }
}
export default Trans;
```


这就是今天讲的一些例子，好好看一下，斟酌斟酌，体会这个state状态的意思
