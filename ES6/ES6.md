---
title: es6 基础
layout: linux
---

## es6 基础

ECMAScript简称就是ES,你可以把它看成是一套标准,JavaScript就是实施了这套标准的一门语言 现在主流浏览器使用的是ECMAScript5。


ECMAScript 6.0（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。在项目中80%的时间用到的ES6语法只占其20%，所以我们暂时先集中精力把这20%学好，那就差不多够用了，剩下的可以看书或是查文档，现学现用。

### 1、Let + Const 块级作用域和常量

let 与 const 声明变量的特点

参考以下demo：

```
//demo1  let 声明的变量自带作用域，默认为大括号{}
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n);  // 5
}

//demo2  let 声明的变量值可更改
let a=10;
a=5;
console.log(a)  //5

//demo3  let 声明变量，嵌套循环不会相互影响
for (let i = 0; i < 3; i++) {
  console.log("out", i);
  for (let i = 0; i < 2; i++) {
    console.log("in", i);
  }
}
//结果 out 0 in 0 in 1 out 1 in 0 in 1 out 2 in 0 in 1

//demo4 let/const 声明变量重复定义会报错
if(true){
  let a = 1;
  let a = 2;  
}
consolel.log(a)  //Identifier 'a' has already been declared

if(true){
  const a=1;
  const a=2;
}
console.log(a)   //Identifier 'a' has already been declared

//demo5 let/const 声明变量，不存在变量的提升
console.log(i,m)
let i=10;
const m=5;
结果 i is not defined

// demo6  const 声明的变量不可更改
const PI = 3.1415;
console.log(PI); // 3.1415

PI = 3;
console.log(PI); // TypeError: "PI" is read-only

if (true) {
  var a = "a"; // 期望a是某一个值
}
console.log(a);
if(true){
  let name = 'zfpx';
}
console.log(name);// ReferenceError: name is not defined


// 闭包新写法
// 以前
;(function () {

})();

现在
{
}


```

### 2.解构

解构意思就是分解一个东西的结构,可以用一种类似数组的方式定义N个变量，可以将一个数组中的值按照规则赋值过去。

```
var [name,age] = ['zfpx',8];  // 定义变量用var/const/let 都可以
console.log(name,age);  // zfpx 8

let [a,b,c]=["abc"]
console.log(a,b,c)  // abc undefined undefined


var [x,y]=getVal(),//函数返回值的解构
    [name,,age]=['zf','male','secrect'];//数组解构

function getVal() {
    return [ 1, 2 ];
}
console.log(x,y);//输出：x:1, y:2
console.log(name,age);//输出： name:zf, age:secrect

```

数组、对象和字符串的解构赋值示例：

```
// 数组的解构赋值
let [one,[[two],three]] = [1,[[2],3]];
console.log(One); // 1
console.log(two); // 2
console.log(three); // 3

// 对象的解构赋值
var { foo, bar } = { foo: "aaa", bar: "bbb" };
console.log(foo);   // "aaa"
console.log(bar );  // "bbb"

var res={
  a:2,
  b:3,
  c:4
}
let {a,c}=res;
console.log(a,c)  // 2 4

// 字符串的解构赋值
const [a, b, c, d, e] = 'hello';
console.log(a + b + c + e); // 'hello'
```

```
this 的指向
var obj={
  name:"aaa",
  say:function aaa(){
    console.log(this)  // obj
  }
}
obj.say()


function ccc(){
  console.log(this)  // window
}

ccc()  //window.ccc()
```

### 3.Arrows 箭头函数

- 箭头函数简化了函数的的定义方式，一般以 "=>" 操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。

- 箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数，从而避免了this指向的问题。
请看下面的例子。

```
//以前
let [a,b]=[1,2];
function add(a,b) {
  console.log(a+b);
}
add(a,b);

//现在
let add = (a,b) => console.log(a+b);  // let/const/var 函数名=（函数参数）=> 返回值


var m=(name,age)=>({name:name,age:age+2});//返回对象
console.log(m("lucy",1))   // object{name:"lucy",age:3}


var b=(x,y)=>{
  console.log(x);    //返回多条语句，要用大括号包裹起来，返回值要手动去书写
  alert(y);
  return {x,y}
}
console.log(b(2,3))  // object{x:2,y:3}


var c=()=>{     //函数有一个参数可以省略括号，函数如果没有参数，小括号不能省略，必须加上
  console.log("ccc");
  alert("abc");
  return 111;
}
console.log(c())  // 111


let k =10;
let obj1={
  k,
  say(){
    console.log("es6 允许的方法的写法")   //  es6允许的方法的写法
  }
}
console.log(obj1)  // object{k:10}
obj1.say()


function add(x,y){   //如果只给一个参数，已知值默认给X，Y的值默认为10；普通写法
  var x=x || 0;
  var y=y || 5;
  return x+y
}
console.log(add(3))


function add(x=5,y=10){  //如果只给一个参数，已知值默认给X，Y的值默认为10； Es6 中的写法
  return x+y
}
console.log(add(3))
```

数组

```
function restFun(a,...rest){    //rest 输出的是数组，a后面所有参数组成的数组（不包含a)
  console.log(a);
  console.log(rest)
}
restFun(1);
restFun(1,2,3,4,5,6)

//将所有参数相加；
function add(...x){             //reduce() 数组的方法，参数为函数，箭头函数
  return x.reduce((m,n)=>m+n)
}


//传递任意个数参数
console.log(add(1,2,3))
console.log(add(1,2,3,4,5,6))



var people=["linda","lily","lucy"]
console.log(...people)
function sayHello(people1,people2,people3){
  console.log(`Hello ${people1},${people2},${people3}`)
}
sayHello(...people)    //展开数组， ...people == "linda","lily","lucy"



let arr1=[1,2,3]
let arr2=["a","b","c"]
let arr3=[...arr1,...arr2]
console.log(arr3)  // [1,2,3,"a","b","c"]


let arr=[4,5,6]
let newArr=arr.map(function(currentValue,index,array){  //生成新的数组,返回值为新生成的数组
  console.log(currentValue,index,array)
  return currentValue+10;
})
console.log(newArr)


let arr4=[7,8,9]
arr4.forEach(function(currentValue,index,array){   //无返回值
  console.log(currentValue+10);
})

arr4.forEach((currentValue)=>console.log(currentValue+10))  //箭头函数写法


let arr6 =[5,8,9,12]
var results=arr6.filter(function(item,index,array){   
  console.log(item,index,array)
  return item>8
})
  过滤，按条件过滤掉不相符的，返回筛选的条件，返回值为符合条件的新数组

// var results=arr.filter(item=>item>8)  箭头函数写法  返回值为筛选的条件

console.log(results)
```

### 4、Template Strings 字符串模板(字符串拼接)

```
let age=10;
let name="lucy";
console.log(`姓名是${name}的年龄是${age}岁`);
console.log("姓名是"+name+"的年龄是"+age+"岁")
```

### 5.Class基本语法

JavaScript语言的传统方法是通过构造函数，定义并生成新对象。下面是一个例子。

```
function Point(x,y){
  this.x=x;
  this.y=y;
}

Point.prototype.toString=function(){
  return '('+this.x+','+this.y+')'       //  另一种写法：`(${this.x},${this.y})`
}

var p=new Point(1,2)
console.log(p.x)  // 1
console.log(p.y)  // 2
console.log(p.toString())   //(1,2)
```

上面这种写法跟传统的面向对象语言（比如C++和Java）差异很大，很容易让新学习这门语言的程序员感到困惑。

ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用ES6的“类”改写，就是下面这样。

```
class Point{
  constructor(x,y){  // 类添加属性要添加到constructor内部，是自动执行的
    console.log("‘constructor’是自动执行的")
    this.x=x;
    this.y=y;
  }
  toString(){
    return this.x
  }
}
var p=new Point(5,6)

console.log(p)  // 对象  Point{x:5,y:6}
console.log(p.x,p.y)  // 5 6
console.log(p.toString)  // toString 的方法
console.log(p.toString())  // 5
```

上面代码定义了一个“类”，可以看到里面有一个constructor方法，这就是构造方法，而this关键字则代表实例对象。也就是说，ES5的构造函数Point，对应ES6的Point类的构造方法。

Point类除了构造方法，还定义了一个toString方法。注意，定义“类”的方法的时候，前面不需要加上function这个关键字，直接把函数定义放进去了就可以了。另外，方法之间不需要逗号分隔，加了会报错。

class 的继承

Class之间可以通过extends关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰和方便很多。

```
class Point{
  constructor(x,y){  // 类添加属性要添加到constructor内部，是自动执行的
    console.log("‘constructor’是自动执行的")
    this.x=x;
    this.y=y;
  }
  toString(){
    return `point toString`
  }
}

class Hello extends Point{
  constructor(c,d){
    super()   //继承属性
    this.c=c;
    this.d=d
  }
  say(){
    return `hello say`
  }
}

var h=new Hello(2,3);
console.log(h)  
console.log(h.toString())  //point toString
```

### 6.module

- 命名导出，用大括号包裹需要导出的名称, 语法： export {name}

```
let a=10;
let b=5;
export {a,b}  //多个导出，中间用逗号隔开
```

- 命名引入，语法： import {导出名}  from '路径文件'

```
import {a,Father} from './demo'  //引入多个，中间用逗号隔开
```

- 默认导出  通常只导出一个，想导出多个用 `{  }` 包裹，以对象的方式导出，一般不常用多个导出

```
export default a  //export default 名称

// 另一种写法
default function aaa(){
  return "默认导出的另一种写法"
}
```

- 默认导入, 语法：  import demo(随便起名) from ‘路径文件’

```
import demo from './demo'
```
