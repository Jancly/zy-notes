---
layout: =
title: 'html中易忘知识点 '
date: 2018-10-03 16:45:44
toc : ture
tags:
    - 学习
    - 前端
    - html
---
> 本章主要讲解关于html中自己特别容易忘记的知识点
<!-- more -->

## 标签html中解释
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd>
<html xmlns="http://www.w3.org/1999/xhtml">
```
解释：
1. 声明了文档的根元素是 html
2. 公共标识符被定义为 "-//W3C//DTD XHTML 1.0 Transitional//EN" 的 DTD 中进行了定义。浏览器将明白如何寻找匹配此公共标识符的 DTD。如果找不到，浏览器将使用公共标识符后面的 URL 作为寻找 DTD 的位置

3. HTML 4.01 规定的三种文档类型、XHTML 1.0 规定的三种 XML 文档类型都是：Strict、Transitional 以及 Frameset。
4. html xmlns="http://www.w3.org/1999/xhtml"，是在文档中的html 标签中使用 xmlns 属性，以指定整个文档所使用的主要命名空间。即声明文档的命名空间。

## 块级元素与行级元素
### 块级元素
**特点：**
1. 总是从新的一行开始
2. 高度、宽度都是可控的　　
3. 宽度没有设置时，默认为100%
4. 块级元素中可以包含块级元素和行内元素
* 常见的块级元素
body  from  select  textarea  h1-h6 html table  button  hr  p  ol  ul  dl  cnter  div address blockquote
```
  <address>...</adderss>   

  <center>...</center>  地址文字

  <h1>...</h1>  标题一级

  <h2>...</h2>  标题二级

  <h3>...</h3>  标题三级

  <h4>...</h4>  标题四级

  <h5>...</h5>  标题五级

  <h6>...</h6>  标题六级

  <hr>  水平分割线

  <p>...</p>  段落

  <pre>...</pre>  预格式化

  <blockquote>...</blockquote>  段落缩进   前后5个字符

  <marquee>...</marquee>  滚动文本

  <ul>...</ul>  无序列表

  <ol>...</ol>  有序列表

  <dl>...</dl>  定义列表

  <table>...</table>  表格

  <form>...</form>  表单

  <div>...</div>
  ```
**行内元素：**
  1. 和其他元素都在一行
  2. 高度、宽度以及内边距都是不可控的
  3. 宽高就是内容的高度，不可以改变
  4. 行内元素只能行内元素，不能包含块级元素
```
  <span>...</span>

  <a>...</a>  链接

  <br>  换行

  <b>...</b>  加粗

  <strong>...</strong>  加粗

  <img >  图片

  <sup>...</sup>  上标

  <sub>...</sub>  下标

  <i>...</i>  斜体

  <em>...</em>  斜体

  <del>...</del>  删除线

  <u>...</u>  下划线

  <input>...</input>  文本框

  <textarea>...</textarea>  多行文本

  <select>...</select>  下拉列表
```