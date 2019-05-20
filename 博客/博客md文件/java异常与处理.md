---
layout: =
title: java异常与处理
date: 2018-08-20 20:22:04
toc : true
tags:
    - 学习
    - java
    - 异常
---
关于Java中经常见到的异常
<!-- more -->
# JAVA中的异常
## 一，java中的两种异常
1.1 编译时异常：编译器会检测的异常。
例：throw new Exception(); //编译时异常
2.2 运行时异常：编译器不会检测的异常。不需要声明。声明也可以，但要让调用者给出处理方式。
例：throw new RuntimeException(); // 不需捕获，不要声明
代码：
```
public class Runtime {

	public static void main(String[] args) {
		int arr[] = { 1, 7, 9 };
		System.out.println(arr[3]);
	}
}
class Demo {
	void show() {
		// throw new Exception(); //编译时异常
		throw new RuntimeException(); // 不需捕获，不要声明
	}
}
```
<!-- more -->
## 二，声明与不声明的区别
2.1 声明：目的是为了让调用者进行处理。如果函数内通过throw抛出了编译时异常，而捕获，那么必须通过throws进行声明，让调用者去处理。
2.2 不声明:目的是不让调用者进行处理，就是为了让程序停止，让调用者看到现象，并进行代码的修正。


## 三，捕获
3.1 捕获：java中对异常有针对性的语句进行捕获。
3.2 声明与捕获：如果函数内通过throw抛出了编译时异常，而捕获，那么必须通过throws进行声明，让调用者去处理。
3.3 捕获语句：
```
try
 {
 //需要被检测的语句
 }
  catch(异常类 变量)
  {
 //异常处理的语句
 }
 finally
 {
 //一定会被执行的语句
 }
 ```

## 四，自定义异常
例：随便定义一个异常（NoAgeException）
代码：
```
public class ZiDing {

	public static void main(String[] args) {
		 Persion p  = new  Persion("肖", -20);

	}

}
class NoAgeException extends RuntimeException{
	NoAgeException(){
		super();
	}
	NoAgeException(String m){
		super(m);//如果自定义异常需要异常信息，可以通过父类带有参数的构造器即可。
	}
}
class Persion{
	private String name;
	private int age;
	 Persion(String name, int age)
	{
		if(age<0)
		{
			throw new NoAgeException(age+"，年龄数值非法");
		}
	}
	
	}
```
构造函数到底抛出这个NoAgeException是继承Exception呢还是继承 RuntimeException呢？
 * 1，继承Exception,必须要有throws声明，后调用者进行捕获，一旦问题处理了程序继续执行。
 * 2，继续RuntimeException,不需要throws声明的，没有捕获 代码，一旦NoAgeException 发生，程序终止，并有jvm将信息显示到屏幕
 上，让调用者看到问题，修正代码。
 


## 五，常见的异常
 * ArrayIndexOutOfBoundException
 * IllegalArgumetException
 * NullPointException
 * ClassCastException
 * ...

 