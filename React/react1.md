---
title: 基本 Webpack React 项目搭建
layout: linux
---

## 基本 Webpack React 项目搭建

G这一集来跑一个 React 的 Hello World ，但是重点我们看一下一个最简的 webpack 配置是怎么样的。

### 最简单的 Webpack 配置文件

首先新建一个项目文件夹，然后在该文件夹下，命令行运行 npm init，回车，
然后在项目文件夹下，new file一个文件，名字叫做webpack.config.js,切记名字不可以写错，里面的内容如下

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

点击 Docs下的setup，点击Webpack选项，然后到命令行 粘贴复制这段代码并回车：

```
npm install --save-dev babel-loader babel-core
```
然后去webpack.config.js这个文件中写上这段代码

```
module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, use: "babel-loader" }
  ]
}
```

然后在去新建一个文件，名字叫做.babelrc，里面复制一下内容

```
{
  "presets": ["env","react"]
}
```

这样在package.json这个文件最后就可以看到安装的包了，即

```
"babel-core": "^6.23.1",
"babel-loader": "^6.3.2",
"babel-preset-env": "^1.1.8",
"babel-preset-react": "^6.23.0",
"webpack": "^2.2.1"
```

这样基本就可以了，但是每次我们运行webpack 都要敲打./node_modules/.bin/webpack，所以我们就把这段话写到package.json中

```
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "test2": "./node_modules/.bin/webpack --watch",            /这个test2可以随便起名   --watch是监听/
  "push": "git add . && git commit -m'add' && git push"
},
```

这样每次我们在终端运行 npm run test2即可
