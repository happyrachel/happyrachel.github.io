---
title: git 上创建分支
layout: linux
---

停止运行目前正在运行的项目，然后查看一下当前所在分支
- git branch

把当前的制作一个版本防止丢失
- git add .
- git commit -m''
- git push

关闭atom，防止更换分支后混乱

将当前的项目进行打包
- git run build
生成了dist文件

### 如果是第一次上传东西到新的分支上面，则首先把dist文件和index.html文件复制到桌面一份，
### 然后将master分支上生成的dist文件夹删掉，在将复制到桌面上的index.html文件中的路径上加上一个.并保存

### 即

```
<script src="/dist/bundle.js"></script>
```
转变成
```
<script src="./dist/bundle.js"></script>
```

开一个新的分支，并查看当前所在分支
- git checkout -b gh-pages
- git branch

打开处在该分支上的项目文件夹，将其中的文件，除了.gitignore和node_moudules剩下的全部都删掉，之后把桌面上的dist文件和修改之后的index.html文件复制到项目文件夹中

然后进行
- git add .
- git commit -m''
- git push

### 这样别人就可以通过  https://happyrachel.github.io/你的项目名称,  访问你的网站了,是不是很神奇



### 如果你要修改东西的话，则需要切换到master分支
- git checkout master
- git branch

### 修改完之后就可以继续进行从头开始的内容了
