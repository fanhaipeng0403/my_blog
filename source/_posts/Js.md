---
title: Js
date: 2017-01-11 09:20:53
tags: JavaScript

---

http://www.jb51.net/article/20428.htm

-----

用 var anObject = new aFunction() 形式创建对象的过程实际上可以分为三步2：

- 第一步是建立一个新对象；
- 第二步将该对象内置的原型对象设置为构造函数prototype引用的那个原型对象；
- 第三步就是将该对象作为this参数调用构造函数，完成成员设置等初始化工作。

-------
举个栗子:

box对象为什么可以调用addstring()方法，addstring()方法不是str对象的吗？
```
var box = new myString('Lee');
alert(box.addstring());
JavaScript 对象 函数
```
------
实际上是:
```
function myString(string){

	var attr=string;

	this.addstring=function(){

		return attr+" added";

	};

	return attr;

}
```
这样比较容易理解
