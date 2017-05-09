---
title: ES6学习笔记1-let、const
date: 2017-05-09 20:11:04
tags: [ES6,let,const]
categories: ES6学习笔记
---

虽然很早以前就学习过多次es6，平时开发也基本上在使用，自以为自己es6还算比较熟悉，但是上周去某安全公司的一次面试彻底的打击到我了，我真的会es6吗？？？因为以前学习都主要是了解起用法，对其基础的原理没有深入的了解，所以这次打算系统重新学习一次es6，并把这次学习过程以博客的方式记录下来。

---

## let
### 定义
let的用法类似于var，用来声明变量,但是所声明的变量，只在let命令所在的代码块内有效(块级作用域，通俗讲就是在{}中间)。
```bash
{
  let a = 1;
  var b = 2;
  console.log(a) //1
  console.log(b) //2
}
console.log(a) //ReferenceError: a is not defined
console.log(b) //2
```
常见使用环境，例如for循环：
```bash
  for(var i = 0; i < 10; i++) {
    setTimeout(function () {
      console.log(i)
    })
  }
  //输出10次10

  //es5 使用闭包
  for(var i = 0; i < 10; i++) {
    (function (i){
      setTimeout(function () {
        console.log(i)
      })
    })(i)
  }
  //0、1、2...9
  //es6 let
  for(let i = 0; i < 10; i++) {
    setTimeout(function () {
      console.log(i)
    })
  }
  //0、1、2...9
```
### 变量提升
var申明变量存在变量提升的问题(即变量可以在声明之前使用，值为undefined),let申明的变量不存在这种问题。
```bash
//var
{
  console.log(a) //undefined
  var a = 1
}
//let
{
  console.log(b) //ReferenceError
  let b = 2
}
```
### 暂时性死区
暂时性死区（temporal dead zone，简称 TDZ）和变量提升有些类似，即变量在使用let命令声明之前，该变量都是不可用的
```bash
{
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```
### 重复申明
let不允许在相同作用域内，重复声明同一个变量。
```bash
//var
{
  var a = 1
  var a = 2
  //a = 2
}
//let
{
    let b = 1
    let b = 2
    //error
    let c = 10
    var c = 1
    //error
}
```

---
## 作用域
### 全局作用域
不在任何函数内定义的变量就具有全局作用域。<br>
ES5默认有一个全局对象（等价于顶层对象）window，全局作用域的变量实际上被绑定到window的一个属性。<br>
ES6规定var命令和function命令声明的全局变量，依旧是顶层对象的属性；let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。
```bash
var a = 1;
// 如果在Node的REPL环境，可以写成global.a
// 或者采用通用方法，写成this.a
window.a // 1

let b = 1;
window.b // undefined
```
### 函数作用域
定义在函数中的参数和变量在函数外部是不可见的。
```bash
  function test() {
    var a = 1
  }
  console.log(a)
  //ReferenceError
```
### 块级作用域
任何一对花括号中的语句集都属于一个块，在这之中定义的所有变量在代码块外都是不可见的，我们称之为块级作用域。
```
function f1() {
  let n = 5;
  if (true) {
    let n = 10
  }
  console.log(n) // 5
}

//块级作用域的任意嵌套
{{{{{let insane = 'Hello World'}}}}}

{{{{
  {let insane = 'Hello World'}
  console.log(insane); // 报错
}}}}

{{{{
  let insane = 'Hello World';
  {let insane = 'Hello World'}
}}}}
```
块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（IIFE）不再必要了。
```
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```

---
## const
### 定义
const声明一个只读的`常量`。一旦声明，常量的值就不能改变。<br>
```
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```
const一旦声明变量，就必须立即初始化，不能留到以后赋值。
```
const foo;
// SyntaxError: Missing initializer in const declaration
```
### 变量提升
const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
```
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```
### 重复申明
onst声明的常量，也与let一样不可重复声明。
```
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```
### 实质
const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。
```
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only

const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报错
```
