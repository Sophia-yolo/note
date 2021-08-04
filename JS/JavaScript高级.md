# 基础总结深入

## 数据类型的分类和判断

### 数据类型的分类

数据类型分类

* 基本(值)类型
  * Number ----- 任意数值 -------- ==typeof==
  * String ----- 任意字符串 ------ ==typeof==
  * Boolean ---- true/false ----- ==typeof==
  * undefined --- undefined ----- ==typeof==/`===`
  * null -------- null ---------- `===`
* 对象(引用)类型
  * Object ----- ==typeof/instanceof==
  * Array ------ ==instanceof==
  * Function ---- ==typeof==

### 数据类型判断

typeof

1. 返回数据类型的==字符串表达==；

   ```js
   var a;
   console.log(typeof a) // 'undefined'
   ```

2. 可以区别：数值、字符串、布尔值、undefined、function；

3. 不能区别：null与object、一般object与array。

instanceof

> 是否是该构造函数的实例

- 专门用来判断对象数据的类型：Object、Array与Function。

**===**

- 可以判断：undefined和null。



![img](https://img-blog.csdnimg.cn/20210125142526467.png)

![img](https://img-blog.csdnimg.cn/20210125144616228.png)

### 变量类型数据类型

> js的变量本身是没有类型的，变量的类型实际上是变量内存中数据的类型（js是弱类型的语言）。var a; 判断变量类型，实际上 是判断值的类型。

数据的类型（数据对象）：

1. 基本类型
2. 对象类型

变量的类型（变量内存值的类型）：

   * 基本类型：保存基本类型的数据（保存基本类型数据的变量）。
   * 引用类型：保存对象地址值（保存对象地址值的变量）。



### 相关问题

#### 实例

> 使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类。我们将通过一个构造函数创建的对象，称为是该类的实例。

#### undefined与null的区别？

> undefined代表定义未赋值；null==定义并赋值==，只是值为null。
>
> ![img](https://img-blog.csdnimg.cn/20210125191350603.png)

#### 什么时候变量赋值为null呢？

1. 初始赋值，表明将要赋值为对象；(将要作为引用变量使用, 但对象还没有确定)
2. 结束前，让对象成为垃圾对象（被垃圾回收器回收）。

```js
var a = null 	// a将指向一个对象，但对象此时还没有确定
a = null 	// 让a指向的对象成为垃圾对象
```

![img](https://img-blog.csdnimg.cn/20210125191816377.png)





## 数据 & 变量 & 内存

#### 数据

>  \* 算术运算
>  \* 逻辑运算
>  \* 赋值
>  \* 运行函数（调用函数传参）
>  ...

* 数据的特点：具有可读、可传递、可运算的基本特性。
* 一切皆数据, 函数也是数据
* 在内存中的所有操作的目标: 数据

#### 变量

- 在程序运行过程中它的值是允许改变的量

* 一个变量对应一块小内存, 它的值保存在此内存中  

#### 内存

> 内存产生和死亡: 
>
> - 内存条(集成电路板)——>通电——>产生一定容量的存储(内存)空间——>存储各种数据——>处理数据——>断电——>内存和数据全部消失
>
> 内存的空间是临时的, 而硬盘的空间是持久的

* 内存条通电后产生的存储空间(临时的)
* 一块内存包含2个方面的数据
  * 内部存储的数据(一般数据/地址数据)
  * 地址值数据
* 内存空间的分类
  * 栈空间: 全局变量和局部变量 (空间较小)
  * 堆空间: 对象  (空间较大)

#### 三者之间的关系

* 内存是容器, 用来存储不同数据
* 变量是内存的标识, 通过变量我们可以操作(读/写)内存中的数据  

#### 相关问题

> 情况讨论：var a = xxx（赋值操作），a内存中到底保存的是什么？
> 问题：var a = xxx（赋值操作），a内存中到底保存的是什么？

1. xxx是一个基本数据，保存的就是这个数据。
2. xxx是一个对象，保存的是对象的地址值。
3. xxx是一个变量，保存的xxx的内存内容（保存的可能是基本数据，也可能是地址值数据）。

> 关于引用变量赋值问题

- 2个引用变量指向同一个对象（保存的内容是同一个对象的地址值），通过一个引用变量修改对象内部数据，另一个引用变量也看得见（看见的是修改之后的数据）。

  ```js
  var obj1 = { name: "Tom"}
  var obj2 = obj1
  obj1.name = "张三"
  console.log(obj2.name)	//打印输出 "张三"
  
  function fn(obj){
      obj.name = "李四"
  }
  fn(obj2)
  console.log(obj1.name)	//打印输出 "李四"
  ```

- 2个引用变量指向同一个对象，让一个引用变量指向另一个对象，另一个引用变量还是指向原来的对象

  ```js
  var a = { age: 12}
  var b = a 
  a = { name:"张三",age:14 }
  b.age = 18
  console.log( b.age, a.name, a.age)	//打印输出 18 "张三" 14
  
  function fn(obj){
      obj = { age: 66 }
  }
  fn(b)
  console.log(b.age)	//打印输出 18
  ```





## 函数

> 用来实现特定功能的, n条语句的封装体，只有函数类型的数据是可以执行的, 其它的都不可以

为什么要用函数?

* 提高复用性
* 便于阅读交流

函数也是对象——`Function instanceof Object===true`

函数的3种不同角色

* 一般函数 : 直接调用  ==test()==
* 构造函数 : 通过new调用   ==new test()==
* 对象(==obj.test()==) : 通过调用内部的属性/方法   ==test.call/apply(obj)==

### 回调函数

> 回调函数 ： 函数作为一个参数传到另一个函数里面，当那个函数执行完之后，在执行传进去的这个函数，这个过程就叫做回调
>
> 1. 你定义de
> 2. 没有调用函数
> 3. 最终执行（在某个时刻或某个条件下）

##### dom事件回调函数

> PS：this ==》发生事件的dom元素

```js
document.getElementById('btn').onclick = function (){
	alert(this.innerHTML)
}
```

##### 定时器回调函数

> PS：this ==》window

```js
setTimeout(function (){
	alert("到点了")
},2000)
```

###### window.setTimeout

- 用法：window.setTimeout(调用函数,延时时间)=>回调函数
- 延时时间单位是毫秒，但可以省略，省略默认为0
- 页面中可能有很多定时器，我们经常给定时器==赋值标识符==
- 停止定时器：window.clearTimeout(timeout ID)
- 延时时间到了，就去调用这个回调函数，只调用一次，然后结束这个定时器

###### setInterval(回调函数，[间隔的毫秒数])

> 每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用

##### ajax请求回调函数

##### 生命周期回调函数



### 具名函数（命名函数）

```js
var fn1=function xxcanghai(){};
```

> 注意：具名函数表达式的函数名只能在创建函数内部使用



### 匿名函数

```js
var fn1=function (){};
getFunctionName(fn1).length;//0
```



### 立即执行函数表达式(IIFE)

> 别名：匿名函数自调用（不需要调用）

1. 写法：


```js
//第一种
(function(){
    
})()
```

```js
//第二种
(function(){
    
}())
```

2. 作用：

> 1. 隐藏实现
> 2. 不会污染外部(全局)命名空间



### this

this：指向问题，一般情况下最终指向调用它的对象

1. 全局作用域或者普通函数中this指向全局对象`window`（定时器里的this指向window）

2. 任何函数本质上都是通过某个对象来调用的，如果没有直接指定就是window

3. 方法调用中谁**调用**this指向谁

   > - `call(obj)`指向obj
   > - `apply(obj)`：指向obj

4. 构造函数中this指向构造函数的实例（类中(函数体中)出现的 `this.xxx=xxx` 中的 this 是当前类的一个实例）



## 分号问题

不加分号有问题：

1. 小括号开头的前一条语句（立即执行函数）
2. 中方括号开头的前一条语句





# 函数高级

## 原型与原型链

### 原型 prototype

函数的prototype属性：

1. 每个函数都有一个prototype属性，它默认指向一个Object空对象（即称为：==原型对象==）

2. 原型对象中有一个属性constructor，它指向==函数对象==

   ```js
   console.log(Object.prototype.constructor === Object);	//true
   ```

给原型对象添加属性（一般是方法）===》实例对象可以访问

> 作用：函数的所有实例对象自动拥有原型中的属性（方法）



### 显示原型与隐式原型

prototype和`__proto__`为引用变量

1. 每个函数function都有一个`prototype`，即==显式原型==（属性）

   > 函数的prototype: 定义函数时被自动赋值, 值默认为{}, 即用为原型对象

2. 每个实例对象都有一个`__proto__`，可称为==隐式原型==（属性）

   > 实例对象的`__proto__`: 在创建实例对象时被自动添加, 并赋值为构造函数的prototype值

3. **对象**的==隐式原型的值==为**其对应构造函数**的==显式原型的值==    原型对象即为当前实例对象的父对象

   ```js
   function Fn(){
   	...
   }
   var fn = new Fn()
   console.log(Fn.prototype === fn.__proto__);	 //true
   ```

4. 内存结构

   ![image-20210730185957787](https://i.loli.net/2021/07/30/5hPZ7tJSIWs6Bua.png)

   

### 原型链

> 访问一个对象的属性时，先在自身属性中查找， 如果找到就返回，如果没找到，沿着`__proto__`这条链向上找，直到找到就返回，如果没找到，返回undefined

==“隐式原型链”==——作用：查找对象属性/ 方法

![image-20210730200148183](https://i.loli.net/2021/07/30/lf9FpCGrouUMb3E.png)

> Object的原型对象是原型链的尽头
>
> ```js
> fn ==> Fn.prototype ==> Object.prototype ==> null
> ```



#### 构造函数/原型/实例对象的关系（图解）

```js
var o1 = new Object()
var o2 = {}
```

![【5】JavaScript 函数高级——原型与原型链深入理解（图解）](https://img1.3s78.com/codercto/2efe759d3957b955f0f3540bb68c9116)



#### 构造函数/原型/实例对象的关系2（图解）

```js
function Foo(){  }
```

上述代码的等价关系：

![image-20210730232509331](https://i.loli.net/2021/07/30/FtworiA9T8vUg3a.png)

![JavaScript 函数高级——原型与原型链深入理解（图解）](https://i.loli.net/2021/07/30/jYoxLh2HvzIE3w4.png)

#### 原型继承

- 构造函数的实例对象自动拥有构造函数原型对象的属性（方法）
- 利用的就是原型链

#### 原型链——属性问题

- ==读取==对象的属性值时：会自动到原型链中查找
- ==设置==对象的属性值时：==不会查找原型链==，如果当前对象中没有此属性，直接添加此属性并设置其值
- 方法一般定义在原型中，属性一般通过构造函数定义在对象本身上。

#### 总结

函数的显式原型指向的对象默认是空Object实例对象（但Object不满足）

```js
	function Fn(){ }
    console.log(Fn.prototype instanceof Object);    //true
    console.log(Object.prototype instanceof Object);    //false
    console.log(Function.prototype instanceof Object);  //true
```

所有函数都是 Function实例

```js
console.log(Function.__proto__ === Function.prototype)	//true
```

Object 的原型对象是原型链的尽头

```js
console.log(Object.prototype.__proto__)	//null
```



### 思考题

#### 🌰一

```js
var A = function() { }
A.prototype.n = 1
var b = new A()
A.prototype = {
  n: 2,
  m: 3
}
var c = new A()
console.log(b.n, b.m, c.n, c.m) // 1 undefined 2 3
```

![image-20210731010607600](https://i.loli.net/2021/07/31/gVAD7scoY6BrnmE.png)

#### 🌰二

```js
var F = function(){};
Object.prototype.a = function(){
  console.log('a()')
};
Function.prototype.b = function(){
  console.log('b()')
};
var f = new F();
f.a() // a()
f.b() // 报错  f.b is not a function
F.a() // a()
F.b() // b()
```

参考下图：

![【5】JavaScript 函数高级——原型与原型链深入理解（图解）](https://img1.3s78.com/codercto/c1ea1c13c1cd0ca65d88d3f2f5f8e8da)



## instanceof

表达式： `A instanceof B`

> 如果 `B` 函数的显式原型对象在 `A` 对象的(隐式)原型链上（简单来说就是判断A 是不是 B 的实例），返回 true ，否则返回 false

Function 是通过 `new` 自己产生的实例

### 案例一

```js
function Foo() {  }
var f1 = new Foo();
console.log(f1 instanceof Foo);	//true
console.log(f1 instanceof Object);	//true
```

![【5】JavaScript 函数高级——原型与原型链深入理解（图解）](https://img1.3s78.com/codercto/424e524fa4e11405e868258e8c77cf62)



### 案例二

```js
console.log(Object instanceof Function); // true 
console.log(Object instanceof Object); // true 
console.log(Function instanceof Function); // true 
console.log(Function instanceof Object); // true 

function Foo() {} 
console.log(Object instanceof Foo); // false
```

![【5】JavaScript 函数高级——原型与原型链深入理解（图解）](https://img1.3s78.com/codercto/c1ea1c13c1cd0ca65d88d3f2f5f8e8da)

> 注意： `Function` 的显示原型和隐式原型是一样的。









## 执行上下文与执行上下文栈

### 变量提升与函数提升

变量提升: 在==变量定义==语句之前, 就可以访问到这个变量(undefined)

```js
var a = 3
function fn(){
    console.log(a);	//undefined
    var a = 4
}
fn()
```

函数提升: 在==函数定义==语句之前, 就执行该函数

> 先有变量提升, 再有函数提升

### 执行上下文

* 执行上下文: 由js引擎自动创建的对象, 包含对应作用域中的所有变量属性
* 执行上下文栈: 用来管理产生的多个执行上下文

执行上下文数（最多）：n+1

1. window（1）
2. 函数的调用（n）

#### 执行上下文的生命周期

执行上下文的生命周期包括三个阶段：==创建阶段 → 执行阶段 → 回收阶段==

##### 1. 创建阶段

当函数被调用，但未执行任何其内部代码之前，会做以下三件事：

- 创建变量对象：首先初始化函数的参数 arguments，提升函数声明和变量声明。

- 创建作用域链（Scope Chain）：在执行期上下文的创建阶段，作用域链是在变量对象之后创建的。作用域链本身包含变量对象。作用域链用于解析变量。当被要求解析变量时，JavaScript 始终从代码嵌套的最内层开始，如果最内层没有找到变量，就会跳转到上一层父作用域中查找，直到找到该变量。

- 确定 this 指向

  ![img](https://image.fundebug.com/2019-03-19-01.png)

> 在一段 JS 脚本执行之前，要先解析代码（所以说 JS 是解释执行的脚本语言），解析的时候会先创建一个全局执行上下文环境，先把代码中即将执行的变量、函数声明都拿出来。变量先暂时赋值为 undefined，函数则先声明好可使用。这一步做完了，然后再开始正式执行程序。

另外，一个函数在执行之前，也会创建一个函数执行上下文环境，跟全局上下文差不多，不过 函数执行上下文中会多出 this arguments 和函数的参数。

##### 2. 执行阶段

执行变量赋值、代码执行

##### 3. 回收阶段

执行上下文出栈等待虚拟机回收执行上下文



#### 全局执行上下文

> 生命周期：准备执行全局代码前产生, 当页面刷新/关闭页面时死亡

###### 执行上下文创建和初始化的过程

1. 在全局代码执行前最先创建一个全局执行上下文：window

2. 对全局数据进行==预处理==（收集一些全局变量, 并初始化，将这些变量设置为window的属性）

   > * 用var定义的全局变量  ==>undefined
   > * 使用function声明的函数   ===>function
   > * this   ===>window

3. 开始执行全局上下文



#### 函数执行上下文

> 生命周期：调用函数时产生, 函数执行完时死亡

###### 执行上下文创建和初始化的过程

1. 在调用函数时, 在执行函数体之前先创建一个函数执行上下文对象（虚拟的，存在于栈中）

2. 对局部数据进行==预处理==（收集一些局部变量, 并初始化，将这些变量设置为执行上下文的属性）

   > * 用var定义的局部变量  ==>undefined
   > * 使用function声明的函数   ===>function
   > * this   ===> 调用函数的对象, 如果没有指定就是window 
   > * 形参变量   ===> 对应实参值
   > * arguments ===>实参列表的伪数组

3. 开始执行函数体代码

###### 🌰：

```js
function fn(a1){
    console.log(a1);
    console.log(a2);
    a3()
    console.log(this);
    console.log(arguments);		//伪数组

    var a2 = 3
    function a3(){
        console.log("a3()");
    }
}

fn(2,3)
```

输出结果：

![image-20210731110225139](https://i.loli.net/2021/07/31/Ov94jSRfMaB62cF.png)



##### 流程分析

```js
var a = 10
var bar = function (x) {
	var b = 5
	foo(x + b)              
}

var foo = function (y) {
	var c = 5
	console.log(a + c + y)
}

bar(10)  
```

![image-20210731112715073](https://i.loli.net/2021/07/31/KWUsvgb9H2ftYcE.png)



### 思考题

#### 🌰一

```js
console.log('global begin：' + i);
var i = 1;
foo(1)
function foo(i) {
    if(i == 4){
        return
    }
    console.log('foo() bagin：' + i);
    foo(i + 1)  //递归调用，在函数内部调用自己
    console.log('foo() end：' + i);
}
console.log('global end：'+ i);
```

输出结果：

![](https://i.loli.net/2021/07/31/QBfPRsbLgoSWD82.png)



#### 🌰二

```js
function a() {}
var a;
console.log(typeof a)	//function
```

> 知识点：先执行变量提升，在执行函数提升



#### 🌰三

```js
if (!(b in window)) {
    var b = 1;
}
console.log(b)		//undefined
```



#### 🌰四

```js
var c = 1
function c(c) {
console.log(c)
	var c = 3
}

c(2)
```

  结果：

![image-20210731122920612](https://i.loli.net/2021/07/31/UygoD4WdG3xZSbP.png)



## 作用域与作用域链

### 理解

* 作用域: 一块代码区域, 在编码时就确定了, 不会再变化
* 作用域链: 多个嵌套的作用域形成的由内向外的结构, 用于查找变量

### 作用域个数

==n+1==

- window（1）
- 函数定义个数（n）

### 分类

* 全局作用域
* 函数作用域
* js没有块作用域(在ES6之前)

### 作用

* 作用域: 隔离变量, 可以在不同作用域定义同名的变量不冲突
* 作用域链: 查找变量

* 区别作用域与执行上下文
  * 作用域: 静态的, 编码时就确定了(不是在运行时), 一旦确定就不会变化了
  * 执行上下文: 动态的, 执行代码时动态创建, 当执行结束消失
  * 联系: 执行上下文环境是在对应的作用域中的

### 思考题

#### 🌰一

```js
var x = 10;
function fn() {
    console.log(x);
}

function show(f) {
    var x = 20;
    f();
}

show(fn);	//输出 10
```

分析：

![image-20210731165538109](https://i.loli.net/2021/07/31/4UIzftMJxoy5elq.png)



#### 🌰二

```js
var fn = function () {
    console.log(fn)
}
fn()

var obj = {
    fn2: function () {
        console.log(fn2)
    }
}
obj.fn2()
```

![image-20210731165832510](https://i.loli.net/2021/07/31/A7r8EK5CHwDlJP9.png)



## 闭包

### 含义

* 当一个嵌套的内部(子)函数引用了嵌套的外部(父)函数的变量(函数)时, 就产生了闭包

* 通过chrome工具得知: 闭包本质是内部函数中的一个对象, 这个对象中包含引用的变量属性

  >  注意: 闭包存在于嵌套的内部函数中

```js
//函数fn2就被包括在函数fn1内部
//这时fn1内部的所有局部变量，对fn2都是可见的。但是反过来就不行，fn2内部的局部变量，对fn1就是不可见的。
function fn1(){
    var a = 2
    var b = 'abc'
    function fn2(){
        console.log(a);
    }
    //既然fn2可以读取fn1中的局部变量，那么只要把fn2作为返回值，我们就可以在fn1外部读取它的内部变量了
    //return fn2
    fn2()
}
fn1()
```

> 这里有一个地方需要注意，函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量！

这里面确实有闭包，a 变量和 fn2 函数就组成了一个闭包（Closure）。

![image-20210731171503008](https://i.loli.net/2021/07/31/IASEVt6Y4oQv2uD.png)

![image-20210731171617484](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210731171617484.png)



### 常见的闭包

####  ① 将函数作为另一个函数的返回值

```js
// 1. 将函数作为另一个函数的返回值
 function fn1() {
   var a = 2
   function fn2() {
     a++
     console.log(a)
   }
   return fn2
 }
 var f = fn1()
 f() // 3
 f() // 4
```

#### ② 将函数作为实参传递给另一个函数调用

```js
// 2. 将函数作为实参传递给另一个函数调用
 function showDelay(msg, time) {
   setTimeout(function () {
     alert(msg)
   }, time)
 }
 showDelay('atguigu', 2000)
```



### 作用

##### 小案例分析

假设我们在做一个游戏，在写其中关于「还剩几条命」的代码。

如果不用闭包，你可以直接用一个全局变量：

```text
window.lives = 30 // 还有三十条命
```

这样看起来很不妥。万一不小心把这个值改成 -1 了怎么办。所以我们不能让别人「直接访问」这个变量。怎么办呢？==用局部变量==。

但是用局部变量别人又访问不到，怎么办呢？

解决办法：暴露一个访问器（函数），让别人可以「间接访问」。

代码如下：

```js
!function(){
  var lives = 50
  
  window.奖励一条命 = function(){
    lives += 1
  }

  window.死一条命 = function(){
    lives -= 1
  }
}()
```

那么在其他的 JS 文件，就可以使用 window.奖励一条命() 来涨命，使用 window.死一条命() 来让角色掉一条命。

看到闭包在哪了吗？

![img](https://pic4.zhimg.com/80/v2-89bf8b72fb612a1e2f348ed0b3e0689f_720w.jpg)

##### 总结

- 延长局部变量的生命周期（让这些变量的值始终保持在内存中。）

* 让函数外部能操作内部的局部变量

* 写一个闭包程序

  ```js
  function fn1() {
    var a = 2;
    function fn2() {
      a++;
      console.log(a);
    }
    return fn2;
  }
  var f = fn1();
  f();	//3
  f();	//4
  f = null //闭包灭亡(包含闭包的函数对象成为垃圾对象)
  ```


> 在这段代码中，f 实际上就是闭包 fn2 函数，它一共运行了两次。这证明了，函数 fn1 中的局部变量 a 一直保存在内存中，并没有在 fn1 调用后被自动清除。
>
> > 原因就在于==fn1==是==fn2==的父函数，而fn2被赋给了一个全局变量，这导致==fn2始终在内存中==，而f2的存在依赖于f1，因此==fn1也始终在内存中==，不会在调用结束后，被垃圾回收机制（garbage collection）回收。



### 闭包的生命周期

产生: 在嵌套内部函数定义执行完时就产生了(不是在调用)

死亡: 在嵌套的内部函数成为垃圾对象时

> 即没有人指向它时死亡,通常置为[`null`],当然指向其他也行,但不安全(容易污染变量)

```js
//闭包的生命周期
function fn1() {
   //此时闭包就已经产生了(函数提升,实际上[fn2]提升到了第一行, 内部函数对象已经创建了)
   var a = 2
   function fn2 () { //如果时[let fn2=function(){}],那么在这行才会产生闭包
     a++
     console.log(a)
   }
   return fn2
 }
 var f = fn1()
 f() // 3
 f() // 4
 f = null //闭包死亡(包含闭包的函数对象成为垃圾对象)
```



### 闭包应用

#### 定义JS模块

模块定义：

> 1. 具有特定功能的js文件
> 2. 将所有的数据和功能都封装在一个函数内部(私有的)
> 3. 只向外暴露一个包信n个方法的对象或函数
> 4. 模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能

- 模块化: 封装一些数据以及操作数据的函数, 向外暴露一些行为

  ```js
  (function (window){
  	var msg = "hello"
  	
  	function f1(){
  		console.log(msg.toUpperCase())
  	}
  	
  	function f2(){
  		console.log(msg.toLowerCase(0))
  	}
  	
  	window.myModule = {
  		f1: f1,
  		f2: f2
  	}
  })(window)
  
  ————————————————————— 模块的调用 ————————————————————————————
  <script type="text/javascript" src="myModule2.js"></script>
  <script type="text/javascript">
    myModule2.doSomething()
    myModule2.doOtherthing()
  </script>
  ```

* 循环遍历加监听
* JS框架(jQuery)大量使用了闭包



#### 缺点

* 变量占用内存的时间可能会过长
* 可能导致内存泄露

###### 解决

* 及时释放 : f = null; //让内部函数对象成为垃圾对象
* 调用时直接`f()()`直接运行调用即可-->匿名函数,用完自动就销毁了

###### 使用闭包的注意点

> 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。



### 内存溢出与内存泄露

##### 内存溢出

> 一种程序运行出现的错误：当程序运行需要的内存超过了剩余的内存时, 就出抛出内存溢出的错误

##### 内存泄露

  * 占用的内存没有及时释放
  * 内存泄露积累多了就容易导致内存溢出
  * 常见的内存泄露:
    * 意外的全局变量
    
      > 函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量！
    
    * 没有及时清理的计时器或回调函数
    
    * 闭包



### 垃圾回收机制

> 内存泄漏 👉堆栈溢出 👉 垃圾回收机制

#### 自动清理

> 将所有引用堆中地址的对象都设置为null，并且将所有引用该地址的对象都设置为null，不会即时清除，垃圾回收车会根据内存的情况在适当的时候清除堆中的孤儿对象。



### 思考题

#### 🌰一

```js
var name = "The Window";

var object1 = {
    name : "My Object",
    getNameFunc : function(){
      return function(){
        return this.name;
      };
    }
};
//直接执行函数指向 window，不构成闭包
alert(object1.getNameFunc()());		// 输出 The Window

var object2 = {
    name : "My Object",
    
    getNameFunc : function(){
      var that = this;
      return function(){
        return that.name;
      };
    }
};

alert(object2.getNameFunc()());		 //输出 The My Object
```





#### 🌰二

```js
function fun(n,o) {
    console.log(o)
    return {
        fun:function(m){
        	return fun(m,n);
        }
    };
}

var a = fun(0);  a.fun(1);  a.fun(2);  a.fun(3);	//undefined,0,0,0
var b = fun(0).fun(1).fun(2).fun(3);				//undefined,0,1,2
var c = fun(0).fun(1);  c.fun(2);  c.fun(3);		//undefined,0,1,1
```

> 注：当调用函数的时候传入的实参比函数声明时指定的形参个数要少，剩下的形参都将设置为undefined值。

执行`a.fun(0);`：返回一个对象

![image-20210731213815338](https://i.loli.net/2021/07/31/I6bJGRLmCu1OMTy.png)

执行`a.fun(1);`：传入1，重新执行 fun(m, n)，这是m为我们传入的1，代码如下、：

```js
{
    fun:function(1){
        return fun(1,0);
    }
}
```

```js
 function fun(n,o){ //n的值为1，o的值为0
        console.log(o);
        return {
            fun:function(m){
                return fun(m,n);//n的值为1
            }
        };
}
fun(1,0);  
//输出0，并返回一个对象，这个对象有一个fun的方法,这个方法调用后，会返回外层fun函数调用的结果，并且外层函数的第二个参数是 n 的值，也就是1  
```

> 因为用 a 接受了fun的返回值，形成闭包，所以下面两个还是0，和上面的分析基本相同，虽然传入的值发生改变，但是由于取得是之前传入的0，所以输出的都是0；

b和a的不同在于，var a = fun(0); 之后一直用的是a这个对象，是同一个对象，而b每次用的都是上次返回的对象。

> fun(0).fun(1).fun(2) ==>>>  这里传入m=2时，继承上一步n已经为1，**（m,n）为2,1，重新进入时，n,o为,2,1**输出o为1；

如果改成这样：

```js
//把返回的对象，重新赋值给a，这样两行的结果就是一样的了。
var a = fun(0); a=a.fun(1); a=a.fun(2); a=a.fun(3);
var b = fun(0).fun(1).fun(2).fun(3);
```





# 对象高级

## 对象的创建模式

##### Object构造函数模式

- 先创建空Object 对象，再动态添加属性/ 方法

> 使用场景：起始时不确定对象内部数据（问题：语句太多）

```js
var obj = {};
obj.name = 'Tom'
obj.setName = function(name){
    this.name=name
}
```

##### 对象字面量模式

- 使用 `{}` 创建对象，同时指定属性、方法

> 使用场景：起始时对象内部数据是确认的（若创建创建多个对象，有重复代码）

```js
var obj = {
  name : 'Tom',
  setName : function(name){this.name = name}
}
```

##### 工厂模式（了解即可）

- 通过工厂函数动态创建对象并返回

> 使用场景：需要创建多个对象（对象没有一个具体的类型，都是Object类型）

```js
function createPerson(name,age) {		//工厂函数
	var obj = {
		name: name,
		age: age,
		setName: function (name){
			this.name = name
		}
	}
	return obj
}

var p1 = createPerson("Tom",12)
var p2 = createPerson("Bob",13)
```

##### 构造函数模式

- 自定义构造函数, 通过new创建对象

> 适用场景: 需要创建多个类型确定的对象（ 每个对象都有相同的数据, 浪费内存）

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.setName = function(name){this.name=name;};
}
new Person('tom', 12);
```

##### 构造函数+原型的组合模式

- 自定义构造函数, 属性在函数中初始化, 方法添加到原型上

> 适用场景: 需要创建多个类型确定的对象

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.setName = function(name){this.name=name;};
new Person('tom', 12);
```



## 继承模式

### 原型链继承 

> 得到方法

```js
//父类型
function Supper(){			// 1. 定义父类型构造函数
    this.supProp = 'Supper property'
}
Supper.prototype.showSupperProp = function(){		// 2. 给父类型的原型添加方法
    console.log(this.supProp);
}

//子类型
function Sub(){			// 3. 定义子类型的构造函数 
    this.subProp = 'Sub proterty'
}
//子类型的原型为父类型的实例对象
Sub.prototype = new Supper()		// 4.创建父类型的对象赋值给子类型的原型,子类型的原型指向父类型实例
Sub.prototype.constructor = Sub		// 5. 将子类型原型的构造属性设置为子类型
Sub.prototype.showSubProp = function(){			// 6. 给子类型原型添加方法
    console.log(this.subProp);
}
var sub = new Sub()			// 7. 创建子类型的对象: 可以调用父类型的方法
```

分析图：

![image-20210731235652684](https://i.loli.net/2021/08/01/KFVhst9alEIJQ35.png)

对于`Sub.prototype.constructor = Sub`的解释：

如果不指定，则其构造函数找的 new Supper() 是从顶层Object继承来的构造函数,指向`Supper()`

![image-20210801014827238](https://i.loli.net/2021/08/01/6XphW72eLlnFaxQ.png)

### 借用构造函数 

> 得到属性

```JS
function Parent(xxx){		// 1.  定义父类型构造函数
    this.xxx = xxx
}		
Parent.prototype.test = function(){};
function Child(xxx,yyy){			// 2.  定义子类型构造函数
    Parent.call(this, xxx);//借用构造函数   this.Parent(xxx)
    this.yyy = yyy
}
var child = new Child('a', 'b');  //child.xxx为'a',child.yyy为'b', 但child没有test()
```

### 组合继承

> 原型链+借用构造函数的组合继承

1. 利用原型链实现对父类型对象的方法继承
2. 利用super()借用父类型构建函数初始化相同属性

```JS
function Parent(xxx){
    this.xxx = xxx
}
Parent.prototype.test = function(){};
function Child(xxx,yyy){
    Parent.call(this, xxx);//借用构造函数   this.Parent(xxx)
    this.yyy = yyy
}
Child.prototype = new Parent(); //得到test()
Child.prototype.constructer = Child		//修正constructor属性
Child.prototype.text2 = function() { }
var child = new Child('a', 'b'); //child.xxx为'a',child.yyy为'b',也有test(),text2()
```

new一个对象背后做了些什么?
* 创建一个空对象
* 给对象设置`__proto__`, 值为构造函数对象的prototype属性值   `this.__proto__ = Fn.prototype`
* 执行构造函数体(给对象添加属性/方法)





# 线程机制与事件

## 线程与进程

![1](https://i.loli.net/2021/08/02/CjBy8IaplMmcVsf.png)

### 进程

* 程序的一次执行, 它占有一片独有的内存空间
* 可以通过windows任务管理器查看进程

### 线程

* 是进程内的一个独立执行单元
* 是程序执行的一个完整流程
* 是CPU的最小的调度单元

### 关系

> 程序是在某个进程中的某个线程执行的

1. 应用程序必须运行在某个进程的某个线程上
2. 一个进程中至少有一个运行的线程:==主线程 ==-->进程启动后自动创建
3. 一个进程中也可以同时运行多个线程；此时我们会说这个程序是多线程运行的
4. 多个进程之间的数据是不能直接共享的 -->内存相互独立(隔离)
5. `线程池(thread pool)`:保存多个线程对象的容器,实现线程对象的反复利用

### 引出的问题

#### ① 何为多进程与多线程?

> 多进程运行: 一应用程序可以同时启动多个实例运行
>
> 多线程: 在一个进程内, 同时有多个线程运行

#### ②比较单线程与多线程?

##### 多线程

优点：能有效提升CPU的利用率

> 缺点：
>
> - 创建多线程开销
> - 线程间切换开销
> - 死锁与状态同步问题

##### 单线程

- 优点：顺序编程简单易懂
- 缺点：效率低

#### ③ JavaScript 是单线程还是多线程?

> JS是单线程运行的 , 但使用H5中的 Web Workers可以多线程运行
>

- 只能由一个线程去操作DOM界面



## 定时器引发的思考

##### 定时器真是定时执行的吗？

> 定时器并不能保证真正定时执行
> 一般会延迟一丁点（可以接受），也有可能延迟很长时间（不能接受）

##### 定时器回调函数是在分线程执行的吗？

> 在主线程执行的，js是单线程的
>

##### 定时器是如何实现的？

> 事件循环模型
>

```js
<button id="btn">启动定时器</button>
<script>
    document.getElementById('btn').onclick = function(){
    	//获取当前时间
        var start = Date.now()
        console.log('启动定时器前...')
        setTimeout（function(){
            console.log('定时器执行了'，Date.now()-start) //定时器并不能保证真正定时执行！
        },200）
        console.log('启动定时器后')  
    }
	//时间长的任务
	for(var a = 0;a < 1000000;a++){
        
    }
</script>
```





## js线程

##### 如何证明js执行时单线程的？

> - setTimeout（）的回调函数是在主线程执行的
> - 定时器回调函数只有在运行栈中的代码全部执行完之后才有可能执行

##### 为什么js要用单线程模式，而不是多线程模式？

> Javascript的单线程，与它的用途有关作为。浏览器脚本语言，Javascript的主要用途是与用户交互，以及操作DOM，这决定了它只能是单线程，否则会带来很复杂的同步问题。

##### 代码的分类

> - 初始化代码
> - 回调代码

##### js引擎执行代码的基本流程

> 先执行初始化代码：包含一些特别的代码，比如设置定时器、绑定事件监听、发送ajax请求
> 后面在某些时刻才会执行回调代码

* js是单线程执行的(回调函数也是在主线程)
* H5提出了实现多线程的方案: Web Workers
* 只能是主线程s更新界面





## 浏览器的时间循环（轮询）模型

### 模型原理图

事件队列：JS引擎遇到一个异步事件后并不会一直等待其返回结果，而是会将这个事件挂起，继续执行执行栈中的其他任务,当一个异步事件返回结果后，js会将这个事件加入与当前执行栈不同的另一个队列

![事件循环模型](https://i.loli.net/2021/08/02/tcNsnQIEdvSiYO9.png)

#### 模型的2个重要组成部分

1. 事件（定时器/DOM事件/Ajax）管理模块
2. 回调队列

### 模型的运转流程

1. 执行初始化代码，将事件回调函数交给对应模块管理
2. 当事件发生时，管理模块会将回调函数及其数据添加到回调队列中
3. 只有当初始化代码执行完后（可能要一定时间），才会遍历去回调队列中的回调函数执行。

### 内存管理机制

![wechatimg104](https://user-gold-cdn.xitu.io/2018/6/13/163f6b03478ae38a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

#### 栈存储

🌟**栈里的代码先行执行**，再从队列中依次读事件，加入栈中执行

栈内存一般储存基础数据类型

```
 Number String Null Undefined Boolean 函数
 (es6新引入了一种数据类型，Symbol)
```

> - 存储基础数据类型
> - 按值访问
> - 存储的值大小固定
> - 由系统自动分配内存空间
> - 空间小，运行效率高
> - 先进后出，后进先出
> - 栈中的DOM，ajax，setTimeout会依次进入到队列中,当栈中代码执行完毕后，再将队列中的事件放到执行栈中依次执行。
> - 微任务和宏任务

#### 堆存储

> - 存储引用数据类型
> - 按引用访问
> - 存储的值大小不定，可动态调整
> - 主要用来存放对象
> - 空间大，但是运行效率相对较低
> - 无序存储，可根据引用直接获取

### 🌰

```js
console.log(1)
let promise = new Promise(function(resolve,reject){
    console.log(3)
    resolve(100)
}).then(function(data){
    console.log(100)
})
setTimeout(function(){
    console.log(4);
})
console.log(2)

```

> 上面这个demo的结果值是 1 3 2 100 4
>
> 🌟setTimeout是宏任务,而Promise.then是微任务 这里的new Promise()是同步的,所以是立即执行的。
>
> 1. new Promise的时候，excutor函数是立即执行的，
> 2. 基于then或者catch存放的是异步的

同步任务 ——> 微任务 ——> 宏任务

#### 宏任务和微任务

> 概念：微任务和宏任务都是属于队列，而不是放在栈中

新的🌰

```js
console.log('1');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('2');
```

> 1 2 promise1 promise2 setTimeout

##### 宏任务

浏览器为了能够使得`JS`内部宏任务与DOM任务能够有序的执行，会在一个task执行结束后，在下一个 task 执行开始前，对页面进行重新渲染 （task->渲染->task->…） 鼠标点击会触发一个事件回调，需要执行一个宏任务，然后解析HTML。

宏任务队列：I/O、定时器、事件绑定、`ajax`

> **setTimeout不一样**，**setTimeout的作用是等待给定的时间后为它的回调产生一个新的宏任务**。
>
> - 打印‘**promise1** , **promise2**’是第一个宏任务里面的事情，而‘**setTimeout**’是**另一个新的独立的**任务里面打印的。

##### 微任务

通常来说就是需要在当前 task 执行结束后立即执行的任务 

> 微任务队列：`Promise.then`/catch、finally、`process.nextTick`



## [H5 Web Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API/Using_web_workers)

### 斐波拉契数列

```js
<input type="text" placeholder="数值" id="number">
<button id="btn">计算</button>

<script type="text/javascript">
var fibonacci = function (n) {
    let n1 = 1; n2 = 1;
    for (let i = 2; i < n; i++) {
        [n1, n2] = [n2, n1 + n2]
    }
    return n2
}

 var input = document.getElementById('number')
 document.getElementById('btn').onclick = function () {
   var number = input.value
   var result = fibonacci(number)
   alert(result)
 }
</script>
```

> 当我运行此行代码,传入计算数值为50左右(有的甚至更低),整个页面就会卡住好久的时间不能操作(计算结束后才会弹窗,但是未弹窗的这段时间用户并不能进行操作),这时候就会发现单线程的弊端了

### Web Workers

> 可以让js在分线程执行

1. 相关API

> - Worker: 构造函数, 加载分线程执行的js文件
> - Worker.prototype.onmessage: 用于接收另一个线程的回调函数
> - Worker.prototype.postMessage: 向另一个线程发送消息

2. 不足

> - worker内代码不能操作DOM(更新UI)
> - 不能跨域加载JS
> - 不是每个浏览器都支持这个新特性
> - 也慢

3. Worker

```
var worker = new Worker('worker.js');
worker.onMessage = function(event){event.data} : 用来接收另一个线程发送过来的数据的回调
worker.postMessage(data1) : 向另一个线程发送数据
```

#### 主线程

1. 创建一个Worker对象
2. 绑定[主线程接收分线程返回的数据]方法
3. 主线程向分线程发送数据,然后等待接受数据
4. 接收到分线程回馈的数据,将数据进行处理(如弹窗)

```js
<body>
<input type="text" placeholder="数值" id="number">
<button id="btn">计算</button>
<script type="text/javascript">
 var input = document.getElementById('number')
 document.getElementById('btn').onclick = function () {
   var number = input.value

   //创建一个Worker对象
   var worker = new Worker('worker.js')
   // 绑定接收消息的监听
   worker.onmessage = function (event) { //此处变成回调代码,会在初始化工作完成后才会进行
     console.log('主线程接收分线程返回的数据: '+event.data)
     alert(event.data)
   }

   // 向分线程发送消息
   worker.postMessage(number)
   console.log('主线程向分线程发送数据: '+number)
 }
 // console.log(this) // window

</script>
</body>
```



#### 分线程

> 将计算放置分线程中

在分线程中输出 this 





#### 原理图

![H5 Web Workers(多线程)](https://i.loli.net/2021/08/02/FLJTG2Wxy1PVKmd.png)









# 深浅拷贝

## 浅拷贝

浅拷贝会创建一个新的对象，这个对象有着原始对象属性值的一份精准拷贝：

1. 如果原始对象属性类型为基本类型，拷贝的就是基本类型的值，因此修改原、新对象的基本类型属性互不影响
2. 如果原始对象属性类型为引用类型，拷贝的就是内存地址（或指向该地址的指针），因此修改原、新对象的引用类型属性会相互影响

```js
let person = {
	name: '李四',
	age: 18,
    other: {
        name: 'hello'
    }
}

function copy(obj){
	let objCopy = {}
	for(let i in obj){
		objCopy[i] = obj[i]
	}
    return objCopy
}

person.name = '张三'
person.other.name = 'ooooooo'
const newObj = copy(person)
console.log('person',person)
console.log('newObj',newObj)
```

![image-20210801215521651](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210801215521651.png)

## 深拷贝

> 原理：完全复制另外一个对象，引用也是自己创建。即完整复制舒服的值（而非引用）。目的在于避免拷贝后数据对原数据产生影响

实现深拷贝的方式

![image-20210801192711925](https://i.loli.net/2021/08/01/1PkX2xq5OZvlfz9.png)

1. `JSON` 方法实现

   ```js
   let person = {
   	name: '张三',
   	age: 14,
       other: {
           name: 'hello'
       }
   }
   
   function copy(obj){
   	let str = JSON.stringify(obj)
   	let newObj = JSON.parse(str)
   	return newObj
   }
   
   const obj1 = copy(person)
   person.other.name = '李四'
   person.name = 'wang'
   console.log('person',person)
   console.log('obj1',obj1)
   ```

2. 手写递归方法：递归方法实现深度克隆原理：遍历对象、数组直到里边都是基本数据类型，然后再去复制，就是深度拷贝

   ```js
   let person = {
   	name: '张三',
   	age: 14,
       other: {
           name: 'hello'
       }
   }
   
   function copy(obj){
   	let newObj = {}
   	for(let i in obj){
   		if(obj[i] instanceof Object){
   			obj[i] = copy(obj[i])
   		}else{
   			newObj[i] = obj[i]
   		}
   	}
   	return newObj
   }
   
   const obj1 = copy(person)
   person.other.name = '李四'
   person.name = 'wang'
   console.log('person',person)
   console.log('obj1',obj1)
   ```

3. 函数库`lodash`：该函数库也有提供 `_.cloneDeep`用来做深拷贝。

   ```js
   var _ = require('lodash');
   var obj1 = {    
       a: 1, 
       b: { 
           f: { 
               g: 1 
           } 
       },    
       c: [1, 2, 3]
   };
   var obj2 = _.cloneDeep(obj1);
   console.log(obj1.b.f === obj2.b.f);     // false
   ```



# 防抖节流

限制函数的执行次数

## 防抖

> 对于==高频触发==的函数，我们并不想频发触发事件，比如说搜索框实时发请求，onmousemove, resize, onscroll等等，这个时候就需要对函数增加防抖功能了

通过 `setTimeout` 的方式，在一定的时间间隔内，将多次触发变成一次触发（最后一次操作）

```js
<body>
	<input type="text">
	<script>
		let ipt = document.querySelector("input");

		ipt.oninput = debounce(function(){
            console.log(this.value)
        },500)

        function debounce(fn,delay){
            let t = null;
            return function(){
                if(t !== null){
                    clearTimeout(t);
                }
                t = setTimeout(() => {
                    fn.call(this)
                },delay)
            }
		}
	</script>
</body>
```

## 节流

> 在某个规定的时间内，节流函数至少执行一次。（控制执行次数）

```js
<style>
	body{
		height: 2000px
	}
</style>


<script>
	let flag = true
	window.onscroll = throttle(function(){
         console.log('ooooo');       
    },500)
    
    function throttle(fn,delay){
    	return function(){
    		if(flag){
            setTimeout(() => {
            	fn.call(this)
                 flag = true
            },delay)
           }
           flag = false
    	}
    }
</script>
```





# 浏览器渲染机制

### 浏览器内核模块组成

主线程

> * js引擎模块 : 负责js程序的编译与运行
> * html,css文档解析模块 : 负责页面文本的解析
> * DOM/CSS模块 : 负责dom/css在内存中的相关处理 
> * 布局和渲染模块 : 负责页面的布局和效果的绘制(内存中的对象)

分线程

> * 定时器模块 : 负责定时器的管理
> * DOM事件模块 : 负责事件的管理
> * 网络请求模块 : 负责Ajax请求



## 浏览器组成

浏览器主要由7个部分组成：

- 用户界面（User Interface）：定义了一些常用的浏览器组件，比如地址栏，返回、书签等等
- 数据持久化（Data Persistence）：指浏览器的cookie、local storage等组件
- 浏览器引擎（Browser engine）：平台应用的相关接口，在用户界面和呈现引擎之间传送指令。
- 渲染引擎（Rendering engine）：处理HTML、CSS的解析与渲染
- JavaScript解释器（JavaScript Interpreter）：解析和执行JavaScript代码
- 用户界面后端（UI Backend）：指浏览器的的图形库等
- 网络（Networking）：用于网络调用，比如HTTP请求



## 浏览器内核

> 支撑浏览器运行的最核心的程序

浏览器内核分为两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎

- ==渲染引擎==：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机
- ==JS引擎==：负责解析和执行javascript来实现网页的动态效果 浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核，最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎

常见的浏览器内核：

> - Chrome, Safari : webkit
> - firefox : Gecko
> - IE : Trident
> - 360,搜狗等国内浏览器: Trident + webkit



## 页面加载流程

从浏览器地址中从==输入url地址==到==渲染出一个页面==，会经过以下过程。

- DNS 查询：浏览器输入的url地址经过DNS解析获得对应的`IP`

- TCP 连接：向服务器发起TCP的3次握手

- HTTP 请求即响应：建立链接后，浏览器向该IP地址发送http请求

- 服务器响应：服务器接收到请求，返回一堆 HTML 格式的字符串代码

- 客户端渲染
  > - 浏览器获得html代码，解析成DOM树
  > - 获取 CSS 并构建CSSOM
  > - 将DOM与 CSSOM 结合，创建渲染树
  > - 根据渲染树来布局，以计算每个节点的几何信息
  > - 将各个节点绘制到屏幕上

需要明白，这五个步骤并不一定一次性顺序完成。如果 DOM 或 CSSOM 被修改，以上过程需要重复执行，这样才能计算出哪些像素需要在屏幕上进行重新渲染。实际页面中，CSS 与 JavaScript 往往会多次修改 DOM 和 CSSOM。



## 浏览器渲染机制

> 主要是客户端渲染

![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/b943ce50-aee3-11eb-bf5b-0ff6e87e9df2.png)

### 解析HTML成DOM树

这个解析过程大概可以分为几个步骤：

![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/18329dc0-af10-11eb-bf5b-0ff6e87e9df2.png)

- 第一步：浏览器从磁盘或网络读取HTML的==原始字节==，也就是传输的0和1这样的字节数据，并根据文件的指定编码（例如 UTF-8）将它们==转换成字符串==。
- 第二步：将==字符串转换成Token==,例如：“”、“”等。Token中会标识出当前Token是“开始标签”或是“结束标签”亦或是“文本”等信息
- 第三步：在每个Token被生成后，会立刻消耗这个Token创建出节点对象，因此在构建DOM的过程中，不是等待所有的Token都生成后才去构建DOM,而是==一边生成Token一边消耗来生成节点对象==。

> 注意：带有结束标签标识的Token不会创建节点对象

- 第四步：通过“开始标签”与“结束标签”来识别并关联节点之间的关系。当所有Token都生成并消耗完毕后，我们就==得到了一颗完整的DOM树==。

但是现在有一个疑问，节点之间的关联关系是如何维护的呢？ 上面我们提到Token会标识是“开始标签”还是“结束标签”，以下图为例：“Hello”Token位于“title”开始标签与“title”结束标签之间，表明“Hello”Token是“title”Token的子节点。同理“title”Token是“head”Token的子节点。

![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/509917c0-af10-11eb-bf5b-0ff6e87e9df2.png)



### 构建CSSOM

解析css构建CSSOM 的过程和构建DOM的过程非常的相似。当浏览器接收到一段CSS，浏览器首先要做的是==识别出Token，然后构建节点并生成CSSOM==

![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/797154a0-af10-11eb-bf5b-0ff6e87e9df2.png)

节点中样式可以通过继承得到，也可以自己设置，因此在构建的过程中浏览器得递归 CSSOM 树，然后确定具体的元素到底是什么样式。为了CSSOM的完整性，也只有等构建完毕才能进入到下一个阶段，哪怕DOM已经构建完，它也得等CSSOM，然后才能进入下一个阶段。

> CSS匹配HTML元素是一个相当复杂和有性能问题的事情。所以，DOM树要小，CSS尽量用id和class，千万不要过渡层叠下去 所以，CSS的加载速度与构建CSSOM的速度将直接影响首屏渲染速度，因此在默认情况下CSS被视为阻塞渲染的资源

### 构建渲染树

当我们生成DOM树和CSSOM树后，我们需要将这两颗树合并成渲染树，在构建渲染树的过程中浏览器需要做如下工作：

- 从 DOM 树的根节点开始遍历每个可见节点。
- 有些节点不可见（例如脚本Token、元Token等），因为它们不会体现在渲染输出中，所以会被忽略。
- 某些节点被CSS隐藏，因此在渲染树中也会被忽略。例如某些节点设置了display: none属性。
- 对于每个可见节点，为其找到适配的 CSSOM 规则并应用它们 ![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/3e1e73a0-af11-11eb-bf5b-0ff6e87e9df2.png)

### 渲染阻塞

在渲染的过程中，遇到一个script标记时，就会停止渲染，去请求脚本文件并执行脚本文件，因为浏览器渲染和 JS 执行共用一个线程，而且这里必须是单线程操作，==多线程会产生渲染 DOM 冲突==。JavaScript的加载、解析与执行会严重阻塞DOM的构建。只有等到脚本文件执行完毕，才会去继续构建DOM。

js不单会阻塞DOM构建，还会导致CSSOM也阻塞DOM的构建，如果JavaScript脚本还操作了CSSOM，而正好这个CSSOM还没有下载和构建，浏览器甚至会延迟脚本执行和构建DOM，直至完成其CSSOM的下载和构建，然后再执行JavaScript，最后在继续构建DOM

因此script的位置很重要，在实际使用过程中遵循以下两个原则：

- CSS 优先：引入顺序上，CSS 资源先于 JavaScript 资源。
- JS置后：我们通常把JS代码放到页面底部，且JavaScript 应尽量少影响 DOM 的构建

### 布局与绘制

浏览器拿到渲染树后，就会从渲染树的根节点开始遍历，然后确定每个节点对象在页面上的确切大小与位置，通常这一行为也被称为“自动重排”。布局阶段的输出是一个盒子模型，它会精确地捕获每个元素在屏幕内的确切位置与大小，所有相对测量值都将转换为屏幕上的绝对像素。这一过程也可称为回流

布局完成后，浏览器会立即发出“Paint Setup”和“Paint”事件，将渲染树转换成屏幕上的像素。

## 性能优化策略

在我们了解浏览器的渲染机制后，DOM 和 CSSOM 结构构建顺序，我们可以针对性能优化问题给出一些方案，提升页面性能。

### 回流(reflow)与重绘(repaint)

当元素的样式发生变化时，浏览器需要触发更新，重新绘制元素。这个过程中，有两种类型的操作，即重绘与回流。

- 重绘(repaint): 当元素样式的改变不影响布局时，浏览器将使用重绘对元素进行更新，此时由于只需要UI层面的重新像素绘制，因此损耗较少
- 回流(reflow): 当元素的尺寸、结构或触发某些属性时，浏览器会重新渲染页面，称为回流。此时，浏览器需要重新经过计算，计算后还需要重新页面布局，因此是较重的操作。会触发回流的操作:
- 添加或删除可见的DOM元素
- 元素的位置发生变化
- 元素的尺寸发生变化（包括外边距、内边框、边框大小、高度和宽度等）
- 内容发生变化，比如文本变化或图片被另一个不同尺寸的图片所替代。
- 页面一开始渲染的时候（这肯定避免不了）
- 浏览器的窗口尺寸变化（因为回流是根据视口的大小来计算元素的位置和大小的

> 注意：回流一定会触发重绘，而重绘不一定会回流,重绘的开销较小，回流的代价较高

因此为了减少性能优化，我们可以尽量避免回流或者重绘操作 css

- 避免使用table布局
- 将动画效果应用到position属性为absolute或fixed的元素上

javascript

- 避免频繁操作样式，可汇总后统一 一次修改
- 尽量使用class进行样式修改
- 减少dom的增删次数，可使用 字符串 或者 documentFragment 一次性插入
- 极限优化时，修改样式可将其display: none后修改
- 避免多次触发上面提到的那些会触发回流的方法，可以的话尽量用 变量存住

### async和defer的作用是什么？有什么区别?

defer 和 async 属性的区别： ![xxx.png](https://qiniu.youxiubiji.com/youxiubiji/20210507/c528c3a0-af11-11eb-bf5b-0ff6e87e9df2.png)

其中蓝色线代表JavaScript加载；红色线代表JavaScript执行；绿色线代表 HTML 解析

1）情况1 <scriptsrc="script.js"> 没有 defer 或 async，浏览器会立即加载并执行指定的脚本，也就是说不等待后续载入的文档元素，读到就加载并执行。

2）情况2 (异步下载) async 属性表示异步执行引入的 JavaScript，与 defer 的区别在于，如果已经加载好，就会开始执行——无论此刻是 HTML 解析阶段还是 DOMContentLoaded 触发之后。需要注意的是，这种方式加载的 JavaScript 依然会阻塞 load 事件。换句话说，async-script 可能在 DOMContentLoaded 触发之前或之后执行，但一定在 load 触发之前执行。

3）情况3 <scriptdefersrc="script.js">(延迟执行) defer 属性表示延迟执行引入的 JavaScript，即这段 JavaScript 加载时 HTML 并未停止解析，这两个过程是并行的。整个 document 解析完毕且 defer-script 也加载完成之后（这两件事情的顺序无关），会执行所有由 defer-script 加载的 JavaScript 代码，然后触发 DOMContentLoaded 事件。

defer 与相比普通 script，有两点区别：

- 载入 JavaScript 文件时不阻塞 HTML 的解析，执行阶段被放到 HTML 标签解析完成之后；
- 在加载多个JS脚本的时候，async是无顺序的加载，而defer是有顺序的加载

js优化可以在script标签加上 defer属性 和 async属性用于在不阻塞页面文档解析的前提下，控制脚本的下载和执行

> 其他: CSS 标签的 rel属性 中的属性值设置为 preload 能够让你在你的HTML页面中可以指明哪些资源是在页面加载完成后即刻需要的,最优的配置加载顺序，提高渲染性能

### 首屏优化加载

- 减少首屏 CGI 的计算量：比如在微信8.8无现金日H5开发中，前端希望拿到用户的个人信息、消费记录、排名三类数据，如果只通过一个CGI来处理，那么后台响应时间肯定会变长；由于在H5的首屏中，只包含了用户信息，消费记录、排名都在第2屏和第3屏，此时其实可以==利用异步的方式==来拿消费记录、排名的数据。
- 页面瘦身：压缩HTML、CSS、JavaScript。
- 减少请求：CSS、JavaScript文件数尽量少，甚至当CSS、JS的代码不多时，可以考虑直接将代码内嵌到页面中。
- 多用缓存：缓存能大幅度降低页面非首次加载的时间。
- 少用table布局，浏览器在渲染table时会消耗较多资源，而且只有table里有一点变化，整个table都会重新渲染。
- 做预加载：部分H5页面首屏可能要下载较多的静态资源，比如图片，这时为了避免加载时出现“难看”的页面，用预加载（loading的方式）做一个过渡

### 总结

得出结论： 浏览器渲染的关键路径共分五个步骤：

> 构建 DOM -> 构建 CSSOM -> 构建渲染树 -> 布局 -> 绘制





# 本地存储

1. 数据存储在用户浏览器中
2. 设置、读取方便、甚至页面刷新不丢失数据
3. 容量较大，sessionStorage约5M、localStorage约20M
4. 只能存储字符串，可以将对象JSON.stringify()编程后存储

## window.sessionStorage

1. 生命周期为关闭浏览器窗口
2. 在同一个窗口下数据可以共享
3. 以键值对的形式存储使用

```js
//存储数据：
sessionStorage.setItem(key,value)
//获取数据：
sessionStorage.getItem(key)
//删除数据：
sessionStorage.removeItem(key)
//删除所有数据：
sessionStorage.clear()
```

## window.localStorage

1. 生命周期永久生效，除非手动删除否则关闭页面也会存在。
2. 可以多窗口/页面共享（同一浏览器可以共享）
3. 以键值对的形式存储使用

```js
//存储数据
localStorage.setItem(key,value)
//获取数据
localStorage.getItem(key)
//删除数据
localStorage.removeItem(key)
//删除所有数据
localStorage.clear()
```



