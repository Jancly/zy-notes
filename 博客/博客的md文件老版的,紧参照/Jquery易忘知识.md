---
layout: =
title: Jquery
date: 2018-09-18 09:53:33
tags:
    - 学习
    - 前端
    - jquery
---
> 将写代码时碰到的难题在百度找的方法记录在此
<!-- more -->
## Jquery中valitate的使用
[原文链接](https://www.jb51.net/article/107581.htm)

## Jq中时间格式化
```
时间格式化
Date.prototype.Format = function (fmt) { //author: meizz
  var o = {
    "M+": this.getMonth() + 1, //月份
    "d+": this.getDate(), //日
    "h+": this.getHours(), //小时
    "m+": this.getMinutes(), //分
    "s+": this.getSeconds(), //秒
    "q+": Math.floor((this.getMonth() + 3) / 3), //季度
    "S": this.getMilliseconds() //毫秒
  };
  if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
  for (var k in o)
  if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
  return fmt;
}
$(function(){
  var date=new Date();
  <!-- 格式可改变 -->
  alert(JSON.stringify(date.Format("yyyy年MM月dd hh:mm:ss")));
})
```
代码输出当前的年月日时分。
## 表格的增加列与删除
### 列增加但dom有增加
```
var del = "<a class='del'>删除</a>";
var tr = "<tr>" + "<td>" + name + "</td>" + "<td>" + describle + "</td>" + "<td>" + time + "</td>" + "<td>" + del + "</td>" + "</tr>";
$("#tbody").append(tr);
```
解释：html能看到显示但在源码没有
### 列增加源码也增加
```
//添加方法
$("#add").bind("click",function(){
    var del = "<a class='del'>删除</a>";
var tr = "<tr>" + "<td>" + name + "</td>" + "<td>" + describle + "</td>" + "<td>" + time + "</td>" + "<td>" + del + "</td>" + "</tr>";
$("#tbody").append(tr);   
```
解释：源码里有，页面也能看的到
### 动态删除
* 此方法适用于用jq添加的元素删除
```
$("#tbody").on("click", ".del", function() {
    //获取此元素父容器
    var aindex= $(this).parents("tr");
    aindex.remove();
    //直接删除此容器
    //$(this).remove();
});
```
解释：此方法可以删除jq添加的元素有的。
### 静态删除
```
$(function(){
$("tbody a").click(function(){
    var aindex= $(this).parents("tr");
aindex.remove();	
});
```
解释：此方法只能删除原来html里有的元素，不能删除jq增加的元素。