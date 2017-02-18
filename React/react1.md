---
title: 基本 Webpack React 项目搭建
layout: linux
---

## 基本 Webpack React 项目搭建

G这一集来跑一个 React 的 Hello World ，但是重点我们看一下一个最简的 webpack 配置是怎么样的。

### 最简单的 Webpack 配置文件

在项目文件夹下，new file一个文件，名字叫做webpack.config.js,切记名字不可以写错，里面的内容如下

```
module.exports = {
  entry: './src/index.js',     /这是入口，一个项目只有一个入口文件/
  output: {
    path:'build',        /这是路径文件夹/
    filename:'bundle.js'    /这是路径夹下文件的名字/
  },
  devtool:'eval',
  module: {
    rules: [
      { test: /\.js$/, exclude: /node_modules/, use: "babel-loader" }
    ]
  }
}
```

### 一句话说明上面文件的作用

项目是 React 项目，所以项目代码中有 ES6 和 JSX 语法都是浏览器不能直接运行的，所以项目需要先编译后运行。上面的配置文件的作用，一句话概括：

> 用 babel 把入口文件 index.js 编译成 bundle.js

详细来说，完成了下面几个小任务：

- 编译 JSX 成原生 JS

- 编译 ES6 成原生 JS

- 把 index.js 引领的多个 ES6 模块文件，打包成一个 bundle.js

注意：Webpack 已经不仅仅是一个打包器了，它已经发展成一个强大的 build tool 构建工具，里面可以融入大量辅助开发的插件。所以通常我们就是把 babel 作为 Webpack 的功能之一来使用。

###添加webpack的插件，也就是babel

babel的官网是 [http://babeljs.io/]（http://babeljs.io/）
