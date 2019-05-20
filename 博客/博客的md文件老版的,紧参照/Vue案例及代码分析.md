---
layout: =
title: Vue案例及代码分析
date: 2018-08-21 20:01:30
tags:
    - 学习
    - 前端
    - vue
---

<!-- more -->
# Vue案例及代码分析
## 一，从跑马灯代码分析
```
<body>
<div id="zou">
	<input type="button" value="浪起来~" @click="lang" />
	<input type="button" value="低调" @click="stop" />
	<h1 id="zi">{{ msg }}</h1>
</div>
<script type="text/javascript">
	//在vm实例中如果需要调用data数据或者调用methods的方法需要使用this.属性名或者
	//，this.方法名，this为new出来的对象
	var vm = new Vue({
		el: "#zou",
		data: {
			msg: "猥琐发育，别浪~",
			time: null,
		},
methods: {
	lang() {
		//var _this = this;//因为定时器里的指向问题
		//var time = setInterval(function() {
		//对字符截取
		//var st = _this.msg.substring(0, 1)
		//var ed = _this.msg.substring(1)
		//字符重新组合
		//_this.msg = ed + st
		//}, 400)
		/*
		* 第二种写法
		*/
		if(this.time!=null) return;//如果time值不为空则返回
		this.time = setInterval(() => {
			console.log(this.msg)
			//对字符截取
			var st = this.msg.substring(0, 1)
			var ed = this.msg.substring(1)
				//字符重新组合
			this.msg = ed + st
		}, 400)
		
		},
		stop(){
			clearInterval(this.time);//清除定时器
			
			this.time=null;//重新赋值为空
		}
	}
	});
//注意：vm会监听自己data的所有数据的改变，只要data数据发生改变，
就会把最新数据从data同步到页面中去；
//好处：程序员不需要关心如何渲染到DOM的页面中去，只需关心数据；
</script>
</body>
```
<!-- more -->
## 二，简单的计算器
1. 案例解释：本案例主要是运用v-model的双向数据v<=>m
2. 代码展示：
```
<div id="c">
	<input type="text"  v-model:value="n1" />
	<select  v-model:value="opt" >  
		<option value="+">+</option>
		<option value="-">-</option>
		<option value="*">*</option>
		<option value="/">/</option>
	</select>
	<input type="text"  v-model:value="n2" />
	<input type="button" value="=" @click="maths" />
	<input type="text" v-model:value="result"/>	
</div>
<script type="text/javascript">
	var vm = new  Vue({
		el: "#c",
		data:{
			n1: "0",
			n2: "0",
			result: "0",
			opt: "+",				
		},
methods:{
maths(){						
switch(this.opt){
	case '+':
	this.result = parseInt(this.n1)+parseInt(this.n2)
	break;
	case '-':
		this.result = parseInt(this.n1)-parseInt(this.n2)
	break;
	case '*':
		this.result = parseInt(this.n1)*parseInt(this.n2)
	break;
	case '/':
		this.result = parseInt(this.n1)/parseInt(this.n2)
	break;
}
//上面的方法可以用eval()方法来操作
//eval()方法是将字符串进行函数算法，此方法尽量不要在做项目中出现
var r = 'parseInt(this.n1)'+'+'+'parseInt(this.n2)'
this.result = eval(r);
```
## 三，品牌列表的增加与删除
```
	<label>
		<!--v-model是为了实现双向数据传输-->
			ID:<input type="text" class="form-control" v-model="id"/>
	</label>
	<label>
			Name:<input type="text" class="form-control" v-model="name"/>
	</label>
	<input type="button" value="添加"  class="panel-primary" @click="add()"/>
</div>
</div>				
<!--表格-->
<table class="table table-hover table-bordered table-striped">
<thead>
	<tr>
	<th>ID:</th>
	<th>Name:</th>
	<th>Ctiem</th>
	<th>Operation</th>
	</tr>
</thead>
<tbody>
<tr v-for="item in list" :key="item.id">
<td>{{item.id}}</td>
<td>{{item.name}}</td>
<td>{{item.ctime}}</td>					
<td>
	<!--prevent是为了阻止默认，th与td区别th是加粗了-->
	<a  href="#"  @click.prevent="delect(item.id)">删除</a>	
</td>
</tr>			
</tbody>			
</table>		
</div>	
<script type="text/javascript">
var vm = new Vue({
el:"#c",
data:{
id:"",
name:"",
list:[
{id:1 ,  name:'奔驰 ',     ctime: new Date()},
{id:2 ,  name:'五菱宏光 ', ctime: new Date()},
],	
},
methods:{
add(){
	if(this.id==""||this.name=="")return true;
	this.list.push({id:this.id,name:this.name,ctime: new Date()});
	this.id=this.name="";					
},
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

//利用findindext方法
var index =	this.list.findIndex(item => {
	if(item.id==id){
		return true;
	}
})
	this.list.splice(index,1);
}
}
});

```

