---
layout: =
title: 'Vue案例方法 '
date: 2018-08-25 20:32:50
toc: true
tags:
    - 学习
    - vue
    - 前端
---
Vue.js方法

<!-- more -->
# 常见的Vue方法集合
## 一,关于数组的方法
forEach some filter findIndex
### 1.1forEach
* 关于关键字搜索的案例（部分）
```
v:
搜索关键字:<input type="text" class="form-control" v-model="keyword"/>
<tr v-for="item in serch(keyword)" :key="item.id">//循环
vm:
serch(keyword){
    //	1，forEach()方法遍历
    var newList = []//定义一个新的数组
    this.list.forEach(item => {
        //列表的名字与关键字有包含则返回对应的数组
        //-1表示不包含，关键字为""时为0返回所有数组
        if(item.name.indexOf(keyword) != -1){//查找名字相符合的关键字
            newList.push(item) //把符合关键字的数组移到新数组中
        }						
    })
    return newList //返回新数组
```
### 1.2 filter
* 关于关键字搜索的案例（另一种方法）
```
return	this.list.filter(item => {
 //   if(item.name.indexOf(keyword)!=-1){
 //       return item
//}
    if(item.name.includes(keyword)){
        return item
    }	
})
```
### 1.3 some
* 关于删除列的案例
```
v:
<a  href="#"  @click.prevent="delect(item.id)">删除</a>	
vm:
delect(id){//根据id删除数据
//两种方法
//根据id找索引然后再调用数组的splice方法
//利用some方法
/*this.list.some((item,i) => {
    if(item.id == id){
        this.list.splice(i,1);
        return true;
    }	
})*/
```
### 1.4 findindext
* 关于删除列的案例另一种方法
```
var index =	this.list.findIndex(item => {
        if(item.id==id){
            return true;
        }
    })
        this.list.splice(index,1);
    },
},

