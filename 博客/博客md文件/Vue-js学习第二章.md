---
layout: =
title: Vue.js学习第二章
date: 2018-08-26 11:03:59
toc: true
tags:
    - 学习
    - 前端
    - vue
---
Vue.js的简单了解
<!-- more -->
# vue第二章
## 一，过滤器

### 1.1普通的：
* 过滤器调用格式:
```
 {{name | 过滤器的名称 }}
```
**过滤器的function第一个参数(data),已经规定死了,永远都是过滤器管道符('|')前面传来的数据**
```
Vue.filter('过滤器的名称',function(data){
})
```
代码：
```
<p>{{msg | test}}</p>
Vue.filter('test',function(msg){
	//return msg.replace('好','坏')//只能改变第一个，
	return msg.replace(/好/g,'坏')//利用正则改变所有的
	
})
msg:"其实我是一个好人，所以你别紧张，好人是有好报的！"
```
### 1.2 可以传参的：
代码：
```
<p>{{msg | test("傻","比")}}</p>
Vue.filter('test',function(msg,arg，arg2){
	return msg.replace(/好/g,arg+arg2)//利用正则改变所有的	
})
```
 ### 1.3 添加多个过滤器：
 代码：
```
<p>{{msg | test("傻")|mvp}}</p>
Vue.filter('test',function(msg,arg){
	return msg.replace(/好/g,arg)//利用正则改变所有的
	
})
Vue.filter('mvp',function(msg){
	return msg.replace(/人/g,"比")
		})
```
### 1.4 注意
* 过滤器可以用在俩个地方：mustache插值，v-bind的表达式
* 注意过滤器的function第一个参数(data),已经规定死了,永远都是过滤器管道符('|')前面传来的数据

### 1.5局部与全局过滤器
1.  全局过滤器
全局过滤器：就是能在任意一个div使用，一般独立定义在js中
2. 局部过滤器
局部过滤器：一般定义在一个Vue中用filters:后面书写定义的方法，只能用在Vue规定的div中
3. 局部与全局的区别
区别：当俩种都有时且过滤名称相同，有先使用局部过滤器
```
<div id="c">
	<h3>{{msg|filMsg}}</h3>
</div>
<div id="c1">
	<h3>{{msg|filMsg}}</h3>
	</div>
	<script type="text/javascript">
		//全局过滤器
		Vue.filter('filMsg',function(msg){
			return msg.replace('这是','这真是')
		})			
		var vm = new Vue({
			el:"#c",
			data:{
				msg:"这是全局过滤"
			},
			methods:{					
			}				
		})
		//定义局部过滤器
		var vm2 = new Vue({
			el:"#c1",
			data:{
				msg:"这是全局过滤"
			},
			methods:{					
			},
		// 局部过滤器的方法
			filters:{
				filMsg:function(msg){
					return msg.replace('全局','局部--')
				}
			}
		})
```
代码结果为：
div#c:这真是全局过滤
div#c1:这是局部--过滤
## 二，ES6的字符串的填充
### 1.padStart
1. 格式：padStart(最大长度，'最前面添加的字符串')
2. 解释：对于字符串根据最大长度，当长度小于格式中的最大长度时，在最前面添加所要的字符串
3. 举例：
```
v:
<h2>{{star}}</h2>
vm:
star:"1".padStart(2,"0"),
```
结果为：
没添加为1，添加为01
### 2.padEnd
1. 格式：padEnd(最大长度，'最前面添加的字符串')
2. 解释：对于字符串根据最大长度，当长度小于格式中的最大长度时，在最后面添加所要的字符串
3. 举例：
```
v:
<h2>{{end}}</h2>
vm:
end:"1".padStart(2,"0"),
```
结果为：
没添加为1，添加为10
## 三，自定义按键修饰符
### 1.vue自带的修饰符
1. 全部按键别名
* .enter
* .tab
* .delete (捕获“删除”和“退格”键)
* .esc
* .space
* .up
* .down
* .left
* .right
2. 举例
```
<input v-on:keyup.enter="submit">
```
解释：当按下enter键时触发方法
3. 可以通过全局 config.keyCodes 对象自定义按键修饰符别名：
```
//全局定义变量
Vue.config.keyCodes.f1 = 112
//在v中使用
<input v-on:keyup.f1="submit">
```
[js 里面的键盘事件对应的键码](https://www.cnblogs.com/wuhua1/p/6686237.html)
## 四，自定义指令
### 一，全局指令
1.1 全局指令的写法：
**Vue.directive('指令名称',{"里面写着一些指令相关的函数"})**
解释：
//参数1：（focus即指令名称）,注意：***写参数时不需要写'-v'，但如果要调用时一定要以'v-'加指令名称***
//参数2：为一个对象，这个对象上有一些指令相关的函数
1.2 例子：
```
v:
<input type="text" name="" id="" value="" v-color/>
vm:
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```

1.3 钩子函数
 * bind: 未插入到Dom中时进行的操作，即初始化，一般用样式比较多，（只执行一次）
 * inserted: 已插入到dom时执行函数，一般用于和js相关操作（执行一次）
 * update ：当VNode更新的时候会执行，可能触发多次
 下面了解：
* componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
* unbind：只调用一次，指令与元素解绑时调用。

1.4 钩子函数的参数（ el、binding、vnode 和 oldVnode）
* el:
**注意** 每一个函数第一个参数永远是'el',是一个原生JS对象可直接操控Dom
* binding: 指令对象
所属属性有：
name：指令名，不包括 v- 前缀。
value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。
oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
可以了解：
* vnode:
Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。
* oldVnode：
上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。
### 二，局部（私有）指令
2.1，局部指令写法：
```
directives: {//定义私有指令
	color: {
		inserted: function(el) {
			el.style.color="blue"
		}
	}
}
```
写法与filter相似，其他的和全局指令相同
### 三，指令的简写
1.  **条件：一定是在bind和update**
2. 代码比较
```
//一般写法
	/*Vue.directive('fontsize',{
		bind:function(el,binding){
			el.style.fontSize= binding.value
		}	
	})*/
	//简写
	Vue.directive('fontsize',function(el,binding){
		el.style.fontSize=binding.value//传的是字符串如："'70px'"	
	})			
```
## 五，Vue生命周期讲解
### 5.1 生命周期定义
定义：从Vue实例的创建，运行到销毁期间，伴随各种事件，这些事件总称为生命周期。
### 5.2 生命周期钩子解释
解释：生命周期事件的别名
生命周期函数 = 声明周期事件 = 生命周期钩子

### 5.3 生命周期示意图
![](https://xfbxfbxfb.github.io/picture/img/vue%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)
### 5.4 生命周期的三个时期函数
1. 创建期
* beforeCreate：实例创建出来之前执行它，此时data和methods还没初始化，不能调用
* created：此时data和methods已初始化，要调用data数据和methods的方法最早在created实现
* beforeMount：此时模板已编译，但数据还未更新上去
解释：
```
v:
<p style="font-size: 50px;" id="p">{{msg}} </p>
vm:
beforeMount(){
	//console.log(document.getElementById("p").innerText)
	//beforeMount执行的时候模板还没替换过来，只是之前写的字符串
},
```
输出结果：{{msg}}，此时的data数据中的msg还未放到页面上去
* mounted: 此时模板已编译好数据已放到上面去了
2. 运行期
* beforeUpdate: 更新前执行此函数，data数据是已更新，但页面数据是旧的还未渲染到Dom节点上去
* updated：更新完毕执行，数据已更新，页面已渲染
3. 销毁期
* beforeDestroy:销毁前执行，实例依旧可用
* destroyed: 实例销毁后调用

