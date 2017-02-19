---
title: 组件的嵌套
layout: linux
---

## 组件的嵌套

一个大的工程都是由一个一个小小的组件构成的，今天学习的就是把一个页面分成一个一个的组件，然后嵌套起来，行程一个整体的页面

入口文件仍然是index.js，如果要修改入口文件，则去webpack.config.js中去修改output，然后重启webpack即可。

在src文件夹下面，新建几个js文件，分别为

- APP.js
- Header.js
- Banner.js
- Footer.js

一般头部都是由logo和登陆组成，所以在建两个js文件

- Logo.js
- SignIn.js

###首先写Header.js，其中代码如下

```
mport React from 'react';

import Logo from './Logo.js';   
import SignIn from './SignIn.js';

class Header extends React.Component{
  render(){
    return(
      <div className="clearfix">
        <Logo/>
        <SignIn/>
      </div>
    )
  }
}

export default Header;  //默认导出Header这个类
```

- 比如从Logo.js引入Logo这个类，其中文件的名字绝对不可以写错

###然后写Logo.js,代码如下

```
 import React from 'react';
 import img from './images/1.jpg'//先把图片当做一个js导入进来，这样img就成了一个变量



 class Logo extends React.Component{
   render(){
     let styles ={width:'100px',border:'3px solid #000',borderRadius:"50%"};
     //这是行内样式
     
     return(
       <div>
         <img src={img} style={styles}/>
       </div>
     )
   }
 }

 export default Logo;
 ```

 前面的大部分工作都在处理JS逻辑的解析和加载，但是我们还一直没有提我们的样式文件应该如何去处理。

 我们在课程中暂且约定使用less预处理器（saas的类似）来写我们项目的样式，那么首先需要下载几个webpack的loader

> npm install --save-dev style-loader css-loader less-loader

 然后进行配置webpack.config.js文件

```
output: {
  path:'build',
  filename:'bundle.js',
  publicPath: "build/"      //这一条是新添加的
},
 module: {
   rules: [
     { test: /\.js$/, exclude: /node_modules/, use: "babel-loader" },
     { test: /\.css/,use: ['style-loader','css-loader']},   //这是新增的
     { test: /\.(jpe?g|png)$/,use: 'file-loader'}     //这是新增的
   ]
 }
 ```

配置了这些文件之后，重启webpack，这样图片就可以加载出来了  

###然后写SignIn.js的代码

 ```
 import React from 'react';

 class SignIn extends React.Component{
   getStyles(){
     return {
       float:'right'
     }
   }
   render(){
     let color=0;
     let styles={
       leftBtn:{background:color?'red':'yellow'},
       rightBtn:{background:'blue'}
     }
     return(
       <div style={this.getStyles()}>
         <button style={styles.leftBtn}>登陆</button>   //这样写的是行内样式
         <button style={styles.rightBtn}>注册</button>
       </div>
     )
   }
 }

 export default SignIn;
 ```

###然后写一下Banner.js的代码，跟其他的基本上一样

 ```
 import React from 'react';

 class Banner extends React.Component{
   render(){
     return(
       <div>
         我是banner
       </div>
     )
   }
 }

 export default Banner;
```

###然后写一下Footer.js的代码

```
import React from 'react';

class Footer extends React.Component{
  render(){
    return(
      <div>
        我是footer
      </div>
    )
  }
}

export default Footer;
```


##最后我们写APP.js这个文件

```
import React from 'react';


import Header from './Header.js'
import Banner from './Banner.js'
import Footer from './Footer.js'

class App extends React.Component{
  render(){
    return(
      <div>
        <Header/>
        <Banner/>
        <Footer/>
      </div>
    )
  }
}
export default App;
```

##修改以下我们的index.js文件

```
import App from './App.js'
import './main.css'
 ReactDOM.render(
   <App/>,document.getElementById('box3')   //这个地方的<APP/>与你写的import后的APP名称必须一致
 )
```
其中引入main.css的时候，就直接通过import直接引入就可以，里面的样式还是以前学习的css样式那么去写



###这样就连接起来了整个头部，banner和footer部分
