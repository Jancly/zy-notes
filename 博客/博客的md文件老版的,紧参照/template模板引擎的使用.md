---
layout: =
title: 'template模板引擎的使用 '
date: 2018-10-18 11:08:23
toc: ture
tags:
    - 学习
    - 前端
    - 模板引擎
---
> 本篇文章主要介绍template模板引擎的使用
<!-- more -->

## 一，template模板引擎的介绍

[点击我查看template基本内容](https://aui.github.io/art-template/zh-cn/docs/)

## 二，template模板的具体操作方法
### 1，一般模板
1. 导入js插件 [插件地址](https://unpkg.com/art-template@4.13.1/lib/template-web.js)
2. 定义模板(要求script标签里必须有type="text/html"和id)
3. 利用template()方法将数据传入到模板
例子如下：
```
1，导入js插件
<script type="text/javascript" src="../js/template.js" ></script>
2. 定义模板(要求script标签里必须有type="text/html"和id)
<script type="text/html" id="resultTemplate">	
    <!--result是data对象数据下的 value是result的值，i是角标-->
    <ul>
    {{each result as value i}}
    <li><span>结果{{i}}：</span> <span>{{value[0]}}</span></li>
    
    {{/each}}
    </ul>
</script>
 3. 利用template()方法将数据传入到模板  
var data ={
        
        Isright:true,
        value:['跑步','吉他','睡觉','打球'],
        kk:"<span style='color: red;'>这是测试</span>"
    }
        var html = template("resultTemplate",data);
        resultTemplate是模板id,data是要传入模板的数据
```
### 2, 模板的其他的语法
**如下例子：**
```
<!--if判断如果数据data中的Isright是true则进行下一段-->
			{{if Isright}}
			<!--遍历data下的value数组,val为value下的值-->
			{{each value as val i}}
			<ul>
			  <li>{{val}}</li>
			</ul>
			{{/each}}
			{{kk}}我是默认转义转为字符串<br>
			{{#kk}}我将转为浏览器能够识别的
			{{/if}}
```
**模板的基本语法如下**

```
 1. 获取数据中的值{{value}}
 2. 循环操作{{each kk as value i}}{{/each}}kk为数据下的数组或其他,value为kk的值，i为kk的角标
 3. 转义#  默认转义(字符串形式){{value}}， 转义{{#value}}转成浏览器能识别的字符
 4. 条件判断 {{if xxx}} {{/if}}
```