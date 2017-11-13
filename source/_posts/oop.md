---
title: 关于面向对象编程思想的理解
date: 2017-09-07 14:06:00
toc: true  
tags: [OOP, js]           
      
---
面向对象
=============
&nbsp;&nbsp;&nbsp;&nbsp;面向对象的思想主要以对象为主，将一个问题抽象成一个具体的对象，并将抽象出来的对象和对象的属性和方法封装成一个类。

&nbsp;&nbsp;&nbsp;&nbsp;面向对象是把构成问题的事物分解成对象，建立对象的目的不是为了要完成一个步骤，而是为了描述某个事物在整个解决问题的步骤中的行为。

&nbsp;&nbsp;&nbsp;&nbsp;实例化：在面向对象的编程中，通常把用类创建对象的过程叫做实例化

面向对象与面向过程的区别
--------------------
&nbsp;&nbsp;&nbsp;&nbsp;面向对象以名词为主，将问题抽象成具体的对象，在解决问题的时候将不同对象组合在一起。

&nbsp;&nbsp;&nbsp;&nbsp;面向过程以动词为主，主要是分析问题的解决步骤，将问题一步步实现后拼接在一起。

&nbsp;&nbsp;&nbsp;&nbsp;有一个比喻很出名也很有意思：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;面向对象：狗.吃(屎)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;面向过程：吃.(狗， 屎)

面向对象两种表达方式
=============
&nbsp;&nbsp;&nbsp;&nbsp;面向对象有两种表达方式，基于类的面向对象和基于原型的面向对象。在基于类的面向对象方式中，对象依靠类来产生。而在基于原型的面向对象方式中，对象则是依靠构造器利用原型构造出来的。

&nbsp;&nbsp;&nbsp;&nbsp;关于这两种哪个更彻底的表达了面向对象的思想目前尚有争论。我也就不发表意见了。

<div class="code">
<div class="codeHeight">
关于对象的上下文依赖（我在别的文章看到的，忘了出处了）
</div>
`
var str = "我是String对象的声明"
var obj = { des: "我是obj对象的声明" }
var fun = function () {
  console.log("我是函数对象，目前属于："， this)
};
obj.fun = fun;
console.log( this === window );  //true
console.log( window.str === str );  //true
console.log( window.obj === obj );  //true
console.log( window.fun === fun );  //true
fun();  //我是函数对象，目前属于：wimdow
obj.fun();  //我是一个函数对象，目前属于：obj
fun.apply(str);  //我是一个函数对象，目前属于：str
`
</div>

