---
layout: =
title: 'JS易忘记例子 '
toc : ture
tags:
    - 学习
    - 前端
    - js
---
> 将自己容易犯错的问题或忘记的题集做一个笔记
<!-- more -->

# 关于JavaScript题集
## 一,易混淆
### 1.1javascript 中 click 和onclick有什么区别
1.onclick是绑定事件，告诉浏览器在鼠标点击时候要做什么
2.click本身是方法,作用是触发onclick事件，只要执行了元素的click()方法，就会触发onclick事件

### var与let的区别
```
var a = 99; // 全局变量a
    f(); // f是函数，虽然定义在调用的后面，但是函数声明会提升到作用域的顶部。 
    console.log(a); // a=>99,  此时是全局变量的a
    function f() {
        console.log(a); // 当前的a变量是下面变量a声明提升后，默认值undefined
        var a = 10;
        console.log(a); // a => 10
    }
```
输出的结果是：undefined 10 99

#### let是ES6中定义块级作用域变量
```
{
    var a = 9;
}
console.log(a);//输出为9
```
let只能在块级使用
```
{
    let a = 9;//a只能在花括号有用
}
console.log(a);//报错:Uncaught ReferenceError: i is not defined
```
#### let 配合for循环的独特应用
let非常适合用于 for循环内部的块级作用域。JS中的for循环体比较特殊，每次执行都是一个全新的独立的块作用域，用let声明的变量传入到 for循环体的作用域后，不会发生改变，不受外界的影响。看一个常见的面试题目：
**一个面试题**
```
for (var i = 0; i <10; i++) {  
  setTimeout(function() {  // 同步注册回调函数到 异步的 宏任务队列。
    console.log(i);        // 执行此代码时，同步代码for循环已经执行完成
  }, 0);
}
// 输出结果
10   共10个
// 这里面的知识点： JS的事件循环机制，setTimeout的机制等
```
将var改成let
```
// i虽然在全局作用域声明，但是在for循环体局部作用域中使用的时候，变量会被固定，不受外界干扰。
for (let i = 0; i < 10; i++) { 
  setTimeout(function() {
    console.log(i);    //  i 是循环体内局部作用域，不受外界影响。
  }, 0);
}
// 输出结果：
0  1  2  3  4  5  6  7  8 9
```
#### let不能重复使用
let不允许在相同作用域内，重复声明同一个变量。否则报错：Uncaught SyntaxError: Identifier 'XXX' has already been declared
**如：**
```
let a = 0;
let a = 'sss';
//报错 Uncaught SyntaxError: Identifier 'a' has already been declared
```
#### let不能声明前使用
* let不能声明前使用即et没有变量提升与暂时性死区
例如：
```
console.log(aicoder);    // 错误：Uncaught ReferenceError ...
let aicoder = 'aicoder.com';
// 这里就可以安全使用aicoder
```
> ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
 总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead  zone，简称 TDZ）。

#### 总结
**let与var的区别**
1. let使用在块级区域
JavaScript的作用域（scope）只有全局和局部，对于var声明的变量，只有函数才能为它创建新的作用域，而let支持块级作用域，花括号就能为它创建新的作用域；
2. let不能重复声明
相同作用域，var可以反复声明相同标识符的变量，而let是不允许的;
3. let不能声明前使用
用let声明的变量，不存在变量提升。而且要求必须 等let声明语句执行完之后，变量才能使用，不然会报Uncaught ReferenceError错误。

