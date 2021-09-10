# 变量

### 关键字：let

1. 不存在重复声明

   ```js
   let star='张三';
   let star='李四'  //error
   ```

2. 块级作用域（在代码块有效），有各自单独的作用域，外层代码块**不受内层代码块的影响**。

   ```js
   {
       let girl='王五'
   }
   console.log(girl) //error
   ```

   > 不仅仅针对花括号，例如if（）里面

3. **不**存在**变量提升**：减少运行时错误

   ```js
   console.log(song)   //error
   let song='恋爱达人'
   ```

4. 在全局作用域的var下，不影响作用域：只要块级作用域内存在 let 命令，它所声明的变量就“绑定”（binding）这个区域（暂时性死区）

   ```js
   let school='abc'
   function fn(){
       console.log(school) //abc
   }
   ```

##### 暂时性死区

> （ temporal dead zone ， `TDZ` ）

1. 在代码块内，使用 let 命令声明变量之前，该变量都是**不可用**的
2. “暂时性死区”也意味着 `typeof` 不再是一个百分之百安全的操作。

有些“死区”比较隐蔽，不太容易发现。 

```js
function bar(x = y, y = 2) { 		//此时 y 还没有声明,属于”死区“
	return [x, y]; 					
} 
bar(); // 报错 
```

如果 y 的默 认值是 x ，就不会报错，因为此时 **x 已经声明**了。 

```js
function bar(x = 2, y = x) { 
	return [x, y]; 
} 
bar(); // [2, 2]
```



##### do 表达式

块级作用域可以使用 do 变为表达式，也就是说可以返回值

```js
let x = do { 
	let t = f(); 
	t * t + 1; 
}; 
//变量 x 会得到整个块级作用域的返回值（ t * t + 1 ）
```



### 关键字：war

1. 可以重复声明

2. 声明全局作用域

3. 允许变量提升：即变量可以在声明之前使用，值为 undefined

   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>点击切换颜色</title>
       <link rel="stylesheet" href="index.css">
   </head>
   <body>
       <div class="conrainer">
           <h2 class="page-header">点击切换颜色</h2>
           <div class="item"></div>
           <div class="item"></div>
           <div class="item"></div>
       </div>
       <script>
           let items = document.getElementsByClassName('item');
           for (var i = 0;i<items.length;i++){
               items[i].onclick = function() {
                   this.style.background = 'pink';
               }
           }
       </script>
   </body>
   </html>

![image-20210418103058820](https://i.loli.net/2021/08/12/eI5LPjRJ26o7dYh.png)PS：

将 `this.style.background = 'pink';` 改为 `items[i].style.background = 'pink';` 会报错

原因：因为在全局作用域 var 下，最后 i 将执行到 3 。

解决方案：var 改为 let 



#### 循环函数

```js
var funcs = [],
object = {
    a: true,
    b: true,
    c: true
};
for (let key in object) {
    funcs.push(function() {
    	console.log(key);
	});
}
funcs.forEach(function(func) {
	func(); // 依次输出 "a"、 "b"、 "c"
});
```

let 使每个函数都能够拥有它自身的 key 变量副本，结果**每个函数都输出了一个 不同的值**。而如果使用 var 来声明 key ，则所有函数都只会输出 "c"



# 常量

### 关键字：`const`

1. 一定要初始化-“赋值”

2. 一般常量使用大写(潜规则)

3. 常量的值不能修改，禁止重复声明已有变量（无论是 var 声明，还是 let 声明）

4. 块级作用域

5. 常量声明不提升：存在**暂时性死区**

6. 对于数组和对象的元素修改，不算是对常量的修改，不会报错

   ```js
   eg1：
   //不会报错
   const TEAN = ['UZI','MXLG','Ming'];
   TEAM.push('Meiko');
   
   eg2：
   if (condition) {
   	const maxItems = 5;
   	// 其他代码
   }
   // maxItems 在代码块外部无法被访问
   ```


> 对象冻结，应该使用 `Object.freeze` 方法。
>
> ```js
> const foo = Object.freeze({});
> // 常规模式时，下面一行不起作用； 
> // 严格模式时，该行会报错 
> foo.prop = 123;
> 
> //常量 foo 指向一个冻结的对象，所以添加新属性不起作用
> ```



# 对象

### 顶层对象

1. 浏览器：windows
2. `Node`：global
3. 顶层对象的属性与全局变量是等价的。

### global对象

同一段代码为了能够在各种环境，都能取到顶层对象，现在一般是使用 this 变量，但是有局限性。

- 全局环境中， this 会返回顶层对象。Node 模块和 `ES6` 模块中， this 返回的是当前模块。
-  函数里面的 this ，如果函数不是作为对象的方法运行，而是单纯作为函数运行， this 会指向顶层对象。

### 简化对象

 ES6允许在对象的大括号内直接写入变量和函数作为对象的属性和方法 

```js
let name = '张三';
let change = function(){
	console.log('我们可以改变世界');
}
const school = {
	name,
	change,
	//这是一个函数
	impove(){
		console.log("我们不在犯罪");
	}
}
console.log(school);
//可以输出 name，change……
```



# 数组

`Array.from()`

1. 将类数组对象转换为真正数组

   具备的条件：

   1. **该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。**
   2. **该类数组对象的属性名必须为数值型或字符串型的数字**

   ```js 
   let arrayLike = {
       0: 'tom', 
       1: '65',
       2: '男',
       3: ['jane','john','Mary'],
       'length': 4
   }
   let arr = Array.from(arrayLike)
   console.log(arr) // ['tom','65','男',['jane','john','Mary']]
   ```

2. 将Set结构的数据转换为真正的数组

   ```js
   let arr = [12,45,97,9797,564,134,45642]
   let set = new Set(arr)
   console.log(Array.from(set, item => item + 1)) // [ 13, 46, 98, 9798, 565, 135, 45643 ]
   ```

   

3. 将字符串转换为数组

   ```js
   let  str = 'hello world!';
   console.log(Array.from(str)) 
   // ["h", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d", "!"]
   ```

   

4. Array.from参数是一个真正的数组

   ```js
   console.log(Array.from([12,45,47,56,213,4654,154]))
   ```

   



# 解构赋值

PS：允许按照一定模式从数组和对象中提取值，对变量进行赋值

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。

#### 基础用法

- 模式匹配：只要等号两边的模式相同，左边的变量就会被赋予对应的值

  ```js
  let [x, y, ...z] = ['a']; 
  x // "a" 
  y // undefined 
  z // []
  ```

  > 如果解构不成功，变量的值就等于 undefined 。

- 不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组

  ```js
  let [x, y] = [1, 2, 3];
  x // 1
  y // 2
  ```


#### 数组的解构

```js
let colors = [ "red" ];

let [ firstColor, secondColor = "green" ] = colors;
//允许在数组任意位置指定默认值
console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

> 不要遗忘初始化器器（即等号 右边的值）



#### 对象的解构

PS：对象的属性没有次序，变量必须与属性**同名**

```js
let node = {
	type: "Identifier",
	name: "foo",
	loc: {
		start: {
			line: 1,
			column: 1
		},
		end: {
			line: 1,
			column: 4
		}
	}
};
let { loc: { start: { line } }} = node; //属性名表达式
// 提取 node.loc.start(变量名与属性名不一致):let { loc: { start: localStart}} = node;
//可以赋值给不同的本地变量名以及添加默认值
//花括号内的右侧， loc 被作为需检查的位置来使用，而不会创建变量绑定。

console.log(start.line); // 1
console.log(start.column); // 1
console.log(value); // undefined
//如果所指定的本地变量在对象中没有找到同名属性，那么该变量会被赋值为 undefined
```



如果变量名与属性名不一致，必须写成下面这样。

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```



对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"
foo // error: foo is not defined
```

> 上面代码中，`foo`是匹配的模式，`baz`才是变量。真正被赋值的是变量`baz`，而不是模式`foo`。

注意点：

1. JavaScript 引擎会将`{x}`理解成一个代码块，从而发生语法错误。

   ```js
   // 正确的写法
   let x;
   ({x} = {x: 1});
   ```

2. 由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

   ```javascript
   let arr = [1, 2, 3];
   let {0 : first, [arr.length - 1] : last} = arr;
   first // 1
   last // 3
   ```



#### 字符串的解构赋值

```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```



#### 数值/布尔值解构

解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

```javascript
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```

上面代码中，数值和布尔值的包装对象都有`toString`属性，因此变量`s`都能取到值。



#### 函数参数的解构赋值

```javascript
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

上面代码中，函数`add`的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量`x`和`y`。对于函数内部的代码来说，它们能感受到的参数就是`x`和`y`。



#### 其他

- 剩余项：使用 `...` 语法来将剩余的项目赋值给一个指定的变量

- 嵌套的解构

- 混合解构：对象和数组解构一起用

- 参数解构

- 可以使用圆括号的情况

- ```
  //都是赋值语句，而不是声明语句
  [(b)] = [3]; // 正确
  ({ p: (d) } = {}); // 正确 —— 模式是取数组的第一个成员，模式是 p ，而不是 d
  [(parseInt.prop)] = [3]; // 正确
  ```



#### 用途

1. 交换变量的值

2. 从函数返回多个值

3. 函数参数的定义

   > 解构赋值可以方便地将一组参数与变量名对应起来。

   ```javascript
   // 参数是一组有次序的值
   function f([x, y, z]) { ... }
   f([1, 2, 3]);
   
   // 参数是一组无次序的值
   function f({x, y, z}) { ... }
   f({z: 3, y: 2, x: 1});
   ```

4. 提取 `JSON` 数据

   ```js
   let jsonData = {
     id: 42,
     status: "OK",
     data: [867, 5309]
   };
   
   let { id, status, data: number } = jsonData;
   
   console.log(id, status, number);
   // 42, "OK", [867, 5309]
   ```

5. 函数参数的默认

   ```javascript
   jQuery.ajax = function (url, {
     async = true,
     beforeSend = function () {},
     cache = true,
     complete = function () {},
     crossDomain = false,
     global = true,
     // ... more config
   } = {}) {
     // ... do stuff
   };
   ```

   > 指定参数的默认值，就避免了在函数体内部再写`var foo = config.foo || 'default foo';`这样的语句。

6. 遍历 Map 结构

   > 如果只想获取键名，或者只想获取键值，可以写成下面这样。

   ```js
   // 获取键名
   for (let [key] of map) {
    // ...
   }
   // 获取键值
   for (let [,value] of map) {
    // ...
   }
   ```

7. 输入模块的指定方法：加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。

   ```js
   const { SourceMapConsumer, SourceNode } = require("source-map");
   ```





# 模板字符串

模板字符串（template string）是增强版的字符串，用反引号（`）标识，特点：

> - 字符串中可以出现换行符；
> - 可以使用 ${xxx} 形式引用变量；

1. 声明

   ```js
   let str = `我也是一个字符串`
   console.log(str,typeof str);
   ```

2. 内容中可以直接出现换行符（所有模板字符串的空格和换行，都是被保留的 ）

   > 标签前面会有一个换行。如果你不想要这个换行，可以使用 trim 方法消除它。

   ```js
   let str = `<ul>
   			<li>冉海锋</li>
   			<li>冉海锋</li>
   		   </ul>`；
   ```

3. 变量拼接

   ```js
   let lovest = '张三';
   let out = `${lovest}是法外狂徒`;		//模板字符串中嵌入变量，需要将变量名写在 ${} 之中。
   console.log(out)  //张三是法外狂徒
   ```

4. 大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性。

   ```javascript
   let x = 1;
   let y = 2;
   
   `${x} + ${y} = ${x + y}`
   // "1 + 2 = 3"
   
   `${x} + ${y * 2} = ${x + y * 2}`
   // "1 + 4 = 5"
   
   let obj = {x: 1, y: 2};
   `${obj.x + obj.y}`
   // "3"
   ```

5. 调用函数。

   ```javascript
   function fn() {
     return "Hello World";
   }
   
   `foo ${fn()} bar`
   // foo Hello World bar
   ```

#### 标签模板

> 函数调用的一种特殊形式。“标签”指的就是函数，紧跟在后面的模板字符串就是它的参数。

```javascript
let a = 5;
let b = 10;

tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```

PS：处理模板字符串





# 箭头函数

> 允许使用箭头（=>）定义函数

1. 声明函数

```js
// a ，b 是形参
let fn = (a,b) =>{
	return a + b;
}
```

2. this 是静态的，this 始终指向函数**声明时**所在作用域下的this的值。

   > PS：`call`方法：可以改变函数内部的值

   ```js
   function A(){
       console.log(this.name)
   }
   
   let B = () => {
       console.log(this.name);
   }
   
   window.name = '尚硅谷';
   const school = {
       name: 'ATGUIGU'
   }
   
   //直接调用
   A()   //尚硅谷
   B()  //尚硅谷
   
   //call
   A.call(school); //ATGUIGU
   B.cal(school);  //尚硅谷
   ```

3. 不能作为构造实例化对象

   ```js
   let A(name,age) => {
       this.name=name;
       this.age=age;
   }
   let me = new A('xiao',123);
   console.me //error
   ```

4. 不能使用 arguments 变量

   ```js
   let fn = () => {
       console.log(arguments)；
   }
   fn(1,2,3)  //error
   ```

5. 简写
   1. 省略小括号：当形参有且只有一个的时候

      ```js
      let add = n => {
          return n + 1;
      }
      ```

   2. 省略花括号：当代码只有一条语句的时候，此时 return 必须省略，而且语句的执行结果就是函数的返回值

      ```js
      let add = n => n+1;
      ```

6. > 箭头函数适合与 this 无关的回调——定时器、数组的方法回调
   >
   > 不适合与 this 有关的回调：事件回调、对象的方法

PS：

fitter()方法

```js
<script>
var ages = [32, 33, 12, 40];
function checkAdult(age) {
    return age >= document.getElementById("ageToCheck").value;
}
function myFunction() {
    document.getElementById("demo").innerHTML = ages.filter(checkAdult);
}
</script>
```

![image-20210418175508790](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210418175508790.png)



# 形参——实参

1. 函数参数的默认值设置（可初始化）

   - 可以给形参赋初始值，一般位置要靠后（潜规则）

     ```js
     function add(a,b,c=12){
         return a+b+c; 
     }
     let result = add (1,2);
     console.log(result) // 15
     ```

   - 与解构赋值结合

     ```js
     function A({host='127.0.0.1',username,password,port}){
         console.log(host+username+password+port)
     }
     A({
         username:'ran',
         password:'123456',
         port:3306
     })
     ```

2. 引入 rest 参数，用于获取函数的实参，用来代替 argument

```js
// ...args = rest 参数
function date(...args){
	console.log(args);		//filter, some, every, map
}
date('112','231','321');
//rest 参数必须放到参数最后
```



# 扩展运算符

> PS：能够将【数组】转换为逗号分隔的【参数序列】
>

```js
const TEAN = ['UZI','MXLG','Ming'];
function active(){
	console.log(arguemnt);
}
active(...TEAN);	//等同active(''UZI','MXLG','Ming'')
```

#### 应用

1. 数组的合并

```js
const kuaizi = ['王太利','肖扬'];
const f4 = ['UZI','MXLG','Ming'];
const together = [...kuazi,...f4];
console.log(together);
```

2. 数组的克隆

```js
const f4 = ['UZI','MXLG','Ming'];
const other = [...f4];
```

3. 将伪数组转为真正的数组

```js
const divs = document.querySelectorAll('div');
const divArr = [...divs];
```



# symbol

> PS：表示独一无二的值。它是 JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。

#### symbol 的特点

- Symbol的值是唯一的，用来解决命名冲突的问题
- Symbol值不能与其他数据进行运算
- Symbol定义的对象属性不能使用for…in循环遍历，但是可以使用`Reflect.ownKeys`来获取对象的所有键名

#### Symbol的使用

1. 创建Symbol

```js
let s = Symbol();
```

2. `Symbol.for` 创建

```js
let s = Symbol.for('');
```

Symbol的值==是唯一的==：

```js
let s = Symbol('aa');
let s2= Symbol('aa');
console.log(s===s2)   //false

let s3 = Symbol.for('bb');
let s4 = Symbol.for('bb');
comsole.log(s3===s4) ///true
```

3. 不能与其他数据进行运算

> 数据类型：`USONB`（you are so NB）
>
> 1. u—undefined
> 2. s—string   symbol
> 3. o—object
> 4. n—null    number
> 5. b—boolean

```js
let result = s + 100  //error
let result = s > 100  //error
let result = s + s  //error
```

5. Symbol内置值

   ```js
   class Person {
       static [Symbol.hasInstance](param){
           console.log(param);
           console.log("我被用来检测了")；
           return false;
       }
   }
   let o = {};
   console.log(o instanceof Person); //我被用来检测了，false
   ```

|      内置Symbol的值       | 调用时机                                                     |
| :-----------------------: | :----------------------------------------------------------- |
|    Symbol.hasInstance     | 当其他对象使用 instanceof 运算符，判断是否为该对象的实例时，会调用这个方法 |
| Symbol.isConcatSpreadable | 对象的 Symbol.isConcatSpreadable 属性等于的是一个布尔值，表示该对象用于 Array.prototype.concat()时，是否可以展开。 |
|      Symbol.species       | 创建衍生对象时，会使用该属性                                 |
|       Symbol.match        | 当执行 str.match(myObject) 时，如果该属性存在，会调用它，返回该方法的返回值。 |
|      Symbol.replace       | 当该对象被 str.replace(myObject)方法调用时，会返回该方法的返回值 |
|       Symbol.search       | 当该对象被 str. search (myObject)方法调用时，会返回该方法的返回值。 |
|       Symbol.split        | 当该对象被 str. split (myObject)方法调用时，会返回该方法的返回值。 |
|      Symbol.iterator      | 对象进行 for…of 循环时，会调用 Symbol.iterator 方法，返回该对象的默认遍历器 |
|    Symbol.toPrimitive     | 该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。 |
|    Symbol. toStringTag    | 在该对象上面调用 toString 方法时，返回该方法的返回值         |
|    Symbol. unscopables    | 该对象指定了使用 with 关键字时，哪些属性会被 with环境排除。  |



#### symbol的应用

> 给对象添加方法

方式一：

```js
// 向对象中添加方法 up down 
let game = {
    name : 'ran',
    up: function(){}, 
    down: function(){} 
}
// 我们要往game对象里面添加方法，但是怕game对象已经存在 
// 同名方法，所以我们这时使用到了Symbol
// 声明一个对象 
let methods = {
    up:Symbol()
    down:Symbol()
}
game[methods.up]=function(){
    console.log('aaa');
}
game[methods.down]=function(){
    console.log('bbb');
}
console.log(game)    // name: 'ran',Symbol(),Symbol()
```

方式二：

```js
let youxi = {
    name: '狼人杀'，
    [Symbol('say')]:function(){
        console.log('阿萨德')
    }
}
console.log(youxi)    // name:'狼人杀',Symbol(say)

// 调用方法
let say = Symbol('say'); 
let youxi1 = { 
    name:"狼人杀",
    [say]: function(){ 
        console.log("我可以发言") 
    },
    [Symbol('zibao')]: function(){ 
        console.log('我可以自爆'); 
    } 
}
youxi1[say](); 
```



# 迭代器

> 迭代器(lterator)是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署lterator接口，就可以完成遍历操作。

#### 迭代器的特性

ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费；

原生具备 iterator 接口的数据(可用 for of 遍历)：

- Array；
- Arguments；
- Set；
- Map；
- String；
- TypedArray；
- NodeList；

> 工作原理：
>
> 1. 创建一个指针对象，指向数据结构的起始位置，
> 2. 第一次调用==next()==方法，指针自动指向数据结构第一个成员，
> 3. 接下来不断调用==next()==，指针一直往后移动，直到指向最后一个成员，
> 4. 每调用 next() 返回一个包含value和done属性的对象
>
> **注：需要自定义遍历数据的时候，要想到迭代器；**

```js
// 声明一个数组 
const xiyou = ['唐僧', '孙悟空', '猪八戒', '沙僧']; 

// 使用 for...of 遍历数组 ,v 代表键值
// for in保存的是键名，for of保存的是键值
for(let v of xiyou){ 
	console.log(v); 	// 唐僧,孙悟空,猪八戒,沙僧  
}

let iterator = xiyou[Symbol.iterator](); 

// 调用对象的next方法 
console.log(iterator.next()); 	// {{value:'唐僧'，done:false}}
console.log(iterator.next()); 
console.log(iterator.next()); 
console.log(iterator.next()); 
console.log(iterator.next()); 

// 重新初始化对象，指针也会重新回到最前面 
let iterator1 = xiyou[Symbol.iterator](); 
console.log(iterator1.next()); 	// {{value:'唐僧'，done:false}}
```

执行结果：

**//  使用 for...of 遍历数组** 

![image-20210812165809914](https://i.loli.net/2021/08/12/8ofDCeL3WBpJmOE.png)

**//  调用对象的next方法** 

![image-20210812165855799](https://i.loli.net/2021/08/12/aHEduyMkTpoQqNY.png)



#### 迭代器的应用

**迭代器自定义遍历对象**——对对象的遍历

```js
const banji = {
    name : "终极一班",
    stus: [
        'aa',
        'bb',
        'cc',
        'dd'
    ],
    [Symbol.iterator](){
        let index = 0;
        let _this = this;
        return {
            next: () => {
                if(index < this.stus.length){
                    const result = {value: _this.stus[index],done: false};
                    //下标自增
                    index++;
                    //返回结果
                    return result;
                }else {
                    return {value: underfined,done:true};
                }
            }
        }
    }
}

for(let v of banji){
    console.log(v);  // aa bb cc dd
}
```



# 生成器

> 生成器函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同

1. 特殊的函数：异步编程、纯回调函数

```js
//声明
function * gen(arg){
	// yield 函数代码的分隔符,调用四次
	consol.log(arg)
	yield '一只没有耳朵';
	yield '一只没有尾巴';
	yield '奇怪';	
}
let chang = gen();
//调用
// next()可以传入实参
chang.next();
```

> **异步编程**：文件操作、网络操作（`ajax`、request）、数据库操作

2. 生成器函数的参数传递

   ```js
   function * gen(args){
       console.log(args);
       let one = yield 111;
       console.log(one);
       let two = yield 222;
       console.log(two);
       let three = yield 333;
       console.log(three);
   }
   
   let iterator = gen('AAA');
   console.log(iterator.next());
   console.log(iterator.next('BBB'));  //next中传入的BBB将作为yield 111的返回结果
   console.log(iterator.next('CCC'));  //next中传入的CCC将作为yield 222的返回结果
   console.log(iterator.next('DDD'));  //next中传入的DDD将作为yield 333的返回结果
   ```

   

   实例1：用生成器函数的方式解决==回调地狱==问题

   ```js
   function one(){
       setTimeout(()=>{
           console.log('111')
           iterator.next()
       },1000)
   }
   function two(){
       setTimeout(()=>{
           console.log('222')
           iterator.next();
       },2000)
   }
   function three(){
       setTimeout(()=>{
           console.log('333')
           iterator.next();
       },3000)
   }
   
   function * gen(){
       yield one();
       yield two();
       yield three();
   }
   
   let iterator = gen();
   iterator.next();
   ```

   实例2：模拟异步获取数据

   ```js
   function one(){
       setTimeout(()=>{
           let data='用户数据';
           // 调用 next 方法，并且将数据传入
           iterator.next(data)
       },1000)
   }
   function two(){
       setTimeout(()=>{
           let data='订单数据';
           iterator.next(data)
       },2000)
   }
   function three(){
       setTimeout(()=>{
           let data='商品数据';
           iterator.next(data)
       },3000)
   }
   
   function * gen(){
       let users=yield one();
       console.log(users)
       let orders=yield two();
       console.log(orders)
       let goods=yield three();
       console.log(goods)
   }
   
   let iterator = gen();
   iterator.next();
   ```

   





# Promise

**异步编程的新解决方案**。

> 语法上 Promise 是一个**构造函数**，用来封装异步操作，并可以获取其成功或失败的结果；

1. 构造函数：Promise (`excutor`){}
2. `promise.prototype.then`
3. `promise.prototype.catch`

#### 基本特性

```js
<script>
    const p =new Promise((resolve, reject)=>{
        setTimeout(()=>{
            let data='数据库数据'
            // resolve(data);
            reject(data);
        })
    })

    p.then(function (value){         //成功则执行第一个回调函数，失败则执行第二个
        console.log(value)
    },function (reason){
        console.error(reason)
    })
</script>
```

#### Promise.then() 方法

> then() 函数返回的实际也是一个Promise对象

1. 当回调后，返回的是非Promise类型的属性时，状态为fulfilled，then() 函数的返回值为对象的成功值，如reutnr 123，返回的Promise对象值为123，如果没有返回值，是undefined
2. 当回调后，返回的是Promise类型的对象时，then() 函数的返回值为这个Promise对象的状态值
3. 当回调后，如果抛出的异常，则then() 函数的返回值状态也是rejected

```js
<script>
    const p =new Promise((resolve, reject) =>{
        setTimeout(()=>{
            resolve('用户数据');
        })
    });

    let result = p.then(value => {
        console.log(value)
        // return 123;
        // return new Promise((resolve, reject) => {
        //     resolve('ok')
        // })
        throw 123
    },reason => {
        console.log(reason)
    })
    console.log(result);
</script>
```

#### Promise.catch() 方法

> catch函数只有一个回调函数，意味着如果Promise对象状态为失败就会调用 catch() 方法并且调用回调函数

```js
<script>
    const p = new Promise((resolve, reject) => {
        setTimeout(()=>{
            reject('出错啦')
        },1000)
    })

    p.catch(reason => {
        console.log(reason)
    })
</script>
```



# 集合

### Set

> 新的数据结构 Set（集合）。**它类似于数组，但成员的值都是唯一的**，集合实现了 iterator接口，所以可以使用『扩展运算符』和『for…of…』进行遍历

集合的属性和方法：

- size 返回集合的元素个数；
- add 增加一个新元素，返回当前集合；
- delete 删除元素，返回 boolean 值；
- has 检测集合中是否包含某个元素，返回 boolean 值；
- clear 清空集合，返回 undefined； 

```js
    let s = new Set();
    console.log(s,typeof s);  // object

    let s2 = new Set(['A','B','C','D'])
    

    //元素个数
    console.log(s2.size);

    //添加新的元素
    s2.add('E');

    //删除元素
    s2.delete('A')

    //检测
    console.log(s2.has('C'));

    //清空
    s2.clear()

    console.log(s2);
```

#### set应用

```js
    let arr = [1,2,3,4,5,4,3,2,1]

    //1.数组去重
    let result = [...new Set(arr)]
    console.log(result);
    
    //2.交集
    let arr2=[4,5,6,5,6]
    let result2 = [...new Set(arr)].filter(item => new Set(arr2).has(item))
    console.log(result2);
    
    //3.并集
    let result3=[new Set([...arr,...arr2])]
    console.log(result3);

    //4.差集
    let result4= [...new Set(arr)].filter(item => !(new Set(arr2).has(item)))
    console.log(result4);
```



### Map

> 它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map也实现了iterator接口，所以可以使用『扩展运算符』和「for…of…』进行遍历。

**Map** **的属性和方法：**

- size 返回 Map 的元素个数；
- set 增加一个新元素，返回当前 Map； 
- get 返回键名对象的键值；
- has 检测 Map 中是否包含某个元素，返回 boolean 值；
- clear 清空集合，返回 undefined；

```js
    let m = new Map();
    m.set('name','ran');
    m.set('change',function()=>{
        console.log('改变！')
    })
    let key={
        school:'atguigu'
    }
    m.set(key,['成都','西安']);

    //size
    console.log(m.size);

    //删除
    m.delete('name');

    //获取
    console.log(m.get('change'));

    // //清空
    m.clear()

    //遍历
    for(let v of m){
        console.log(v);
    }
```





# class 

> 引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已；

**知识点：**

1. class 声明类；
2. constructor 定义构造函数初始化；
3. extends 继承父类；
4. super 调用父级构造方法；
5. static 定义静态方法和属性；
6. 父类方法可以重写；

```js
    class shouji {
        constructor(brand,price) {
            this.brand=brand;
            this.price=price
        }

        call(){
            console.log('我可以打电话')
        }
    }

    let A = new shouji('1+',1999);
    console.log(A)
```



### 静态成员

```js
<script>
  class Person{
      static name='手机'
  }
  let nokia = new Person();
  console.log(nokia.name);
</script>
```



### ES5 构造函数方法继承

```js
 function Phone(brand,price){
      this.brand=brand;
      this.price=price;
  }
  Phone.prototype.call=function (){
      console.log("我可以打电话");
  }
  function SmartPhone(brand,price,color,size){
      Phone.call(this,brand,price);
      this.color=color;
      this.size=size;
  }

  //设置子级构造函数原型
  SmartPhone.prototype=new Phone;
  SmartPhone.prototype.constructor=SmartPhone;

  //声明子类方法
  SmartPhone.prototype.photo = function (){
      console.log('我可以玩游戏');
  }
  const chuizi = new SmartPhone('锤子',2499,'黑色','5.5inch')
  console.log(chuizi);
```



### Class的类继承

```js
    class Phone{
        constructor(brand,price) {
            this.brand=brand;
            this.price=price;

        }
        //父类的成员属性
        call(){
            console.log('我可以打电话')
        }
    }
    class SmartPhone extends Phone{
        constructor(brand,price,color,size) {
            super(brand,price);
            this.color=color;
            this.size=size;
        }
        photo(){
            console.log('拍照');
        }

        playGame(){
            console.log('打游戏');
        }
    }
    const xiaomi=new SmartPhone('小米',1999,'黑色','4.7inch')
    xiaomi.call();
    xiaomi.photo();
    xiaomi.playGame();
```



### 子类对父类方法的重写

```
	class Phone{
        constructor(brand,price) {
            this.brand=brand;
            this.price=price;

        }
        //父类的成员属性
        call(){
            console.log('我可以打电话')
        }
    }
    class SmartPhone extends Phone{
        constructor(brand,price,color,size) {
            super(brand,price);
            this.color=color;
            this.size=size;
        }
        photo(){
            console.log('拍照');
        }

        playGame(){
            console.log('打游戏');
        }

        //重写！
        call(){
            console.log('我可以进行视频通话')
        }
    }
    const xiaomi=new SmartPhone('小米',1999,'黑色','4.7inch')
    xiaomi.call();
    xiaomi.photo();
    xiaomi.playGame();
```



### get和set设置

```js
	class Phone{
      get price(){
          console.log("价格被读取了")
          return 'I LOVE YOU'
      }

      set price(value){
          console.log('价格被修改了')
          return value;
      }
  }

    //实例化对象
    let s = new Phone();
    s.price=12  
    // console.log(s.price)   //其实是调用price方法
```



### 数值扩展

1. Number.EPSILON

   - Number.EPSILON 是 JavaScript 表示的最小精度；

   - EPSILON 属性的值接近于 2.2204460492503130808472633361816E-16；

     ```js
        // Number.EPSILON是 JavaScript的最小精度，属性的值接近于 2.22044...E-16
        function equal(a,b){
            if(Math.abs(a-b) < Number.EPSILON){
                return true;
            }else {
                return false;
            }
        }
        console.log(equal(0.1 + 0.2 === 0.3))  //false
        console.log(equal(0.1+0.2,0.3))  //true
     ```

     

2. 二进制和八进制

   > ES6 提供了二进制和八进制数值的新的写法，分别用前缀 0b 和 0o 表示；
   >
   > ```js
   >    //二进制和八进制
   >    let b = 0b1010; //2进制
   >    let o = 0o777;  //8进制
   >    let d = 100;    //10进制
   >    let x = 0xff;   //16进制
   >    console.log(x)   //255
   > ```

3. Number.isFinite() 

   > Number.isFinite() 用来检查一个数值是否为有限的；
   >
   > ```js
   >  //检测一个数是否为有限数
   >    console.log(Number.isFinite(100));  //true
   >    console.log(Number.isFinite(100/0));  //false
   >    console.log(Number.isFinite(Infinity));  //false
   > ```

4. Number.isNaN() 

   > Number.isNaN() 用来检查一个值是否为 NaN；
   >
   > ```js
   >   //检测一个数值是否为NaN
   >    console.log(Number.isNaN(123))  //false
   > ```

5. Number.parseInt() 与 Number.parseFloat()：

   > ES6 将全局方法 parseInt 和 parseFloat，移植到 Number 对象上面，使用不变；
   >
   > ```js
   >   //字符串转整数
   >    console.log(Number.parseInt('5213123love')); //5213123
   >    console.log(Number.parseFloat('5.123123神器')); //5.123123
   > ```

6. Math.trunc

   > 用于去除一个数的小数部分，返回整数部分；
   >
   > ```
   >    //将小数部分抹除
   >    console.log(Math.trunc(3.45345345345)) //3
   > ```
   >
   > 

7. Number.isInteger

   > Number.isInteger() 用来判断一个数值是否为整数；
   >
   > ```js
   >    //判断是否为整数
   >    console.log(Number.isInteger(5));  //true
   >    console.log(Number.isInteger(2.5)); //false
   > ```
   >
   > 

8. Math.sign 

   > 判断一个数到底为正数 负数 还是零 
   >
   > ```js
   >    //检测一个数到底是正数、负数、还是0
   >    console.log(Math.sign(100)) //1
   >    console.log(Math.sign(0))  //0
   >    console.log(Math.sign(-123)) //-1
   > ```



### 对象扩展

ES6 新增了一些 Object 对象的方法：

1. `Object.is` 判断两个值是否严格相等，与『===』行为基本一致（+0 与 NaN）；

   ```js
   	console.log(Object.is(120,120))  //true
   	console.log(Object.is(NaN,NaN))  //true
   ```

2. `Object.assign` 对象的合并，将源对象的所有可枚举属性，复制到目标对象；

   ```js
       const a = {
           name:'ran',
           age:12
       }
       const b = {
           pass:'i love you'
       }
       console.log(Object.assign(a,b))   //{ age:'12', name:'ran', pass:'i love you' }
   ```

3. **proto**、setPrototypeOf、 setPrototypeOf 可以直接设置对象的原型；

```js
	//3.Object.setPrototypeOf 设置原型对象 Object.getPrototypeof
    const school = {
        name:'尚硅谷'
    }
    const cities = {
        xiaoqu:['北京','上海']
    }
    Object.setPrototypeOf(school,cities)
    console.log(Object.getPrototypeOf(school))  //{xiaoqu: Array(2)}
    console.log(school)  //{name: "尚硅谷"}
```





# 模块化

类似于一个公司由各个部门组成，一个工程也由各个模块组成，高内聚低耦合，各司其职。先理解一下概念

> 模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来；

### 好处

模块化的优势有以下几点：

1. 防止命名冲突；
2. 代码复用（模块化的封装）；
3. 高维护性；

### 模块化规范

**ES6 之前**的模块化规范有：

1. CommonJS  =>  NodeJS、Browserify； 

   `COMMONJS`：

   ```js
   // 通过require函数来引用
   const math = require("./math");
   
   // 通过exports将其导出
   exports.getSum = function(a,b){
   	return a + b;
   }
   ```

2. AMD（Asynchronous Module Definition(异步模块定义)）=> requireJS； 

3. CMD => seaJS；

**ES6 MODULE**

> （使用最多）

```js
// 通过import函数来引用
import math from "./math";

// 通过export将其导出
export function sum(a, b){
	return a + b;
}
```



### 作用域

定义：运行时变量、函数、对象可访问性

> 作用域决定了代码中变量和其他资源的可见性

#### 全局作用域

```js
    var a = 1;    
    window.a; // 1    
    global.a; // 1 
```

#### 局部作用域

```js
    function a(){
        var v = 1;
    }
    window.v; // undefined
```

如果在传统 `js` 写法中，引入多个 `script`，就很容易造成全局作用域冲突而导致不可预测的问题：

```js
	<body>
    	<script scr="./moduleA.js"></sciprt>
        <script scr="./moduleB.js"></sciprt>
        <script scr="./moduleC.js"></sciprt>
    </body>
```

改进步骤一，使用变量作用域形成局部作用域：

```js
// 定义模块内的局部作用域，以moduleA为例
    var Susan = {
    	name: "susan",
        sex: "female",
        tell: function(){
        	console.log("im susan")
        }
    }
```

但是步骤一无法保证模块属性内部安全性，比如可能不小心改掉属性值，可以通过立即执行函数进行改写，形成闭包。
那么可以进行改进步骤二：
`ps`：什么是[立即执行函数](https://blog.csdn.net/qq_33457248/article/details/80773496)（参考资料： ）？
		     什么是[自由变量](https://www.cnblogs.com/pssp/p/5206240.html)（参考资料：）？简单来说是跨作用域的变量

```js
	// 定义模块内的闭包作用域（模块作用域），以moduleA为例
    var SusanModule = (function(){
        var Susan = {
        // 自由变量
    	name: "susan",
        // 自由变量
        sex: "female",
        // 只允许访问tell方法，不能访问和修改其他属性
        return {
        	tell: function(){
        		console.log("im susan")
        	}
        }
    })()
```

对于步骤二还有一种写法，推荐使用这种写法，也是早期模块实现的方法

```js
	// 定义模块内的闭包作用域（模块作用域），以moduleA为例
    (function(window){
    	var name = "susan"
        var sex = "female"
        functioon tell(){
        	console.log("im ", this.name)
        }
        window.susanModule = {tell}
    })(window)// window作为参数传给
```



### ES6 模块化语法

模块功能主要有两个命令构成：export 和 inport

- export命令用于规定模块的对外接口
- inport命令用于输入其他模块提供的功能

**简单使用**

`m.js`（导出模块）：

```js
export let school = '尚硅谷'
export function teach(){
    console.log('教技能')
}
```

`模块化.html`（导入和使用模块）：

```html
<script type="module">
    import * as m1 from "./src/js/m1.js";
	console.log(m1);
</script>
```



### 暴露语法汇总

1. 统一暴露

   ```js
   //统一暴露
   let school = '尚硅谷';
   function findjob(){
       console.log('找工作吧');
   }
   export {school,findjob}
   ```

2. 默认暴露

   ```js
   //默认暴露
   export default {
       school:'ATGUIGU',
       change:function(){
           console.log('我们可以改变你')
       }
   }
   ```

3. 分别暴露

   ```js
   // 分别暴露） 
   export let school = "尚硅谷"; 
   export function teach(){ 
   	console.log("我们可以教你开发技术！"); 
   }
   ```

   

### 引入语法汇总

1. 通用导入方式

   ```js
   import * as m1 from "./src/js/m1.js"
   import * as m2 from "./src/js/m2.js"
   import * as m3 from "./src/js/m3.js"
   ```

2. 解构赋值方式

   ```js
   import {school,teach} from "./src/js/m1.js"
   // 重名的可以使用别名
   import {school as guigu,findJob} from "./src/js/m2.js"
   // 导入默认导出的模块，必须使用别名
   import {default as m3 } from "./src/js/m3.js"
   ```

3. 简便形式（只针对默认暴露）

   ```JS
   import m3 from "./src/js/m3.js"
   ```



### 使用模块化的另一种方式

将js语法整合到一个文件app.js：

```js
// 引入m.js模块内容
import * as m from "./m.js"; 
console.log(m); 
console.log(m.school); 
m.teach();
```

引入：

```html
<script src="./src//js/app.js" type=modeule></script>
```





### Babel对ES6模块化代码转换

Babel 是一个 JavaScript 编译器；

> Babel 能够将新的ES规范语法转换成ES5的语法；

步骤：使用Babel转换JS代码——打包成一个文件——使用时引入即可；

##### 步骤

第一步：安装工具

- babel-cli（命令行工具）
- babel-preset-env（ES转换工具） 
- browserify（打包工具，项目中使用的是webpack）；

第二步：初始化项目

```shell
npm init -y
```

第三步：安装

```shell
npm i babel-cli babel-preset-env browserify
```

第四步：使用babel转换

```shell
npx babel js（js目录） -d dist/js（转化后的js目录） --presets=babel-preset-env
```

第五步：打包

```shell
npx browserify dist/js/app.js -o dist/bundle.js
```

第六步：在使用时引入bundle.js

```shell
<script src="./js/bundle.js" type="module"></script>
```



# ES7

#### Array.prototype.includes

> 1. Includes 方法用来检测数组中是否包含某个元素，返回布尔类型值；
> 2. 判断数组中是否包含某元素，语法：arr.includes(元素值)； 
>
> ```js
> //include
> const mingzhu = ['西游记','红楼梦','水浒传','三国演义']
> console.log(mingzhu.includes('西游记'))  //true
> console.log(mingzhu.includes('金瓶梅'))  //false
> ```

#### 指数操作符

> 在 ES7 中引入指数运算符「**」，用来实现幂运算，功能与 Math.pow 结果相同；

幂运算的简化写法，例如：2的10次方：2**10；

```js
// 指数操作符 
console.log(Math.pow(2,10)) 	//1024
console.log(2**10);		//1024
```





# ES8

### async函数

> async和await两种语法结合可以让异步代码像同步代码一样

async函数：

- async函数的返回值为promise对象
- async返回的promise对象的结果值由async函数执行的返回值决定

> 1. 如果返回的是一个非Promise的对象(return 123)，则fn()返回的结果就是成功状态的Promise对象，值为返回值
> 2. 如果返回的是一个Promise对象，则fn() 返回的结果与内部Promise对象的结果一致
> 3. 如果返回的是抛出错误，则fn() 返回的就是失败状态的Promise对象

```js
// async函数：异步函数 
async function fn(){ 
    return new Promise((resolve,reject)=>{ 
        // resolve("成功啦！"); 
        reject("失败啦！"); 
    }) 
}

const result = fn(); 
// console.log(result); // 返回的结果是一个Promise对象 

// 调用then方法 
result.then(value => { 
	console.log(value); 	//成功的数据
},reason => { 
	console.warn(reason); 
}); 
```



## await表达式

1. await必须放在async函数中
2. await右侧的表达式==一般为promise对象==
3. await可以返回的是右侧promise成功的值
4. await右侧的promise如果失败了，就会抛出异常，需要通过try…catch捕获处理

```js
<script>
    //创建Promise对象
    const p = new Promise((resolve, reject) => {
        // resolve("成功的值")
        reject("失败了")
    })

    //await 必须放在async函数中
    async function main() {
        try {
            let res = await p;
            console.log(res);
        } catch (e) {
            console.log(e);
        }
    }

    //调用函数
    main()  //失败了
</script>
```

应用：发送AJAX请求

```js
	//ajax请求返回一个promise
    function sendAjax(url){
        return new Promise((resolve, reject) => {
        
            //创建对象
            const x =new XMLHttpRequest();
    
            //初始化
            x.open('GET',url);
    
            //发送
            x.send();
    
            //时间绑定
            x.onreadystatechange = ()=>{
                if(x.readyState === 4 ){
                    if(x.status >= 200 && x.status < 300){
                        //成功
                        resolve(x.response)
                    }else {
                        //失败
                        reject(x.status)
                    }
                }
            }
        })
    }

   //async 与 await 测试
    async function main(){
        let result = await sendAjax("https://api.apiopen.top/getJoke")
        console.log(result);
    }
    main()
```



## 对象方法扩展

```js
	const school = {
        name:'尚硅谷',
        cities:['北京','上海','深圳'],
        xueke:['前端','Java','大数据','运维']
    };
	
	//获取对象所有的键
    console.log(Object.keys(school));
```

1. Object.values()方法：返回一个给定对象的所有可枚举属性值的数组；

   ```js
   //获取对象所有的值
   console.log(Object.values(school));
   ```

2. Object.entries()方法：返回一个给定对象自身可遍历属性 [key,value] 的数组；

   ```js
   //entries,用来创建map
   console.log(Object.entries(school));
   console.log(new Map(Object.entries(school)))
   ```

3. Object.getOwnPropertyDescriptors()该方法：返回指定对象所有自身属性的描述对象；

   ```js
   //对象属性的描述对象
   console.log(Object.getOwnPropertyDescriptors(school))
   
   const obj = Object.create(null,{
       name:{
           value:'尚硅谷',
           //属性特性
           writable:true,
           configurable:true,
           enumerable:true,
       }
   })
   ```

   ![image-20210813010213066](https://i.loli.net/2021/08/13/TqoYJesPlSaR1rX.png)





# ES9

## **Rest** **参数与** **spread** 扩展运算符

> Rest 参数与 spread 扩展运算符在 ES6 中已经引入，不过 ES6 中只针对于数组，在 ES9 中为对象提供了
> 像数组一样的 rest 参数和扩展运算符；

```js
 <script>
    function connect({host,port,...user}){
        console.log(host);
        console.log(port);
        console.log(user)
    }
    connect({
        host:'127.0.0.1',
        port:3306,
        username:'root',
        password:'root',
        type:'master'
    })  //127.0.0.1  3306  {username: "root", password: "root", type: "master"}

</script>
```

```js
<script>
    const AA={
        username:'ran'
    }
    const BB={
        password:'lyyrhf'
    }
    const CC={
        job:'Java'
    }
    const D={...AA,...BB,...CC};
	// ...AA => username: 'ran'
    console.log(D) //{username: "ran", password: "lyyrhf", job: "Java"}
</script>
```



## 正则扩展

#### 命名捕获分组

```js
// 声明一个字符串 
let str = '<a href="http://www.baidu.com">hello</a>'; 
```

// 需求：提取url和标签内文本 

```js
// 之前的写法 
const reg = /<a href="(.*)">(.*)<\/a>/; 

// 执行 
const result = reg.exec(str); 
console.log(result); 

// 结果是一个数组，第一个元素是所匹配的所有字符串 
// 第二个元素是第一个(.*)匹配到的字符串 
// 第三个元素是第二个(.*)匹配到的字符串 
// 我们将此称之为捕获 

console.log(result[1]); 
console.log(result[2]); 
```

![image-20210813023352534](https://i.loli.net/2021/08/13/gz47WuRsMbPvYLk.png)

```js
// 命名捕获分组 
const reg1 = /<a href="(?<url>.*)">(?<text>.*)<\/a>/; 

const result1 = reg1.exec(str); 
console.log(result1); 

console.log(result1.groups.url); 
console.log(result1.groups.text); 
```

![image-20210813023259087](https://i.loli.net/2021/08/13/GTKvJMZeyOjgVw6.png)



#### 反向/正向断言

> ES9 支持反向断言，通过对匹配结果前面的内容进行判断，对匹配进行筛选；

```js
// 字符串 
let str = "JS5201314你知道么555啦啦啦"; 

// 需求：我们只想匹配到555 

// 正向断言 
const reg = /\d+(?=啦)/; // 前面是数字后面是啦 
const result = reg.exec(str); 
console.log(result); 

// 反向断言 
const reg1 = /(?<=么)\d+/; // 后面是数字前面是么 
const result1 = reg.exec(str); 
console.log(result1); 
```





#### **dotAll** 模式

> 正则表达式中点.匹配除回车外的任何单字符，标记『s』改变这种行为，允许行终止符出现；

```js
// dot就是. 元字符，表示除换行符之外的任意单个字符 
let str = ` 
    <ul>
        <li>
            <a>肖生克的救赎</a> 
            <p>上映日期: 1994-09-10</p> 
        </li> 

        <li>
            <a>阿甘正传</a> 
            <p>上映日期: 1994-07-06</p> 
        </li> 
    </ul> 
   `;

// 需求：我们想要将其中的电影名称和对应上映时间提取出来，存到对象 

// const reg = /<li>\s+<a>(.*?)<\/a>\s+<p>(.*?)<\/p>/; 
// const result = reg.exec(str); 
// console.log(result); 

// dotAll 模式 
const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs; 	// g是全局模式
let result; 
let data = []; 
while(result = reg.exec(str)){ 
	console.log(result); 
	data.push({title:result[1],time:result[2]}); 
}
console.log(data); 
```



# ES10

###  对象扩展方法

> **Object.fromEntries**
>
> - 将二维数组或者map转换成对象；
> - 之前学的`Object.entries`是将对象转换成二维数组；

```js
<script>
   //二维数组
   const res = Object.fromEntries([
       ['name','冉海锋'],
       ['cities','成都','武汉']
   ])
   console.log(res) //{name: "冉海锋", cities: "成都"}

   //Map
   const m = new Map();
   m.set('name','ranhaifeng')
   const result = Object.fromEntries(m)
   console.log(result); //{name: "ranhaifeng"}
</script>
```



### 字符串扩展方法

> **trimStart** 和 **trimEnd**：去掉字符串前后的空白字符；

```js
<script>
   //trim
   let str= ' asd  '
   console.log(str) //asd
   console.log(str.trimStart()) //asd  清空头空格
   console.log(str.trimEnd()) //  asd  清空尾空格
</script>
```



### flat与flatMap

> 将多维数组转换成低维数组；

```js
<script>
    const arr = [1,2,3,[4,5,6,[7,8,9]]]
    //参数为深度，是一个数字
    console.log(arr.flat(2)) //[1,2,3,4,5,6,7,8,9]


	const arr2=[1,2,3,4]
	const result = arr2.flatmap(item => [item * 10]); //如果map的结果是一个多维数组可以进行flat 是两个操作的结合

</script>
```





### Symbol的description

> 获取Symbol的描述字符串；

```js
let s = Symbol('尚硅谷');
console.log(s.description) //尚硅谷
```



# ES11

### String.prototype.matchAll

> 用来得到正则批量匹配的结果；

```js
let str = ` 
    <ul>
        <li>
            <a>肖生克的救赎</a> 
            <p>上映日期: 1994-09-10</p> 
        </li> 

        <li>
            <a>阿甘正传</a> 
            <p>上映日期: 1994-07-06</p> 
        </li> 
    </ul> 
`;

// 正则 
const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/sg; 
const result = str.matchAll(reg); // 返回的是可迭代对象，可用扩展运算符展开 // console.log(...result); 
// 使用for...of...遍历 
for(let v of result){ 
	console.log(v); 
}
```



### 私有属性

> 私有属性外部不可直接访问；

```js
<script>
    class Person {
        //公有属性
        name;
        //私有属性
        #age;
        #weight;

        //构造方法
        constructor(name, age, weight) {
            this.name = name;
            this.#age = age;
            this.#weight = weight;
        }
        intro(){
            console.log(this.name);
            console.log(this.#age);
            console.log(this.#weight);
        }
    }
    
    //实例化
    const girl = new Person('冉', 18, '45kg');
    console.log(girl); 			//Person{name: "冉", #age: 18, #weight: "45kg"}
	// 公有属性的访问 
	console.log(girl.name);		// 冉
	// 私有属性的访问
    console.log(girl.#age) 		//error
    girl.intro(); 				// 冉 18  45kg
</script>
```



### Promise

> **Promise.allSettled**：获取多个promise执行的结果集；

```js
<script>
    //声明两个promise对象
    const p1 = new Promise((resolve, reject) => {
        setTimeout(()=>{
            resolve('商品数据-1')
        },1000)
    })


    const p2 = new Promise((resolve, reject) => {
        setTimeout(()=>{
            reject('出错了！')
        },1000)
    })
    
    //调用allsettled方法:返回的结果始终是一个成功的，并且异步任务的结果和状态都存在
    const res = Promise.allSettled([p1,p2]);
    console.log(res)
    
    // Promise {<pending>}
    //     __proto__: Promise
    //     [[PromiseState]]: "fulfilled"
    //     [[PromiseResult]]: Array(2)
    
    //调用all方法：返回的结果是按照p1、p2的状态来的，如果都成功，则成功，如果一个失败，则失败，失败的结果是失败的Promise的结果
    const result = Promise.all([p1,p2])
    console.log(result)

</script>
```



### 可选链操作符

> `?.`：如果存在则往下走，省略对对象是否传入的层层判断；

```js
//相当于一个判断符，如果前面的有，就进入下一层级
function main(config){
    const dbHost = config?.db?.host
    console.log(dbHost) //192.168.1.100
}

main({
    db:{
        host:'192.168.1.100',
        username:'root'
    },
    cache：{
    	host:'192.168.1.200',
    	username:'admin'
	}
})
```



### 动态import

> 动态导入模块，什么时候使用时候导入；

hello.js：

```js
export defalt{
    alert('hello')
}
```

app.js：

```js
// import * as m1 from "./hello.js"; // 传统静态导入
btn.onclick = function(){
    //使用之前并未引入，动态引入，返回的其实是一个Promise对象
    import('./hello.js').then(module=>{
        module.hello();
    })
}
```



### BigInt类型

> 更大的整数

```js
//大整型
let n = 521n;
console.log(n,typeof(n))  // 521n  n 

//函数
let n = 123;
console.log(BigInt(n)) // 123n  //不要使用浮点型，只能用int

//大数值运算
let max = Number.MAX_SAFE_INTEGER; // 9007199254740991
console.log(max +1) // 9007199254740992
console.log(max +2) // 9007199254740992 出问题了
console.log(BigInt(max)+BigInt(1)) 9007199254740992n
console.log(BigInt(max)+BigInt(2)) 9007199254740993n
```



## globalThis对象

> 绝对全局对象：始终指向全局对象window；

```js
console.log(globalThis) //window  //适用于复杂环境下直接操作window
```

































