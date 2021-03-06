# My Own FrontEnd Note

## 1. Javascript 

### 函数

#### 函数的形态：
```js
//声明形态
function f1 () {
    console.log('hello world 1');
}

//表达形态
let f2 = function () {
    console.log('hello world 2');
}

//嵌套形态
function f3 () {
    let f4 = function() {
        console.log("hello world 3");
    }
    f4();
}

//闭包形态
function f5 (){
    return f6 = function () {
        console.log("hello world 4")
    }
}

//call:
f1();
f2();
f3();
f5()();

```

#### 函数声明的提升：
只有声明形态函数存在函数声明提升特性（ES5）

立即调用匿名函数:
```js
(function (){
    //xxx
}())

(function (){
    //xxx
})()
//这两种写法等效
```

#### 匿名函数的递归调用：
```js
(function (i){
    if (i < 3){
        arguments.callee(++i);
    }
})(1)
```
不推荐使用此种方法，严格模式下无法使用

#### 箭头函数
箭头函数无法access arguments，没有自己的super或者new.target

### 作用域
基本概念：函数作用域和全局作用域

ES6 块级作用域：
ES6为了向后兼容ES5， 其实是可以在块状{}区域外访问到声明的，只有用let才能无法在块外访问内容

意义：

更加简洁

规避var的副作用：声明提前、污染内存

### 执行上下文

执行上下文总共有三种类型：

全局执行上下文：这是默认的、最基础的执行上下文。不在任何函数中的代码都位于全局执行上下文中。它做了两件事：1. 创建一个全局对象，在浏览器中这个全局对象就是 window 对象；2. 将 this 指针指向这个全局对象。一个程序中只能存在一个全局执行上下文。
函数执行上下文：每次调用函数时，都会为该函数创建一个新的执行上下文。每个函数都拥有自己的执行上下文，但是只有在函数被调用的时候才会被创建。一个程序中可以存在任意数量的函数执行上下文。每当一个新的执行上下文被创建，它都会按照特定的顺序执行一系列步骤，具体过程将在本文后面讨论。
eval执行上下文：运行在 eval 函数中的代码也获得了自己的执行上下文，ES6 之后不再推荐使用 eval 函数，所以本书出于面试实用考虑，不会深入讨论eval。

生命周期：
a. 创建阶段
当函数被调用，但未执行任何其内部代码之前，会做以下三件事：

创建变量对象：首先初始化函数的参数 arguments，提升函数声明和变量声明（变量的声明提前有赖于var关键字）。
创建作用域链：在执行期上下文的创建阶段，作用域链是在变量对象之后创建的。作用域链本身包含变量对象。作用域链用于解析变量。当被要求解析变量时，JavaScript 始终从代码嵌套的最内层开始，如果最内层没有找到变量，就会跳转到上一层父作用域中查找，直到找到该变量。
确定 this 指向。
b. 执行阶段
创建完成之后，就会开始执行代码，在这个阶段，会完成变量赋值、函数引用、以及执行其他代码。

c. 回收阶段
函数调用完毕后，函数出栈，对应的执行上下文也出栈，等待垃圾回收器回收执行上下文。

### 变量对象
Variable Object， VO


### This
this 既不指向函数自身也不指向函数的作用域，这之前是很多前端工程师容易误解的地方，现在澄清一下。

this的指向，是在函数被调用的时候确定的，也就是执行上下文被创建时确定的；
this 的指向和函数声明的位置没有任何关系，只取决于函数的调用位置（也即由谁、在什么地方调用这个函数）；
正因为在执行上下文的创建阶段this的指向就已经被确定了，在执行阶段this指向不可再被更改。

https://coffe1891.gitbook.io/frontend-hard-mode-interview/1/1.2.3

### call apply bind
