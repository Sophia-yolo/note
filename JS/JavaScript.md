# 引入方式

### 外部JavaScript

```js
<script src="js/index.js">
```

> 表示引入文件名为“index.js”的JavaScript文件，其中文件的路径是“js/index.js”



### 内部JavaScript

```js
<script type="text/javascript">
    ……
</script>
```

> 内部JavaScript文件一般在head中引入，也可在body中引用





# JavaScript基础

## 基本输入输出方法

- document.write()：在页面输出一个内容。

- document.body.innerHTML     在网页中所要显示出来的内容,

- alert()：弹出一个警告消息框。

- console.log()

- confirm()：弹出一个消息确认框👉同步等待

- prompt()：弹出带输入框的提示框，弹出框优先级别较高

  > 优先级别：confirm() > prompt() > console.log()

- open(url，字符串，特殊含义字符串)



## 变量和常量

### 变量

——变量的值在程序运行过程中是可以改变的。

> **在JavaScript中，所有变量都是用var声明**。

###### 命名

> - 变量由字母、下划线、`$`或数字组成，并且第一个字母必须是“字母、下划线或`$`”。
> - 变量不能是系统关键字和保留字。

###### 使用

- 变量的声明
- 变量的赋值



### 常量

——常量指的是一个不能改变的量。即常量的值从定义开始就是固定的，一直到程序结束都不会改变。



## 数据类型

### 基本数据类型

- 数字型（number型）：整数、浮点数

  > NaN，即非数值（Not a Number）是一个特殊的数值，JS中当对数值进行计算时没有结果返回，则返回NaN

- 字符串型（string型）：如"绿叶学习网"；

  > PS：单引号括起来的字符串中，不能含有单引号，只能含有双引号。同样的道理，双引号括起来的字符串中，也不能含有双引号，只能含有单引号。

- 布尔型（Boolean型）：true或fasle；

- 空值（null型）；

- 未定义值（undefined型）；

- [symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) ([ECMAScript](https://developer.mozilla.org/zh-CN/docs/Glossary/ECMAScript) 2016新增)。 -->[`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 对象是 Symbol原始值的[封装 (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/Wrapper) 。

- [bigint](https://developer.mozilla.org/zh-CN/docs/Glossary/BigInt)， -->**BigInt** 是一种数字类型的数据，它可以表示任意精度格式的整数。

### 对象(引用)类型

> 1. object：任意对象
> 2. function：一种特别的对象（可以执行）
> 3. Array：一种特别的对象（数值下标，内部数据有序）

### 转义字符

- 如果是在document.write()中换行，则应该用：`<br/>`
- 如果是在alert()中换行，则应该用：`\n`





## 类型转换

> 类型转换就是指将其他的数据类型，转换为String Number 或 Boolean

### 强制类型转换

1. Number()	//只能将纯“数字型字符串”转换为数字👉Number("2018")

> 转换的情况：
>
> 1. 字符串 > 数字
>    如果字符串是一个合法的数字，则直接转换为对应的数字
>    如果字符串是一个==非法的数字==，则转换为==NaN==
>    如果是一个空串或纯空格的字符串，则转换为0
> 2. 布尔值 > 数字：布尔值 true 转换为1，false转换为0
> 3. 空值 > 数字：null转换为0
> 4. 未定义（undefined 转换为NaN） > 数字

2. ```js
   parseInt()  //将字符串型转换为整型
   parseFloat()  //将字符串型转换为浮点型
   ```

3. Boolean()	//转换为布尔值

> 转换的情况
>
> - 字符串 > 布尔（除了空串其余全是true）
>
> - 数值 > 布尔（除了0和NaN其余的全是true）
>
> - null、undefined > 布尔（都是false）
> - 对象 > 布尔（都是true）

4. .toString()	//将数值型数据（整型或浮点型）转换为字符串

> **这个方法不适用于null和undefined**

5. String()	//转换为字符串

> **对于Number Boolean String都会调用他们的toString()方法来将其转换为字符串，对于null值，直接转换为字符串”null”。对于undefined直接转换为字符串”undefined”**



### 隐式的类型转换

1. 与空字符串相加

   ```js
   var a = 2018 + "";
   var b = a + 1000;
   document.write(b);
   
   //输出20181000
   ```

2. 为任意的数据类型做两次非运算，即可将其转换为布尔值（==隐式类型转换==）：

   ```js
   var a = "hello";  
   a = !!a; //true
   ```



## 运算符

- 算术运算符；

  ![image-20210802112027189](https://i.loli.net/2021/08/02/sVWCn54ZpyE7Q6I.png)

  > 运算符在前置时，表达式值等于变量原值。
  >
  > 运算符在后置是，表达式值等于变量变更以后的值

- 关系运算符

  > 小于（<） 、大于（>） 、小于等于（<=）和大于等于（>=）

- 赋值运算符

  >  = 、+= 、-=、*=、/=、%=

- 逻辑运算符；

  > 非使用符号 ! 表示，与使用 && 表示，或使用 || 表示

- 条件运算符

  > - var a = 条件 ? 表达式1 : 表达式2；

- **typeof** 运算符：返回数据类型的字符串表达

  > 1. 判断数值、字符串、布尔值、undefined、function
  > 2. 不能区别：null/object，object/array

- **instanceof**：判断对象的具体类型，结果为true/false

- **===**：判断undefined/null，结果为true/false

  > `===`表示全等，他和`==` 基本一致，不过 == 在判断两个值时会进行自动的类型转换，而===不会。

- == 

  ![image-20210802112753433](https://i.loli.net/2021/08/02/5uYP2qrmlQgBS4U.png)
  
  > 判断一个值是否是NaN
  > 使用isNaN()函数



## 流程控制语句

### 选择结构

1. if语句
2. if……else语句
3. if……else if……语句
4. if语句的嵌套
5. switch语句;

### 循环结构

1. while语句

2. do……while语句

3. for语句；

   label

   使用 label 语句可以在代码中添加标签，以便将来使用。 

   语法：

   – label: statement

   例子：

   ```js
   start: for (var i=0; i < count; i++) {
   	alert(i);
   }
   ```

   这个例子中定义的 start 标签可以在将来由 break 或 continue 语句

   引用。加标签的语句一般都要与 for 语句等循环语句配合使用。


### 跳转语句

1. break语句	👉 彻底结束循环
2. continue语句   👉 结束本次循环





## 对象

- 多个数据的封装体（集合体）。
- 用于保存多个数据的容器。
- 一个对象代表现实中的一个事物（代表现实中的某个事物 ，是该事物在编程中的抽象）。

### 创建对象

方式一：

```js
var obj = new Object();
```

复制

方式二：

```js
var obj = {};
```

#### 向对象中添加属性

> 语法：对象.属性名 = 属性值;

### 遍历

语法：”属性名” in 对象

```js
//循环遍历对象自身的和继承的可枚举属性(不含Symbol属性).  
var obj = {'0':'a','1':'b','2':'c'};  
  
for(var i in obj) {  
     console.log(i,":",obj[i]);  
}
```

**使用对象字面量，在创建对象时直接向对象中添加属性**
语法：

```js
var obj = {  
    属性名:属性值,  
    属性名:属性值,  
    属性名:属性值,  
    属性名:属性值  
}
```



## 函数

### 函数定义

> **如果return后不跟值，或者是不写return则函数默认返回undefined。**

##### 1. 不指定函数名的函数（匿名函数）

```js
function(参数1,参数2,….,参数n)
{
    //函数体语句
}
```

##### 2. 指定函数名的函数（命名函数）

```js
function 函数名(参数1,参数2,….,参数n)
{
    //函数体语句
    return 表达式;

}
```



### 函数的调用

#### 直接调用

> 函数名(实参1, 实参2, ... , 实参n);

#### 表达式中调用

#### 超链接中调用

```js
<!DOCTYPE html> 
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <script>
        function expressMes()
        {
            alert("她：我爱helicopter。\n我：oh~my，= =?!");
        }
    </script>
</head>
<body>
    <a href="javascript:expressMes()">表白对话</a>
</body>
</html>
```

#### 事件中调用

```js
<!DOCTYPE html> 
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <script>
        function alertMes()
        {
            alert("绿叶，给你初恋般的感觉~");
        }
    </script>
</head>
<body>
    <input type="button" onclick="alertMes()" value="提交" />
</body>
</html>
```



### 立即执行函数

> 函数定义完，立即被调用，这种函数叫做立即执行函数

立即执行函数往往只会执行一次

```js
(function(a,b){  
    console.log("a = "+a);  
    console.log("b = "+b);  
})(123,456);
```



### 特殊函数

#### 嵌套函数

#### 递归函数

> 满足三个条件：
>
> 1. 函数自己调用自己
> 2. 一般情况有参数
> 3. 一般情况有return

方法：

1. 寻找临界值
2. 找这次和上次的关系
3. 假设当前函数已经使用，调用自身计算上一次



#### 内置函数

##### 1. eval()函数

> PS：可以把一个字符串当做一个JavaScript表达式一样去执行它

##### 2. isFinite()函数

> 用来确定某一个数是否是一个有限数值。
>
> > PS：如果该参数为非数字、正无穷数和负无穷数，则返回false；否则的话，返回true。如果是**字符串类型的数字，就会自动转化为数字型。**

##### 3. isNaN()函数

> NaN指的是“Not a Number（非数字）——如果第1个字符不是数字

##### 4. parseInt()函数

##### 5. parseFloat()函数

##### 6. escape()函数

PS：对字符串进行编码，以便它们能在所有计算机上可读

语法：`escape(charString)`👉 charString是必选参数，表示要进行编码的字符串或文字。

说明：

escape()函数返回一个包含charString内容的字符串值（Unicode格式）。

除了个别如`“*@”`之类的符号外，其余所有`空格`、`标点符号`以及其他`非ASCII字符`均可用`“%xx”`这种形式的编码代替，其中xx等于表示该字符的十六进制数。

##### 7. unescape()函数



### 函数的属性和方法

#### 方法

call()
apply()

> 这两个方法都是函数对象的方法需要通过函数对象来调用

通过两个方法可以直接调用函数，并且**可以通过第一个实参来指定函数中this**

不同：

1. call是直接传递函数的实参
2. apply需要将实参封装到一个数组中传递



#### 函数参数arguments

arguments中有一个属性callee表示当前执行的函数对象

> 1. argument.length
> 2. argument[下标]

#### REST

由于JavaScript函数允许接收任意个参数，所以不得不用arguments来获取函数定义a以外的参数。

```js
function exm(a) {
    var rest = [];
    if (arguments.length > 1) {
        for (var i = 1; i<arguments.length; i++) {
            rest.push(arguments[i]);
        }
    }
```

ES6：用在函数最后，多余的参数以数组的形式交给变量rest，如果传入的参数未填满函数定义的参数，rest会是一个空数组。



### 内置对象和常用方法

#### 字符串对象：String

PS：*isNaN()对空格字符会转化为0，需要加个判断charAt(i)不能为空格*

##### 大小写转换

> - 字符串名.toLowerCase() 
> - 字符串名.toUpperCase()

##### charAt()

> 字符串名.charAt(n)       //获取字符串中的某一个字符

##### concat()

> 字符串1.concat(字符串2,字符串3,…,字符串n);
>
> 👉PS：将“字符串2,字符串3,…,字符串n”按照顺序连接到字符串1的尾部，并返回连接后的字符串。

##### localeCompare()

> 字符串1.localeCompare(字符串2)
>
> - 如果字符串1小于字符串2，则返回小于0的数字；
> - 如果字符串1大于字符串2，则返回数字1；
> - 如果字符串1等于字符串2，则返回数字0；

##### substring()

> 字符串名.substring(start, end)        //截取字符串的某一部分👉集合：[start,end)
>
> > 截取的下标是从0开始的，也就是说0表示第1个字符，1表示第2个字符……n表示第n+1个字符。对于字符串操作来说，凡是涉及下标，都是从0开始。
> >

##### replace()

> - 字符串名.replace(**原字符串**, 替换字符串) 👉只替换一个
> - 字符串名.replace(**正则表达式**, 替换字符串)👉替换所有

##### split()

PS：分割符可以是一个字符、多个字符、一个空格或一个正则表达式。此外，分割符并不作为返回数组元素的一部分。

```js
字符串名.split("分割符")
```

> `split(" ")`和`split("")`是不一样的

##### 检索字符串的位置

- ⭐字符串名.indexOf(指定字符串)  👉返回指定字符串首次出现的下标

  PS：返回的是字符串的位置

- 字符串名.lastIndexOf(指定字符串) 👉返回指定字符串最后出现的下标

  > PS：如果字符串中不包含“指定字符串”`，indexOf()`或`lastIndexOf()`就会返回**-1**

- match()

  PS：match()方法就是用来检索一个字符串是否存在。如果存在的话，返回要检索的字符串；如果不存在的话，返回null。

  > ```js
  > stringObject.match(字符串)  ``//匹配字符串;
  > stringObject.match(正则表达式) ``//匹配正则表达式
  > ```

- search()

  PS：stringObject指的是字符串对象。search()方法返回的是子字符串的起始位置，如果没有找到任何匹配的子串，则返回-1。

##### **`trim()`** 方法

> 会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR等）。



#### 数组对象：Array

##### 数组的创建

> - var 数组名 = new Array(元素1, 元素2, ……, 元素n);    *//完整形式* 
> - var 数组名 = [元素1, 元素2, ……, 元素n];             *//简写形式*

##### 获取数组长度

> 数组名.length

##### 方法

| function name | function                                                     | usage                                   |
| :------------ | :----------------------------------------------------------- | :-------------------------------------- |
| push()        | 用来向数组的末尾添加一个或多个元素，并返回数组新的长度       | 语法：数组.push(元素1,元素2,元素N)pop() |
| pop()         | 用来删除数组的最后一个元素，并返回被删除的元素               |                                         |
| unshift()     | 向数组的开头添加一个或多个元素，并返回数组的新的长度         |                                         |
| shift()       | 删除数组的开头的一个元素，并返回被删除的元素                 |                                         |
| reverse()     | 可以用来反转一个数组，它会对原数组产生影响                   |                                         |
| concat()      | 可以连接两个或多个数组，它不会影响原数组，而是新数组作为返回值返回 |                                         |

##### splice()

```
可以用来删除数组中指定元素，并使用新的元素替换  
   该方法会将删除的元素封装到新数组中返回  
参数：  
   1.删除开始位置的索引  
   2.删除的个数  
   3.三个以后，都是替换的元素，这些元素将会插入到开始位置索引的前边
```

##### slice(sart,[end])

```
可以从一个数组中截取指定的元素  
该方法不会影响原数组，而是将截取到的内容封装为一个新的数组并返回  
参数：  
   1.截取开始位置的索引（包括开始位置）  
   2.截取结束位置的索引（不包括结束位置）  
        第二个参数可以省略不写，如果不写则一直截取到最后  
    参数可以传递一个负值，如果是负值，则从后往前数 
```

##### join([splitor])

可以将一个数组转换为一个字符串
参数：
需要一个字符串作为参数，这个字符串将会作为连接符来连接数组中的元素

PS：使用默认符号（,）

> 数组名.**join**("连接符");👉将数组中的所有元素连接成一个字符串。

##### sort()

可以对一个数组中的内容进行排序，默认是按照Unicode编码进行排序

> 数组名.sort(函数名)

```js
<script>
    //定义一个升序函数
    function up(a, b) 
    {
        return a - b;
    }
    //定义一个降序函数
    function down(a, b) 
    {
        return b - a;
    }
    //定义数组
    var arr = [3, 9, 1, 12, 50, 21];
    arr.sort(up);
    document.write("升序：" + arr.join("、") + "<br/>");
    arr.sort(down);
    document.write("降序：" + arr.join("、"));
</script>
```

> **正序排序原理：**
>
> - return a-b 这段代码：a指的是array[j] b指的是array[j+1] 即 a 指的是前一个数，b指的是后一个数；
> - a-b>0时，也就是 第一个数比第二个数大 则 在if语句中 fncompare()函数的结果 为>0

##### 遍历数组

> 遍历数组就是将数组中元素都获取到

方法一：

```js
for(var i=0 ; i<数组.length ; i++){  
    //数组[i]  
}
```

方法二：

使用forEach()方法来遍历数组（不兼容IE8）

```js
数组.forEach(function(value , index , obj){  
  
});
```

forEach()方法需要一个==回调函数作为参数==，
数组中有几个元素，回调函数就会被调用几次，每次调用时，都会将遍历到的信息以实参的形式传递进来，
我们可以定义形参来获取这些信息。

> - value:正在遍历的元素
> - index:正在遍历元素的索引
> - obj:被遍历对象





#### 日期对象：Date

语法：

```js
var 日期对象名 = new Date();
```

创建一个指定的时间对象

```js
var d = new Date("月/日/年 时:分:秒");
```

##### 获取年、月、日

| 方法          | 说明                                              |
| :------------ | :------------------------------------------------ |
| getFullYear() | 获取年份，取值为4位数字                           |
| getMonth()    | 获取月份，取值为0（一月）到11（十二月）之间的整数 |
| getDate()     | 获取日数，取值为1~31之间的整数                    |

##### 设置年、月、日

1. setFullYear

   PS：`时间对象.setFullYear(year,month,day);`👉year表示年，是必选参数

2. setMonth()

   PS：`时间对象.setMonth(month, day);`👉month表示月，是必选参数

3. setDate()

   PS：`时间对象.setDate(day);`

##### 获取时分秒

| 方法         | 说明                             |
| :----------- | :------------------------------- |
| getHours()   | 获取小时数，取值为0~23之间的整数 |
| getMinutes() | 获取分钟数，取值为0~59之间的整数 |
| getSeconds() | 获取秒数，取值为0~59之间的整数   |

##### 设置时、分、秒

1. setHours()

   > 时间对象.setHours(hour, min, sec, millisec);
   >
   > > 说明：
   > >
   > > hour是**必选参数**，表示时，取值为0~23之间的整数。
   > >
   > > min是可选参数，表示分，取值为0~59之间的整数。
   > >
   > > sec是可选参数，表示秒，取值为0~59之间的整数。
   > >
   > > millisec是可选参数，表示毫秒，取值为0~999之间的整数。

2. setMinutes()

   > 时间对象.setMinutes( min, sec, millisec);

3. setSeconds()

   > 时间对象.setSeconds(sec, millisec);

##### 获取星期几

PS：getDay()返回一个数字，其中0表示星期天，1表示星期一……6表示星期六。

> 时间对象.getDay();



#### 数值对象：Math

:star:Math.PI

PS：例如180°就应该写成Math.PI，而360°就应该写成Math.PI*2

> - Math.属性 
> - Math.方法

###### Math对象中的方法（常用）

|     方法     | 说明                                                         |
| :----------: | :----------------------------------------------------------- |
| max(a,b,…,n) | 返回一组数中的最大值                                         |
| min(a,b,…,n) | 返回一组数中的最小值                                         |
|    sin(x)    | 正弦                                                         |
|    cos(x)    | 余弦                                                         |
|    tan(x)    | 正切                                                         |
|   asin(x)    | 反正弦                                                       |
|   acos(x)    | 反余弦                                                       |
|   atan(x)    | 反正切                                                       |
| atan2(y, x)  | 反正切（注意y、x顺序）：**atan2(y, x)能够精确判断角度对应哪一个角** |
|   floor(x)   | 向下取整：返回小于或等于指定数的“最近的那个整数”             |
|   ceil(x)    | 向上取整：返回大于或等于指定数的“最近的那个整数”             |
|   random()   | 生成随机数：[0, 1)                                           |

###### Math对象中的方法（不常用）

| 方法     | 说明                     |
| :------- | :----------------------- |
| abs(x)   | 返回x的绝对值            |
| sqrt(x)  | 返回x的平方根            |
| log(x)   | 返回x的自然对数（底为e） |
| pow(x,y) | 返回x的y次幂             |
| exp(x)   | 返回e的指数              |





# BOM

**浏览对象模型**（Browser Object Model ）：一个窗口  👉 把浏览器当作一个对象来看待

- BOM的顶级对象是window
- BOM学习的是浏览器窗口交互的一些对象
- BOM是浏览器厂商在各自浏览器上定义视为，兼容性比较差

## BOM的构成

![4](https://i.loli.net/2021/08/03/JPRT2tpXrdIO7jv.png)

1. BOM 比 DOM 更大。它包含 DOM。

2. window 对象是浏览器的顶级对象，它具有双重角色

3. 它是 JS 访问浏览器窗口的一个接口

4. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法

5. 在调用的时候可以省略 window，前面学习的对话框都属于 window 对象方法，如 alert()、prompt()等。

6. window下的一个特殊属性 window.name

   ```js
   // 定义在全局作用域中的变量会变成window对象的属性
   var num = 10;
   console.log(window.num);
   // 10
   
   // 定义在全局作用域中的函数会变成window对象的方法
   function fn() {
       console.log(11);
   }
   console.fn();
   // 11
   
   var name = 10;  //不要用这个name变量,window下有一个特殊属性window.name
   console.log(window.num);
   ```



## window 对象的常见事件

1. 

------

调节窗口大小事件 ：window.addEventListener('risise',function(){})\window.onresize=function(){}

------

document.readyState属性

> onreadystatechange事件就是专门用于监听document.readyState属性的改变的



### 窗口加载事件

#### load

> window.onload\window.addEventListener("load",function(){})
>
> ​						——等页面内容全部加载完毕，在去执行处理函数

```js
window.onload = function(){
    
};

// 或者
window.addEventListener("load",function(){});
```

注意：

- 有了window.onload就可以把JS代码写到页面元素的上方（因为onload是等页面内容全部加载完毕，再去执行处理函数）
- window.onload 传统注册事件方式，只能写一次（如果有多个，会以最后一个window.onload为准）
- 如果使用addEventListener 则没有限制

#### DOMCountentLoaded

```
document.addEventListener('DOMContentLoaded',function(){})
```

接收两个参数：

- DOMCountentLoaded事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等


- 如果页面的图片很多的话, 从用户访问到onload触发可能需要较长的时间


- 交互效果就不能实现，必然影响用户的体验，此时用 DOMContentLoaded事件比较合适。


#### 区别

- load等页面内容全部加载完毕，包括页面dom元素，图片，flash，css等

- DOMContentLoaded 是DOM加载完毕，不包含图片 flash css 等就可以执行，加载速度比load更快一些

  ```js
  <script>
      // load
      window.onload = function() {
          var btn = document.querySelector('button');
          btn.addEventListener('click', function() {
              alert('点击我');
          })
      }
      window.onload = function() {
          alert(22);
      }
  
  
      window.addEventListener('load', function() {
          var btn = document.querySelector('button');
          btn.addEventListener('click', function() {
              alert('点击我');
          })
      })
      window.addEventListener('load', function() {
          alert(22);
      })
  	//DOMContentLoaded
      document.addEventListener('DOMContentLoaded', function() {
              alert(33);
          })
  </script>
  ```

#### 调整窗口大小事件

> window.onresize 是调整窗口大小加载事件，当触发时就调用的处理函数

```js
window.onresize = function() {}

// 或者
window.addEventListener('resize',function(){});
```

只要窗口大小发生像素变化，就会触发这个事件

> 我们经常利用这个事件完成==响应式布局==。**window.innerWidth 当前屏幕的宽度**

```js
window.addEventListener('load', function() {
    var div = document.querySelector('div');
    window.addEventListener('resize', function() {
        console.log(window.innerWidth);

        console.log('变化了');
        if (window.innerWidth <= 800) {
            div.style.display = 'none';
        } else {
            div.style.display = 'block';
        }

    })
})
```



### 系统对话框

> 详见JavaScript基础输入输出



## 定时器

### setTimeout()定时器

`setTimeout()`方法用于设置一个定时器，该定时器在定时器到期后执行调用函数。

```js
window.setTimeout(调用函数,[延迟的毫秒数]);
```

注意：

1. window可以省略
2. 这个调用函数：可以直接写函数 / 写函数名  /  采取字符串 ‘函数名()’ （不推荐）
3. 延迟的毫秒数省略默认是0，如果写，必须是毫秒
4. 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符
5. setTimeout() 这个调用函数我们也称为回调函数 callback
6. 普通函数是按照代码顺序直接调用，而这个函数，需要等待事件，事件到了才会去调用这个函数，因此称为回调函数。



### clearTimeout()停止定时器

`clearTimeout()`方法取消了先前通过调用 `setTimeout()`建立的定时器

```js
window.clearTimeout(timeoutID)
```

**注意**：

- `window`可以省略
- 里面的参数就是定时器的标识符



### setInterval()定时器

setInterval()方法重复调用一个函数，每隔这个时间，就去调用一次回调函数

```
window.setInterval(回调函数,[间隔的毫秒数]);
```

**注意**：

- window可以省略
- 这个回调函数：可以直接写函数  /  写函数名  /  采取字符 ‘函数名()’
- 第一次执行也是间隔毫秒数之后执行，之后每隔毫秒数就执行一次

### clearInterval()停止定时器

- `clearInterval ( )` 方法取消了先前通过调用 `setInterval()` 建立的定时器

**注意**：

- `window`可以省略
- 里面的参数就是定时器的标识符



### this指向

- 全局作用域或者普通函数中`this`指向全局对象`window`(注意定时器里面的this指向window)
- 方法调用中谁调用`this`指向谁
- 构造函数中`this`指向构造函数实例







## JS执行机制

### JS是单线程

JavaScript 语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。

> 这是因为 JavaScript 是为处理页面中用户的交互，以及操作 DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之后再删除。

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是： 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

### 同步和异步

同步和异步的本质区别：执行顺序不同

> 为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程。于是，JS 中出现了同步和异步。

##### 同步:

> 前一个任务结束后再执行后一个任务

##### 异步：

> 在做这件事的同时，你还可以去处理其他事情

##### 同步任务

> 同步任务都在主线程上执行，形成一个 执行栈

##### 异步任务

> JS中的异步是通过回调函数实现的，异步任务相关回调函数添加到任务队列中

异步任务有以下三种类型：

1. 普通事件，如click,resize等
2. 资源加载，如load,error等
3. 定时器，包括setInterval,setTimeout等

![8](https://i.loli.net/2021/08/03/JpQbHt4kV8yMxsT.png)

js的执行机制=>事件循环

1. 先执行执行栈中的同步任务
2. 异步任务(回调函数)放入任务队列中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

![8](https://i.loli.net/2021/08/03/NlKthy7xHkpLong.png)

> 同步任务放在执行栈中执行，异步任务由异步进程处理放到任务队列中，执行栈中的任务执行完毕会去任务队列中查看是否有异步任务执行，由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为事件循环（ event loop）。



## history对象

> - window 对象给我们提供了一个 history 对象，与浏览器历史记录进行交互
> - 该对象包含用户（在浏览器窗口中）访问过的 URL。

| history对象方法 | 作用                                                         |
| :-------------: | ------------------------------------------------------------ |
|     back()      | 可以后退功能                                                 |
|    forward()    | 前进功能                                                     |
|    go(参数)     | 前进后退功能，参数如果是 1 前进1个页面 如果是 -1 后退1个页面 |

```js
<body>
    <a href="list.html">点击我去往列表页</a>
    <button>前进</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // history.forward();
            history.go(1);
        })
    </script>
</body>
```



## navigator对象

- navigator 对象包含有==关浏览器的信息==，它有很多属性
- 我们常用的是userAgent,该属性可以返回由客户机发送服务器的user-agent头部的值

下面前端代码可以判断用户是用哪个终端打开页面的，如果是用 PC 打开的，我们就跳转到 PC 端的页面，如果是用手机打开的，就跳转到手机端页面

```js
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
 } else {
    window.location.href = "";     //电脑
 }
```



## location对象

> location属性用于获取或设置窗口的UPL，并且用于解析URL，返回的是一个对象。

#### URL

==统一资源定位符（uniform resouce locator）==是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的 URL

URL 的一般语法格式为：

> ```
> protocol://host[:port]/path/[?query]#fragment
> ```
>
> //完整的url：协议://主机号:端口号/路径/？查询字符串#锚点
>
> ```
> http://www.itcast.cn/index.html?name=andy&age=18#link
> ```

|   组成   | 说明                                   |
| :------: | -------------------------------------- |
| protocol | 通信协议 常用的http,ftp,maito等        |
|   host   | 主机(域名) www.itheima.com             |
|   port   | 端口号，可选                           |
|   path   | 路径 由零或多个'/'符号隔开的字符串     |
|  query   | 参数 以键值对的形式，通过&符号分隔开来 |
| fragment | 片段 #后面内容 常见于链接 锚点         |

### location对象属性

|              对象属性               | 返回值                                |
| :---------------------------------: | ------------------------------------- |
|            location.href            | 获取或者设置整个URL                   |
|          location.protcol           | 返回协议                              |
| location.host<br/>location.hostname | 返回主机（域名）www.baidu.com         |
|            location.port            | 返回端口号，如果未写返回空字符串      |
|          location.pathname          | 返回路径                              |
|           location.search           | 返回参数                              |
|            location.hash            | 返回片段，#后面内容，常见于链接、锚点 |

### location对象方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称为重定向页面）                 |
| location.replace() | 替换当前页面，因为不记录历史，所以不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者 f5 ，如果参数为true 强制刷新 ctrl+f5 |





## 创建元素

### 删除元素

> `node.removeChild(child)`——从BOM中删除一个节点，返回删除的节点

阻止链接跳转需要添加 Javascript:void(0); 或者 javascript:;

### 新增元素

#### 动态创建元素节点

1. 创建多个元素：`document.createElement('tagName')`（效率低一点，但是结构更清晰）

2. 创建文本节点：`document.createTextNode()`

   > 1. document.write() 直接将内容写入页面的内容流，但是文档流执行完毕，则会导致页面全部重绘
   > 2. elemter.innerHTML  是将内容写入某个DOM节点，不会导致页面全部重绘，创建多个效率更高(不要拼接字符串，采取数组形式拼接，结构稍微复杂。

#### 添加节点

（需要获取父元素）

1. node.appendChild(child)
   将一个节点添加到指定父节点的子节点列表**末尾**，类似css中after伪元素
2. node.insertBefore(child,指定元素)
   将一个节点添加到指定父节点的子节点列表的**前面**，类似css中before伪元素。

#### 复制节点

`node.cloneNode()`
若括号参数为空或者为false，则是浅拷贝，即只克隆赋值节点本身，不克隆里面的子节点。

### 替换节点

`A.replaceChild(new,old);`：A表示父元素，new表示新子元素，old表示旧子元素。









# DOM

> 通过DOM 接口可以改变网页的内容、结构和样式

**文档对象模型**：把文档当作一个对象来看待

- DOM的顶级对象是document
- DOM主要学习的是操作元素
- DOM是W3C标准规范

![image-20210802154549393](https://i.loli.net/2021/08/02/EXAe6UQMi4OcL9k.png)

- 文档：一个页面就是一个文档，DOM中使用doucument来表示
- 元素：页面中的所有标签都是元素，DOM中使用 element 表示
- 节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示

> DOM 把以上内容都看做是==对象==



## 组成

元素：element

文档：document

节点：node

| 节点类型 | nodeType值 |
| :------- | :--------- |
| 元素节点 | 1          |
| 属性节点 | 2          |
| 文本节点 | 3          |

> 1. 一个元素就是一个节点，这个节点称之为“元素节点”。
> 2. 属性节点和文本节点看起来像是元素节点的一部分，但实际上，它们是独立的节点，并不属于元素节点。
> 3. 只有元素节点才可以拥有子节点，属性节点和文本节点都无法拥有子节点

```js
<div id="wrapper">绿叶学习网</div>
```

### DOM事件流(事件传播)

![img](https://img-blog.csdn.net/20180908210245907?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDEyMjk5Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. 捕获阶段 document->html->body->div
2. 当前目标阶段
3. 冒泡阶段 div->body->html->document

```js
window.onload = function () 
{
    ……
}
```



## 获取元素

### 如何获取页面元素

获取页面中的元素可以使用以下几种方式:

- 根据 ID 获取
- 根据标签名获取
- 通过 HTML5 新增的方法获取
- 特殊元素获取

### 根据ID获取

`document.getElementByID()`——返回为元素对象

```js
console.dir——打印返回的对象，更好的查看属性和方法
```

使用 console.dir() 可以打印我们获取的元素对象，更好的查看对象里面的属性和方法。

🌰：

```js
<div id="time">2019-9-9</div>
<script>
    // 1.因为我们文档页面从上往下加载，所以得先有标签，所以script写在标签下面
    // 2.get 获得 element 元素 by 通过 驼峰命名法
    // 3.参数 id是大小写敏感的字符串
    // 4.返回的是一个元素对象
    var timer = document.getElementById('time');
    console.log(timer);
    // 5. console.dir 打印我们的元素对象，更好的查看里面的属性和方法
    console.dir(timer);
</script>
```



### 根据标签名获取

`document.getElementsByTagName()`——返回元素对象，以伪数组的方式存储，元素对象是动态的

> getElementsByName()只限用于表单元素，它获取的也是一个元素集合，也就是类数组(伪数组)。

因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
得到元素对象是==动态的==

🌰：

```html
<ul>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
</ul>
<script>
    // 1.返回的是获取过来元素对象的集合 以伪数组的形式存储
    var lis = document.getElementsByTagName('li');
    console.log(lis);
    console.log(lis[0]);
    // 2.依次打印,遍历
    for (var i = 0; i < lis.length; i++) {
        console.log(lis[i]);
    }
    // 3.如果页面中只有 1 个 li，返回的还是伪数组的形式
    // 4.如果页面中没有这个元素，返回的是空伪数组
</script>
```

注意：父元素必须是单个对象(必须指明是哪一个元素对象)，获取的时候不包括父元素自己

```js
<script>
	//element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素
    var ol = document.getElementById('ol');
    console.log(ol.getElementsByTagName('li'));
</script>
```



### 根据类名获取（h5 新增）

> document.getElementsByClassName('类名')



### 根据选择器获取（h5 新增）

```js
> document.querySelector('选择器')——根据指定选择器返回第一个对象 
> document.quertSelectorAll()——根据指定选择器返回
```

> PS：document.querySelectorAll(".test")表示获取所有class为test的元素。
>
> 由于获取的是多个元素，因此这也是一个类数组。想要精确得到某一个元素，也需要使用数组下标的形式来获取。



### 通过name属性获取

`document.getElementsByName("name名")`

说明：

> 1. getElementsByName()获取的也是一个类数组，如果想要准确得到某一个元素，可以使用数组下标形式来获取。
> 2. getElementsByName()只用于表单元素，一般只用于单选按钮和复选框。



### 获取特殊元素

①获取body元素——返回body元素对象

```
document.body;
```

②获取html元素——返回html元素对象

> document.documentElement;

③获取title元素——返回 title元素对象

> document.title
>





## 事件基础

### 事件概述

简单理解： 触发— 响应机制。

> 网页中的每个元素都可以产生某些可以触发 JavaScript 的事件，例如，我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作。
>

事件三要素：

1. 事件源(谁)
2. 事件类型(什么事件)
3. 事件处理程序(做啥)

```js
<script>
    // 点击一个按钮，弹出对话框
    // 1. 事件是有三部分组成  事件源  事件类型  事件处理程序   我们也称为事件三要素
    //(1) 事件源 事件被触发的对象   谁  按钮
    var btn = document.getElementById('btn');
    //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
    //(3) 事件处理程序  通过一个函数赋值的方式 完成
    btn.onclick = function() {
        alert('点秋香');
    }
</script>
```

### 执行事件的步骤

1. 获取事件源
2. 注册事件(绑定事件)
3. 添加事件处理程序(采取函数赋值形式)

```js
<script>
    // 执行事件步骤
    // 点击div 控制台输出 我被选中了
    // 1. 获取事件源
    var div = document.querySelector('div');
    // 2.绑定事件 注册事件
    // div.onclick 
    // 3.添加事件处理程序 
    div.onclick = function() {
        console.log('我被选中了');
    }
</script>
```

### 文档的加载

> 浏览器在加载一个页面时，是按照==自上向下的顺序加载==的，加载一行执行一行。
>
> 如果将js代码编写到页面的上边，当代码执行时，页面中的DOM对象还没有加载，此时将会无法正常获取到DOM对象，导致DOM操作失败。

解决方式一：
可以将js代码编写到body的下边

```js
<body>  
		<button id="btn">按钮</button>  
  
		<script>  
			var btn = document.getElementById("btn");  
			btn.onclick = function(){  
		  
			};  
	</script>  
</body>
```

解决方式二：
将js代码编写到`window.onload = function(){}`中

> window.onload 对应的回调函数会在整个页面加载完毕以后才执行，所以可以确保代码执行时，DOM对象已经加载完毕了

```js
<script>  
    window.onload = function(){  
        var btn = document.getElementById("btn");  
        btn.onclick = function(){  
        };  
    };  
</script>
```





## 操作元素

### 获取元素样式

##### element.innerText

> 去除html标签和去掉空格和换行，获取的仅仅是文本内容。
>
> ```js
>  div.innerText = '<strong>今天是：</strong> 2019';
> ```

##### element.innerHTML

> 取的是元素内部所有的内容➡➡➡加上个反斜杠（\）可以换行
>
> ```js
> div.innerHTML = '<strong>今天是：</strong> 2019';
> ```

##### 面试题

三种动态创建元素的区别

- doucument.write()
- element.innerHTML
- document.createElement()

区别：

- document.write() 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
- innerHTML 是将内容写入某个 DOM 节点，不会导致页面全部重绘
- innerHTML 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
- `createElement()`创建多个元素效率稍低一点点，但是结构更清晰

> 总结：不同浏览器下， innerHTML 效率要比 createElement 高



### 改变元素属性

🤝attr：

> - 表单元素的属性操作： type、value、checked、selected、disabled
> - 改变元素内容：src、href、id、alt、title

```
obj.attr= "值";
```

### 改变样式属性

> 我们可以通过 JS 修改元素的大小、颜色、位置等样式。

#### 行内样式操作

```js
obj.style.attr = "值";
```

#### 类名样式操作

```
// element.className
```

#### 常见问题：

**使用style对象来设置样式时，为什么我们不能使用background-color这种写法，而必须使用backgroundColor”这种骆驼峰型写法呢？**

> 大家别忘了，在obj.style.backgroundColor中，backgroundColor其实也是一个变量，变量中是不允许出现中划线的，因为中划线在JavaScript中是减号的意思。

注意：

1. JS里面的样式采取==驼峰命名法==，比如 fontSize ，backgroundColor

2. JS 修改 style 样式操作 ，产生的是行内样式，==CSS权重比较高==

3. 如果样式修改较多，可以==采取操作类名方式==更改元素样式

4. class 因为是个保留字，因此使用className来操作元素类名属性

5. className 会直接更改元素的类名，会覆盖原先的类名

   ```JS
   <body>
          <div class="first">文本</div>
          <script>
              // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
              var test = document.querySelector('div');
              test.onclick = function() {
                  // this.style.backgroundColor = 'purple';
                  // this.style.color = '#fff';
                  // this.style.fontSize = '25px';
                  // this.style.marginTop = '100px';
                  // 让我们当前元素的类名改为了 change
   
               // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况
               // 3. 如果想要保留原先的类名，我们可以这么做 多类名选择器
               // this.className = 'change';
               this.className = 'first change';
           }
       </script>
   
   </body>
   ```



#### 读取元素的当前样式

##### getComputedStyle()（一般浏览器）

> 这个方法是window对象的方法，可以返回一个对象，这个对象中保存着当前元素生效样式
> 参数：

1. 要获取样式的元素

2. 可以传递一个伪元素，一般传null

   ```js
   //获取元素的宽度
   getComputedStyle(box , null)[“width”];
   //通过该方法读取到样式都是只读的不能修改
   ```

##### currentStyle（IE8）

> 语法：元素.currentStyle.样式名

```js
box.currentStyle[“width”]
//通过这个属性读取到的样式是只读的不能修改
```




##### 实现兼容性

```js
/*  
* 定义一个函数，用来获取指定元素的当前的样式  
* 参数：  
* 		obj 要获取样式的元素  
* 		name 要获取的样式名  
*/  
function getStyle(obj , name){  
//对象.属性不存在，不会报错，如果直接寻找对象，（当前作用域到全局作用域）找不到会报错  
    if(window.getComputedStyle){  
        //正常浏览器的方式，具有getComputedStyle()方法  
        return getComputedStyle(obj , null)[name];  
    }else{  
        //IE8的方式，没有getComputedStyle()方法  
        return obj.currentStyle[name];  
    }  
    //return window.getComputedStyle?getComputedStyle(obj , null)[name]:obj.currentStyle[name];			  
}
```



#### 排他思想

如果有同一组元素，我们相要某一个元素实现某种样式，需要用到循环的排他思想算法：

1. 所有元素全部清除样式（干掉其他人）

2. 给当前元素设置样式 （留下我自己）

3. 注意顺序不能颠倒，首先干掉其他人，再设置自己

   ```js
   <body>
          <button>按钮1</button>
          <button>按钮2</button>
          <button>按钮3</button>
          <button>按钮4</button>
          <button>按钮5</button>
   
          <script>
              // 1. 获取所有按钮元素
              var btns = document.getElementsByTagName('button');
              // btns得到的是伪数组  里面的每一个元素 btns[i]
              for (var i = 0; i < btns.length; i++) {
                  btns[i].onclick = function() {
                      // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
                      for (var i = 0; i < btns.length; i++) {
                          btns[i].style.backgroundColor = '';
                      }
                      // (2) 然后才让当前的元素背景颜色为pink 留下我自己
                      this.style.backgroundColor = 'pink';
   
               }
           }
           //2. 首先先排除其他人，然后才设置自己的样式 这种排除其他人的思想我们成为排他思想
       </script>
   
   </body>
   ```







### 自定义属性

#### getAttribute()

👉 等值于 obj.attr（⚠️自定义属性无法实现）

> 获取元素的某个属性的值：obj.getAttribute("attr")

#### setAttribute()

👉 等值于 obj.attr = "值";（⚠️自定义属性值的设置无法实现）

> 设置元素的某个属性的值

#### removeAttribute()

> 删除元素的某个属性：obj.removeAttribute("attr")

#### hasAttribute()

> 判断元素是否含有某个属性：obj.hasAttribute("attr")
>
> 👉返回一个布尔值，如果包含该属性，则返回true

🌰：

```js
<body>
    <div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        // (1) element.属性
        console.log(div.id);
        //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思 我们程序员自己添加的属性我们称为自定义属性 index
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
        // 2. 设置元素属性值
        // (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是class 不是className
        // 3 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
    </script>

</body>
```



### H5自定义属性

自定义属性目的：

- 保存并保存数据，有些数据可以保存到页面中而不用保存到数据库中
- 有些自定义属性很容易引起歧义，不容易判断到底是内置属性还是自定义的，所以H5有了规定

#### 设置H5自定义属性

H5规定自定义属性 `data-`开头作为属性名并赋值

```js
<div data-index = "1"></>
// 或者使用JavaScript设置
div.setAttribute('data-index',1);
```

#### 获取H5自定义属性

1. 兼容性获取 element.getAttribute('data-index')
2. H5新增的：element.dataset.index 或element.dataset['index'] IE11才开始支持

🌰：

```js
<body>
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
</body>
```



## DOM节点

### 父级节点

 node.parentNode——离元素最近的父节点

### 子节点

- parentNode.childNodes——包括元素节点和文本节点等等

- ⭐parentNode.children(非标准)——实际开发常用的

- parentNode.firstChild——第一个子节点，不管是文本节点还是元素节点

- parentNode.lastChild——最后一个子节点，不管是文本节点还是元素节点

  > 解决办法有两个：
  >
  > （1）将li元素间的“换行空格”去掉。
  >
  > （2）使用nodeType来判断：我们都知道，元素节点的nodeType属性值为1，文本节点的nodeType属性值为3。然后使用if判断，如果oUl.lastChild.nodeType值为3，则执行removeChild()两次，第1次删除“空白节点”，第2次删除元素。如果oUl.lastChild.nodeType值不为3，则只执行removeChild()一次。
  >
  > ```js
  > if (oUl.lastChild.nodeType == 3) {           
  >     oUl.removeChild(oUl.lastChild);           
  >     oUl.removeChild(oUl.lastChild);       
  > } else {           
  >     oUl.removeChild(oUl.lastChild);       
  > }
  > ```

- ⭐parent.firstElementChild——第一个字元素节点，ie9才支持

- ⭐parent.lastElementChild

  > 实际开发中一般用parent.children[0]代表第一个子元素节点，parent.children[parent.children-1]代表最后一个子元素节点。

### 兄弟节点

- node.nextSibling ：返回当前元素的下一个兄弟节点，找不到则返回null

- node.previousSiblng ：返回当前元素的上一个兄弟节点，找不到则返回null

- ⭐node.nextElementSibling 

  > 放回当前元素的下一个元素兄弟节点，找不到则返回null，ie9才支持

- ⭐node.previousElementSibling 

  > 返回当前元素的上一个元素兄弟节点，找不到则返回null，ie9才支持

```js
//解决兄弟元素节点兼容性的办法function getNextElementSibling(elmenet){    var el =element;    while (el = el.nextSibling) {        if (el.nodeType === 1) {            return el;        }    }    return null;}
```



## DOM核心

对于DOM操作，我们主要针对子元素的操作，主要有

- 创建
- 增
- 删
- 改
- 查

- 属性操作
- 时间操作

### 创建

1. document.write
2. innerHTML
3. createElement

### 增

1. appendChild
2. insertBefore

### 删

1. removeChild

### 改

> 主要修改dom的元素属性，dom元素的内容、属性、表单的值等

1. 修改元素属性：src、href、title 等
2. 修改普通元素内容：innerHTML、innerText
3. 修改表单元素：value、type、disabled
4. 修改元素样式：style、className

### 查

> 主要获取查询dom的元素

1. DOM提供的API方法：getElementById、getElementsByTagName (古老用法，不推荐)
2. H5提供的新方法：querySelector、querySelectorAll (提倡)
3. 利用节点操作获取元素：父(parentNode)、子(children)、兄(previousElementSibling、nextElementSibling) 提倡

### 属性操作

> 主要针对于自定义属性

1. setAttribute：设置dom的属性值
2. getAttribute：得到dom的属性值
3. removeAttribute：移除属性









# 事件(event)

## 事件对象

（形参）：只有有了事件才会存在，由系统自动创建，不需要传递参数

> 可以在响应函数中定义一个形参，来使用事件对象，

但是在IE8以下浏览器中事件对象是作为window对象的属性保存

- 官方解释：event 对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态
- 简单理解：
  - 事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面
  - 这个对象就是事件对象 event，它有很多属性和方法，比如“
    1. 谁绑定了这个事件
    2. 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置
    3. 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键

- 这个 event 是个形参，系统帮我们设定为事件对象，不需要传递实参过去
- 当我们注册事件时， event 对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）

```js
元素.事件 = function(event){  
    event = event || window.event;  
};  
  
元素.事件 = function(e){  
	e = e || event;  
	  
};
```

> ie678通过： `window.event `
>
> 兼容性写法：`e = e ：|| window.event`

## 注册事件(绑定事件)

> 给元素添加事件，称为注册事件或者绑定事件。

注册事件有两种方式：

1. 传统方式
2. 方法监听注册方式

|                         传统注册方式                         |                   方法监听注册方式                    |
| :----------------------------------------------------------: | :---------------------------------------------------: |
|                  利用 on 开头的事件 onclick                  |                   w3c 标准推荐方式                    |
|          <button onclick = "alert("hi")"></button>           |            addEventListener() 它是一个方法            |
|                 btn.onclick = function() {}                  | IE9 之前的 IE 不支持此方法，可使用 attachEvent() 代替 |
|                    特点：注册事件的唯一性                    |     特点：同一个元素同一个事件可以注册多个监听器      |
| 同一个元素同一个事件只能设置一个处理函数;最后注册的处理函数将会覆盖前面注册的处理函数 |                  按注册顺序依次执行                   |

### addEventListener()

- `eventTarget.addEventListener()`方法将指定的监听器注册到 eventTarget（目标对象）上

  > 当该对象触发指定的事件时，就会执行事件处理函数

```js
eventTarget.addEventListener(type,listener[,useCapture])
```

该方法接收三个参数：

1. type:事件类型字符串，比如click,mouseover,注意这里不要带on
2. listener：事件处理函数，事件发生时，会调用该监听函数
3. useCapture：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习

```js
<body>
    <button>传统注册事件</button>
    <button>方法监听注册事件</button>
    <button>ie9 attachEvent</button>
    <script>
        var btns = document.querySelectorAll('button');
        // 1. 传统方式注册事件
        btns[0].onclick = function() {
            alert('hi');
        }
        btns[0].onclick = function() {
            alert('hao a u');
        }
            // 2. 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click', function() {
            alert(22);
        })
        btns[1].addEventListener('click', function() {
            alert(33);
        })
            // 3. attachEvent ie9以前的版本支持
        btns[2].attachEvent('onclick', function() {
            alert(11);
        })
    </script>
</body>

```




### attachEvent()

- 兼容：在IE8中可以使用attachEvent()来绑定事件

- 当该对象触发指定的事件时，指定的回调函数就会被执行
- 可以绑定多个监听事件，不同的是它是后绑定先执行，执行顺序和addEventListener()相反

```js
eventTarget.attachEvent(eventNameWithOn,callback)
```

该方法接收两个参数：

- `eventNameWithOn`：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
- `callback`： 事件处理函数，当目标触发事件时回调函数被调用
- ie9以前的版本支持



### 注册事件兼容性解决方案

> 兼容性处理的原则：首先照顾大多数浏览器，再处理特殊浏览器

```js
//定义一个函数，用来为指定元素绑定响应函数  
/*  
 * 	addEventListener()中的this，是绑定事件的对象  
 * 	attachEvent()中的this，是window  
 *  需要统一两个方法this : 利用call()
 */  
/*  
 * 参数：  
 * 	obj 要绑定事件的对象  
 * 	eventStr 事件的字符串(不要on)  
 *  callback 回调函数  
 */  
function bind(obj , eventStr , callback){  
    // 判断浏览器是否支持
    if(obj.addEventListener){  
        //大部分浏览器兼容的方式  
        obj.addEventListener(eventStr , callback , false);  
    }else if{  
        //IE8及以下  
        obj.attachEvent("on"+eventStr , function(){  
            //在匿名函数中调用回调函数  
            callback.call(obj);  
        });  
    } else {
        //相当于 element.onclick = fn;
        elemenet['on' + eventName] = fn;
    } 
}
```



## 事件委托

> 事件委托也称为事件代理，在 jQuery 里面称为事件委派

- 事件委托的原理：事件监听器设置在**其父节点**，然后利用**冒泡原理**影响设置在子节点 。通过委派可以减少事件绑定的次数，提高程序的性能

### 传统注册方式

> 利用on开头的事件onclick（特点：注册事件的唯一i性）

事件三部分组成：

1. 事件源（事件被触发的对象）
2. 事件类型（注册事件/绑定事件）
3. 事件处理程序（函数赋值的方式）

### 方法监听注册方式

- addEventListener()是一个方法
- attachEvent()

### 案例

```js
//给 ul 注册点击事件，然后利用事件对象的 target 来找到当前点击的 li，因为点击 li，事件会冒泡到 ul 上， ul 有注册事件，就会触发事件监听器。
<body>
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
            // 点了谁，就让谁的style里面的backgroundColor颜色变为pink
        })
    </script>
</body>
```



## 删除事件(解绑事件)

#### removeEventListener删除事件方式

```js
eventTarget.removeEventListener(type,listener[,useCapture]);
```

该方法接收三个参数：

- type:事件类型字符串，比如click,mouseover,注意这里不要带on
- listener：事件处理函数，事件发生时，会调用该监听函数
- useCapture：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习

#### detachEvent删除事件方式(兼容)

```
eventTarget.detachEvent(eventNameWithOn,callback);
```

该方法接收两个参数：

- eventNameWithOn：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
- callback： 事件处理函数，当目标触发事件时回调函数被调用
- ie9以前的版本支持

#### 传统事件删除方式

```js
eventTarget.onclick = null;
```

事件删除示例：

```js
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
            alert(11);
            // 1. 传统方式删除事件
            divs[0].onclick = null;
        }
        // 2.removeEventListener 删除事件
        divs[1].addEventListener('click',fn);   //里面的fn不需要调用加小括号

        function fn(){
            alert(22);
            divs[1].removeEventListener('click',fn);
        }
        // 3.IE9 中的删除事件方式
        divs[2].attachEvent('onclick',fn1);
        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick',fn1);
        }
    </script>
</body>
```

#### 删除事件兼容性解决方案

```js
 function removeEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 removeEventListener 方法
      if (element.removeEventListener) {
        element.removeEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.detachEvent) {
        element.detachEvent('on' + eventName, fn);
      } else {
        element['on' + eventName] = null;
 } 
```





## DOM事件流

> 事件流描述的是==从页面中接收事件的顺序==
> 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

![2](https://i.loli.net/2021/08/03/NCx8ZrUlHgfipOq.png)

事件冒泡： IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点的过程。

事件捕获： 网景最早提出，由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。

**加深理解**：

我们向水里面扔一块石头，首先它会有一个下降的过程，这个过程就可以理解为从最顶层向事件发生的最具体元素（目标点）的捕获过程；之后会产生泡泡，会在最低点（ 最具体元素）之后漂浮到水面上，这个过程相当于事件冒泡。

### 捕获阶段

> document -> html -> body -> father -> son

两个盒子嵌套，一个父盒子一个子盒子，我们的需求是当点击父盒子时弹出 father ，当点击子盒子时弹出 son

```js
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // dom 事件流 三个阶段
        // 1. JS 代码中只能执行捕获或者冒泡其中的一个阶段。
        // 2. onclick 和 attachEvent（ie） 只能得到冒泡阶段。
        // 3. 捕获阶段 如果addEventListener 第三个参数是 true 那么则处于捕获阶段  document -> html -> body -> father -> son
        var son = document.querySelector('.son');
        son.addEventListener('click', function() {
             alert('son');
        }, true);
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, true);
    </script>
</body>
```

> 但是因为DOM流的影响，我们点击子盒子，会先弹出 father，之后再弹出 son

这是因为捕获阶段由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收

document -> html -> body -> father -> son

先看 document 的事件，没有；再看 html 的事件，没有；再看 body 的事件，没有；再看 father 的事件，有就先执行；再看 son 的事件，再执行。



### 冒泡阶段

事件的冒泡指的是事件向上传导，当后代元素上的事件被触发时，将会导致其祖先元素上的同类事件也会触发

```js
<body>

    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
		// 4. 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 那么则处于冒泡阶段  son -> father ->body -> html -> document
        var son = document.querySelector('.son');
        son.addEventListener('click', function() {
            alert('son');
        }, false);
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
</body>
```

我们点击子盒子，会弹出 son、father、document

这是因为冒泡阶段开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点

> son -> father ->body -> html -> document



## 事件对象阻止默认行为

```js
<body>
    <div>123</div>
    <a href="http://www.baidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
                e.preventDefault(); //  dom 标准写法
            })
            // 3. 传统的注册方式
        a.onclick = function(e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);
        }
    </script>
</body>

```

## 阻止事件冒泡

事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点

事件冒泡本身的特性，会带来的坏处，也会带来的好处，需要我们灵活掌握。

- 标准写法

  ```
  e.stopPropagation();
  ```

- 非标准写法： IE6-8 利用对象事件 cancelBubble属性

  ```
  e.cancelBubble = true;
  ```

```js
<body>
    <div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        // 常见事件对象的属性和方法
        // 阻止冒泡  dom 推荐的标准 stopPropagation() 
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
</body>
```

### 阻止事件冒泡的兼容性解决方案

```js
if(e && e.stopPropagation){
      e.stopPropagation();
  }else{
      window.event.cancelBubble = true;
  }
```

### e.target 与 this

> e.target 与 this 的区别

- `this`是事件绑定的元素，这个函数的调用者(绑定这个事件的元素)，返回的是绑定事件的对象（元素）
- `e.target`返回的是触发事件的对象（元素）

```js
<body>
    <div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            console.log(e.target);
            console.log(this);

        })
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
                // 我们给ul 绑定了事件  那么this 就指向ul  
                console.log(this);
                console.log(e.currentTarget);
            
            // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
                console.log(e.target);
            })

            // 了解兼容性
            // div.onclick = function(e) {
            //     e = e || window.event;
            //     var target = e.target || e.srcElement;
            //     console.log(target);

        // }
        // 2. 了解 跟 this 有个非常相似的属性 currentTarget  ie678不认识
    </script>
</body>

```

### 事件对象的兼容性

事件对象本身的获取存在兼容问题：

- 标准浏览器中浏览器是给方法传递的参数，只需定义形参e就可以获取到
- 在 IE6 -> 8 中，浏览器不会给方法传递参数，如果需要的话，需要到window.event中获取查找

```js
解决方案：e = e || window.event
```

```js
<body>
    <div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        div.onclick = function(e) {
                // e = e || window.event;
                console.log(e);
				// 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;

            }
</body>

```





## 常见的鼠标事件

### 表单事件

| 事件     | 说明                                               |
| :------- | :------------------------------------------------- |
| onfocus  | 获得鼠标焦点触发                                   |
| onblur   | 失去鼠标焦点触发                                   |
| onselect | 选中“单行文本框”或“多行文本框”中的内容时，就会触发 |

> focus()跟onfocus是不一样的。focus()是一个方法，仅仅用于让元素获取焦点。而onfocus是一个属性，它是用于事件操作的。

具有“获取焦点”和“失去焦点”特点的元素只有2种。

- （1）表单元素（单选框、复选框、单行文本框、多行文本框、下拉列表）
- （2）超链接

**onchange**

> 常用于“具有多个选项的表单元素”。

- （1）单选框选择某一项时触发。
- （2）复选框选择某一项时触发。
- （3）下拉列表选择某一项时触发。



|  鼠标事件   |     触发条件     |
| :---------: | :--------------: |
|   onclick   | 鼠标点击左键触发 |
| onmouseover |   鼠标经过触发   |
| onmouseout  |   鼠标离开触发   |
|   onfocus   | 获得鼠标焦点触发 |
|   onblur    | 失去鼠标焦点触发 |
| onmousemove |   鼠标移动触发   |
|  onmouseup  |   鼠标弹起触发   |
| onmousedown |   鼠标按下触发   |

### 禁止鼠标右键与鼠标选中

- `contextmenu`主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单
- `selectstart` 禁止鼠标选中

```js
<body>
    <h1>我是一段不愿意分享的文字</h1>
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function(e) {
                e.preventDefault(); // 阻止默认行为
            })
            // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function(e) {
            e.preventDefault();

        })
    </script>
</body>
```

### 鼠标事件对象

event对象代表事件的状态，跟事件相关的一系列信息的集合

现阶段我们主要是用鼠标事件对象 MouseEvent 和键盘事件对象 KeyboardEvent。

|  鼠标事件对象   |                  说明                   |
| :-------------: | :-------------------------------------: |
|    e.clientX    |  返回鼠标相对于浏览器窗口可视区的X坐标  |
|    e.clientY    |  返回鼠标相对于浏览器窗口可视区的Y坐标  |
| e.pageX（重点） | 返回鼠标相对于文档页面的X坐标 IE9+ 支持 |
| e.pageY（重点） | 返回鼠标相对于文档页面的Y坐标 IE9+ 支持 |
|    e.screenX    |      返回鼠标相对于电脑屏幕的X坐标      |
|    e.screenY    |      返回鼠标相对于电脑屏幕的Y坐标      |




## 常用的键盘事件

键盘事件一般有两个用途：表单操作和动画控制。

> 键盘事件一般都会绑定给一些可以获取到焦点的对象或者是document

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发(对于onkeydown来说如果一直按着某个按键不松手，则事件会一直触发)——当onkeydown连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常的快，这种设计是为了防止误操作的发生。 |
| onkeypress | 某个键盘按键被按下时触发，但是它不识别功能键，比如 ctrl shift 箭头... |

- **如果使用addEventListener 不需要加 on**
- `onkeypress` 和前面2个的区别是，它不识别功能键，比如左右箭头，shift 等
- 三个事件的执行顺序是： keydown – keypress — keyup

```js
// 常用的键盘事件
//1. keyup 按键弹起的时候触发 
// document.onkeyup = function() {
//         console.log('我弹起了');

//     }
document.addEventListener('keyup', function() {
    console.log('我弹起了');
})

//3. keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
document.addEventListener('keypress', function() {
        console.log('我按下了press');
    })
    //2. keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
document.addEventListener('keydown', function() {
        console.log('我按下了down');
    })
    // 4. 三个事件的执行顺序  keydown -- keypress -- keyup
```



### 键盘对象属性

| 键盘事件对象 **属性** | 说明                    |
| --------------------- | ----------------------- |
| keyCode               | 返回该**键**值的ASCII值 |

- `onkeydown`和 `onkeyup` 不区分字母大小写，`onkeypress` 区分字母大小写。
- 在我们实际开发中，我们更多的使用keydown和keyup， 它能识别所有的键（包括功能键）
- `Keypress` 不识别功能键，但是`keyCode`属性能区分大小写，返回不同的ASCII值

事件对象中还提供了几个属性（这个三个用来判断alt ctrl 和 shift是否被按下，如果按下则返回true，否则返回false）

1. altKey
2. ctrlKey
3. shiftKey


案例

```js
//console.log(event.keyCode);  
  
//判断一个y是否被按下  
//判断y和ctrl是否同时被按下  
if(event.keyCode === 89 && event.ctrlKey){  
	console.log("ctrl和y都被按下了");  
}
```

```js
input.onkeydown = function(event) {  
    event = event || window.event;  
    //数字 48 - 57  
    //使文本框中不能输入数字  
    if(event.keyCode >= 48 && event.keyCode <= 57) {  
        //在文本框中输入内容，属于onkeydown的默认行为  
        //如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中  
        return false;  
    }  
};
```



## 编辑事件

#### oncopy

> 防止页面内容被复制

#### onselectstart

> 防止页面内容被选取。

#### oncontextmenu

> 禁止鼠标右键



## 页面事件

#### onload

> 表示文档加载完成后再执行的一个事件

#### onbeforeunload

> 表示离开页面之前触发的一个事件



