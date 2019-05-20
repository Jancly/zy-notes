---
layout: =
title: 'PHP的学习 '
date: 2018-10-06 20:13:54
toc: ture
tags:
    - 学习
    - 前端
    - php
---
> 为了学前后端的交互，和动态网页的制作，必须会一点php的应用，本章主要讲解php的基本语法
> 注意所有的php都是在服务器中运行
> 没事多来看看

<!-- more -->

## 常见的语句
### echo作用相当于页面的输出字符串
但是不能输出复杂类型
复杂输出输出有：print_r()和var_dump();

###  无论是声明变量，还是变量都要加上$符号
```
//声明变量
$str="hello word";
//输出变量
echo $str;
```
###  数字加减可用"+"，字符拼接是用".";
```
$str1 ="abc";
$str2 ="def";
$str3 = $str1.$str2;
echo = $str3;
```
###  数组
* 基础
```
$arr = array();
$arr[0]="zhangsan";
$arr[1]="lisi";
//echo不能输出复杂的类型
print_r($arr);
var_dump($arr);

echo json_encode($arr);//将数组转化为json格式
```
* 自定义数组
将下标变为自定义的字符串
```
$arr= array("name1"=>"zhangsan","name2"=>"lisi","name3"=>"wangwu");
$arr["name1"];
echo $arr["name1"];
```
代码输出：zhangsan;

* 数组遍历
方式1 for循环
```
$arr = array("zhangsan","lisi","wangwu");
for($i=0;$i<count($arr);$i++){
    $temp = $arr[$i];
    echo $temp."<br/>";

}
```
方式2 foreach   
此方法可遍历非数字角标，使用更为广泛
```
$arr= array("name1"=>"zhangsan","name2"=>"lisi","name3"=>"wangwu");
foreach($arr as $key => $value ){
    echo $key .">>>".$value."<br/>";
}
```
代码输出 ：
name1>>>zhangsan
name2>>>lisi
name3>>>wangwu
### php的函数

* 自定义函数
```
$result = add(3,5);
echo "结果为".$result;
//自定义加法
function add($num1,$num2){
  return $num1+$num2;
}
```
输出：结果为8

### php的表单验证
* get方法
```
//html:
<div class="a">
<form method="get" action="../phpfile/login.php">
<h3> 欢迎登录</h3>
<label>
    姓名：
    <input type="text" name="name" placeholder="填写bo" />
    
</label>
<br />
<label>
    密码：
    <input type="text" name="password" placeholder="密码为123" />
</label>
    <br />
    <input type="submit" value="登录" />
</form>

//php的get方法写法
$name = $_GET["name"];
	$password =$_GET["password"];
	if($name == "bo" && $password == "123" ){
		
		echo "登录成功";
	}else{
		echo "登录失败";
	}
```
* post方法
```
//html:
method="post"
//php的写法：
$name = $_POST["name"];
	$password =$_POST["password"];
	if($name == "bo" && $password == "123" ){		
	echo "Login sucess";
	}else{
	echo "登录失败";
    	}
```
自我对俩方法的认识：其实这两方法差不多，get倾向于向服务器拿数据，post倾向于向服务器发送数据。





