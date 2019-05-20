---
layout: =
title: '易忘的JS用法 '
date: 2018-09-26 16:40:34
tags:
    - 学习
    - 前端
    - js
---
![]()

>此篇笔记主要是记录自己易忘的js用法，
<!-- more -->

## 算出某段程序运用时间
代码如下
```
console.time("time");// 启动计时器
code...
console.timeEnd("time");// 停止计时，输出时间
```
代码解释：在控制台打印出执行代码code的时间