---
layout: =
title: Vue.js的学习第一章
date: 2018-08-20 09:54:48
toc: true
#分页标签
categories: "前端"
tags:
    - 学习
    - 前端
    - vue
---


<!-- more -->
# vue与MVVM
## 一，MVVM 与 MVC解释
MVC （Model-View-Controller）

M - Model ：数据保存

V - View : 用户界面

C - Controller ： 业务逻辑
1，MVVM:MVVM是Model-View-ViewModel的简写。即模型-视图-视图模型。【模型】M指的是后端传递的数据。【视图】v指的是所看到的页面。【视图模型】vm mvvm模式的核心，它是连接view和model的桥梁。它有两个方向：一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据。实现的方式是：DOM 事件监听。这两个方向都实现的，我们称之为数据的双向绑定。

MVVM是将“数据模型数据双向绑定”的思想作为核心，因此在View和Model之间没有联系，通过ViewModel进行交互，而且Model和ViewModel之间的交互是双喜那个的，因此试图的数据的变化会同事修改数据源，而数据源数据的变化也会立即反应到View上。


2,MVC:MVC是Model-View- Controller的简写。即模型-视图-控制器。M和V指的意思和MVVM中的M和V意思一样。C即Controller指的是页面业务逻辑。使用MVC的目的就是将M和V的代码分离。‘MVC是单向通信。也就是View跟Model，必须通过Controller来承上启下。MVC和MVVM的区别并不是VM完全取代了C，ViewModel存在目的在于抽离Controller中展示的业务逻辑，而不是替代Controller，其它视图操作业务等还是应该放在Controller中实现。也就是说MVVM实现的是业务逻辑组件的重用。由于mvc出现的时间比较早，前端并不那么成熟，很多业务逻辑也是在后端实现，所以前端并没有真正意义上的MVC模式。
MVC ，用户操作> View (负责接受用户的输入操作)>Controller（业务逻辑处理）>Model（数据持久化）>View（将结果通过View反馈给用户）

<!-- more -->
## 二，vue中v-cloak,v-text,v-html,v-bind
### 1.v-cloak
代码：
```
样式：
		[v-cloak]{
			/*没加载时不显示可以消除闪烁*/
			display: none;

		}
body:

<p>{{ msg }}</p>
<!--使用v-cloak可以解决插值闪烁问题-->
	<p v-cloak>=={{ msg }}-- </p>

vm:
var vm = new Vue({
			el:"#c"	,
			data:{
				msg:"你好！"
            }
)}
```
结果为：你好！
### 2.v-text
能覆盖原有内容
代码：
```
<!--使用 v-text 默认没有闪烁，会将原本内容清空-->
		    <h1 v-text="msg">===</h1>
```
### 3.v-html
能覆盖原有内容
代码：
```
<div v-html="msg2">fgyhtrf</div>
data:{
				msg:"你好！",
				msg2:"<h1>我是一个大H </h1>",
			}

```
### 4.v-bind（属性绑定）
:v-bind 是 在vue中用来绑定属性的指令（缩写:）
代码：
```
<input type="button" value="按钮" title="按钮" />
<input type="button" value="按钮" v-bind:title="mytitle" />
	<!--v-bind 是可以简写为：中也可以写合法的js表达式-->
<input type="button" value="按钮"  :title="mytitle+'123'" />
```
### 5.v-on(事件绑定)
v-on （缩写@)
* 未绑定时的需要使用dom操作
代码：
```
<input type="button" value="点击按钮" id="button" />
			document.getElementById("button").onclick = function(){
			alert("你好")
		}
```
* 使用v-on操作
代码：
```
<input type="button" value="点击按钮" id="button" v-on:click="show" />
//缩写 <input type="button" value="点击按钮" id="button" @click="show" />
//在vue里的methods中放入点击的方法
methods:{//methods定义vue属性所有实例方法
					show:function(){
						alert("vue事件绑定！")
					}
					
				}		
```
## 三，事件修饰符
### 3.1 .stop(阻止冒泡)
自我解释：按钮添加.stop阻止冒泡，在重叠的事件中只能点最上面的
```
<div class="inner" @click="innerclc">
		<input type="button" value="点击" @click.stop="butclc" />
	</div>
```
### 3.2 .prevent(阻止默认事件)
自我解释：添加.prevent阻止默认,不能进入百度页面
```
<a href="https://www.baidu.com/" @click.prevent="qu">百度娘</a>
```
### 3.3 .capture(添加事件侦听器使用事件捕获模式)
自我解释：方框.capture点击按钮时从外到里进行捕获
```
<div class="inner" @click.capture="innerclc">
		<input type="button" value="点击" @click="butclc" />
</div>
```
### 3.4 .self(只当事件在该元素本身‘比如不是子元素’触发时触发回调)
自我解释：添加.self作用为只有点击了本元素才能触发此元素的函数,
只能阻止自己本身的冒泡，并不会阻止其他的冒泡，与.stop不同。
```
<div class="inner" @click.self="innerclc">
	<input type="button" value="点击" @click="butclc" />
</div>
```
### 3.5 .once（事件只触发一次）
自我解释：只能触发一次
## 四，v-model的数据双向传送
### 4.1 数据的单向传送
1. 自我解释：利用v-bind只能单向数据传送，不能通过v=>m,只能通过m=>v
m的数据的修改能改变v的，但v不能改变m的
2. 举例代码：
```
<div id="c">
			<h2>{{ msg }}</h2>
			<input type="text" name="" id="" v-bind:value="msg" />			
		</div>
```
v-bind只能单向绑定，从m绑定到v,不能实现数据的双向绑定，
### 4.2 数据的双向传送
1. 自我解释：能够实现v<=>m，随便改变哪个数据都能一起修改
2. 代码：
```
<div id="c">
			<h2>{{ msg }}</h2>
			<input type="text" name="" id="" v-model="msg" />
		//同等<input type="text" name="" id="" v-model:value="msg" />				
</div>
```
3. 注意：v-model只能运用在表单元素中
例如：
input(radio,text,address,email...),select ,checkbox,textarea;
## 五，在Vue使用的样式
### 5.1 四种class样式
* 一些忘记的样式
```
.thin{
	/*字体的粗细*/
	font-weight: 200;
}
.italic{
	/*字体为斜体*/
	font-style: italic;
}
.active{
	/*字体的间距*/
	letter-spacing:0.5em;
}
```
1. 数组样式
解释：传递一个数组，class需要用v-bind绑定
```
<h1 :class="['red', 'active', 'italic']"> 这是一个大大的H1</h1>
```
2. 数组中添加三元表达式
```
<h1 :class="['red', 'active', flag?'italic':'']"> 这是一个大大的H1</h1>
data:{
	flag: true,
},
```
3. 数组添加对象增加可读性
```
<h1 :class="['red','active',{'thin':flag}]"> 这是一个大大的H1</h1>
```
4. 直接使用对象
```
<h1 :class="{active:true ,italic:true ,red:true}">这是一个大大的H1</h1>

或者：
<h1 :class="a">这是一个大大的H1</h1>
a:{active:true ,italic:true ,red:true},
```
### 5.2 三种style样式
1. 直接在元素通过:style形式，书写样式对象
```
<h1 :style="{color: 'blue','font-weight':'200',   }" >这是一个大大的H1样式！</h1>
```
**注意样式有'-'时需要打'',**
2. 将样式在data定义为对象，并直接引用到：style
```
<h1 :style="style1" >这是一个大大的H1样式！</h1>
data: {
		style1:{color: 'blue', 'font-weight':'200' , 'font-style': 'italic'    },
		}	
```
3. 在：style通过数组引用多个data上的对象
```
<h1 :style="[style1,style2]" >这是一个大大的H1样式！</h1>
data: {
		style1:{color: 'blue', 'font-weight':'200' , 'font-style': 'italic'    },
		style2:{'letter-spacing':'0.5em'}
	},
```
## 六， v-for的四种使用方式
### 1. 循环数组
```
<!--普通数组-->
	<h3 v-for="item in list">{{item}}</h3>
<!--带有索引值的数组-->
	<h3 v-for="(item,i) in list" > 索引值==={{i}}===值{{item}}   </h3>
	data:{
	list:[1,2,3,4,5,6],
	}
```
### 2. 对象数组
```
<!--循环对象数组-->
	<h3 v-for="(user,i) in list2">{{user.id}}==={{user.name}}+++索引值{{i}}</h3>
	data:{
list2:[
			{id:1 , name:"章一" },
			{id:2 , name:"章二" },
			{id:3 , name:"章三" },
			{id:4 , name:"章四" },
			{id:5 , name:"章五" }		
			],
	}
```
### 3. 对象
```
<!--循环对象-->
	<h3 v-for="(val, key,i) in list3 ">值为{{val}}+关键字{{key}}+索引{{i}}</h3>
	<!--遍历对象时,对应的分别为 值 , 关键字和索引(少见)-->
```
### 4. 迭代数字
```
<!--迭代数组-->
	<h3 v-for="(count,i) in 5">第{{count}}次循环+索引{{i}}</h3>
	<!--注意:用v-for迭代数字时count是从1开始-->
```
### 5.v-for中key的用法
解释：v-for循环时key属性只能使用number获取string,而且必须使用v-bind绑定属性
代码中的key可以使多选框不会在添加时错位
```
<label>
		id:
	</label>
	<input type="text" v-model="id" />
	<label>
		name:<input type="text" v-model="name" />
	</label>
	<input type="button" value="添加" @click="add" />
	<!--v-for循环时key属性只能使用number获取string,而且必须使用v-bind绑定属性-->
	<h3 v-for="user in list" :key="user">
		<input type="checkbox" />
		id={{user.id}}===name={{user.name}} 
	</h3>
data:{
	id:'',
	name:'',
	list:[
	{id:1, name:"李四" },
	{id:2, name:"李看" },
	{id:3, name:"哦懂" },
	{id:4, name:"阿瑟东"}
	],}
	methods:{
	add(){
			//将添加的放到最下面
		//this.list.push({id:this.id, name:this.name });
		// 将添加的放到最上面
		this.list.unshift({id:this.id, name:this.name });
	},
```
## 七， v-if与v-show的区别
```
<input type="button" value="显示/隐藏" @click="flag=!flag" />
	<h3 v-if="flag">这是一个v-if的显示</h3>
	<h3 v-show="flag">这是一个v-show的显示</h3>
	flag:true,
```
* v-if:每次都会重新删除或重新创建元素,高性能切换消耗
* v-show:不会删除创建,只是添加元素的display:none样式,高初始渲染消耗
* 用法:频繁切换用v-show,不被用户看到用v-if

