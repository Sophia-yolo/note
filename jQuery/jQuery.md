## [jQuery 文档](https://jquery.cuishifeng.cn/)



## jQuery的优势

- **轻量级**。核心文件才几十kb，不会影响页面加载速度
- ==强大的选择器==。允许使用几乎所有选择器以及jQuery独创的高级而复杂的选择器
- 出色的==DOM操作==的封装。
- 可靠的**事件处理机制**。
- 完善的Ajax。
- ==不污染顶级变量==。
- ==跨浏览器兼容==。基本兼容了现在主流的浏览器
- 链式编程/隐式迭代
- 对事件、样式、动画支持，大大简化了DOM操作
- 行为层与结构层分离。开发者可以使用jQuery选择器选中元素，然后直接给元素添加事件。
- 支持插件扩展开发。有着==丰富的第三方的插件==，例如：树形菜单、日期控件、轮播图等。





## 认识jQuery

[jQuery下载](http://code.jquery.com/)

### 本质

>  本质是闭包——立即执行函数

 

### 原生 JavaScript-jQuery的区别

![在这里插入图片描述](https://i.loli.net/2021/08/15/vp2O3UzSfXnsqFR.png)

1. 原生JavaScript 和 jQuery 入口函数的加载模式不同
   - 原生 JavaScript 会等到DOM元素加载完毕，并且图片也加载完毕才会执行
   - jQuery 会等到DOM元素加载完毕，但==不会等到图片也加载完毕就会执行==

2. 原生 JavaScript 在多个入口函数下，后面编写的会覆盖前面编写的，而 jQuery 不会

   > jQuery框架本质是一个闭包,每次执行我们都会给ready函数传递一个新的函数,不同函数内部的数据不会相互干扰
   >
   > > - 多个window.onload只会执行一次, 后面的会覆盖前面的
   > > - 多个$(document).ready()会执行多次,后面的不会覆盖前面的

3. jQuery 中编写多个入口函数，会以此执行。



### jQuery的入口函数

```js
 		// 1.第一种写法
        $(document).ready(function () {
            ...  //此处是页面DOM加载完成入口
        });

        // 2.第二种写法
        jQuery(document).ready(function () {
           ...  //此处是页面DOM加载完成入口
        });

        // 3.第三种写法(推荐)
        $(function () {
            ...  //此处是页面DOM加载完成入口
        });

        // 4.第四种写法
        jQuery(function () {
            ...  //此处是页面DOM加载完成入口
        });
```

1. jQuery的顶级函数`$`(是jQuery的别称)
2. jQuery对象只能使用jQuery方法，DOM对象则使用原生JavaScript的属性和方法
3. jQuery对象和DOM对象相互转换：
   1. $('DOM对象')
   2. ==$('DOM对象')[0]==/$​('DOM对象')get(0)
   3. 获取的是jQuery对象，则在变量前面加上$

### 解决jQuery 与其他库的冲突

1. jQuery库在其他库之后导入

```js
//释放$的使用权
jQuery.noConflict();	//释放之后就不能使用$，改为使用jQuery

//自定义一个访问符号
var nj = jQuery.noConflict();
nj(function(){
	~
})
```

2. jQuery库在其他库之前导入

> $改为使用jQuery



### jQuery核心函数

| 核心函数 | 描述                     |
| -------- | ------------------------ |
| $()      | 代表调用jQuery的核心函数 |



### jQuery 对象

```js
    var $div = $("div");
    console.log($div);

    var arr = [1, 3, 5];
    console.log(arr);
```

![image-20210815181425126](https://i.loli.net/2021/08/15/BhWYJiSDbFsTHLo.png)

> jQuery 对象是一个伪数组
>
> - 有 0-length-1 的属性
> - 并且有 length 属性

#### jQuery拷贝对象

```
 $.extend([deep], target, object1, [objectN])
```

> 1. deep:如果设为true为深拷贝，默认为false浅拷贝
> 2. target:要拷贝的目标对象
> 3. object1:待拷贝到第一个对象的对象
> 4. objectN:待拷贝到第N个对象的对象
> 5. 浅拷贝是把被拷贝的对象复杂数据类型中的地址拷贝到目标对象修改目标对象会影响被拷贝对象
> 6. 深拷贝，前面加true，完全克隆（拷贝的对象，而不是地址），修改目标对象不会影响被拷贝对象。





### jQuery静态方法

```js
// 1.定义一个类
function AClass() {
}

// 2.给这个类添加一个静态方法
AClass.staticMethod = function () {
    alert("staticMethod");
}

// 静态方法通过类名调用
AClass.staticMethod();

// 3.给这个类添加一个实例方法
AClass.prototype.instanceMethod = function () {
    alert("instanceMethod");
}
// 实例方法通过类的实例调用
// 创建一个实例(创建一个对象)
var a = new AClass();

// 通过实例调用实例方法
a.instanceMethod();
```

| 静态方法        | 描述                                             |
| --------------- | ------------------------------------------------ |
| each()          | 遍历数组                                         |
| map()           | 遍历数组                                         |
| trim()          | 去除字符串两端的空格，不影响字符串               |
| isWindow()      | 判断传入的是不是window对象，*返回值: true/false* |
| isArray()       | 判断是不是数组，*返回值: true/false*             |
| isFunction()    | 判断是否为函数                                   |
| holdReady(true) | 暂停入口函数的执行                               |

#### foreach — each

```js
var arr = [1, 3, 5, 7, 9];
var obj = {0:1, 1:3, 2:5, 3:7, 4:9, length:5};
```

1. foreach

   > 原生的 *forEach* 方法只能遍历数组, 不能遍历伪数组
   >
   > -  第一个参数: 遍历到的元素        
   > - *第二个参数: 当前遍历到的索引*
   >
   > ```js
   > arr.forEach(function (value, index) {
   >      console.log(index, value);
   >  });
   > ```

2. each

   > 注意点: 	jQuery的each方法是可以遍历伪数组的
   >
   > - *第一个参数: 当前遍历到的索引*        
   > - *第二个参数: 遍历到的元素*        
   >
   > ```js
   > $.each(arr, function (index, value) {
   >      console.log(index, value);
   >  });
   > $.each(obj, function (index, value) {
   >     console.log(index, value);
   > });
   > ```



#### map()

1. 第一个参数: 当前遍历到的元素        
2. 第二个参数: 当前遍历到的索引        
3. 第三个参数: 当前被遍历的数组

> 注意点：*和原生的forEach一样,不能遍历的伪数组*

```js
// 上一个例子
arr.map(function (value, index, array) {
    console.log(index, value, array);
 });
```



 **jQuery中的each静态方法和map静态方法的区别**:

1. each静态方法默认的返回值就是, ==遍历谁就返回谁==
   map静态方法默认的返回值是一个==空数组==
2. each静态方法==不支持==在回调函数中对遍历的数组进行处理
   map静态方法可以在回调函数中通过return对遍历的数组进行处理, 然后生成一个新的数组返回



## jQuery选择器

### 基本选择器

![image-20210815184103245](https://i.loli.net/2021/08/15/au7jch1DGzWYEKV.png)

### 层级选择器

![在这里插入图片描述](https://i.loli.net/2021/08/15/Z175gdStq69TUye.png)

### 过滤选择器

#### 基本筛选器过滤

![在这里插入图片描述](https://i.loli.net/2021/08/15/gNwICFQLVqSzZUP.png)



#### 内容过滤

![在这里插入图片描述](https://i.loli.net/2021/08/15/iMnmwt5lTqWB6gv.png)



#### 可见性过滤 

| 可见性过滤选择器 | 功能                                                         |  放回值  |
| :--------------: | :----------------------------------------------------------- | :------: |
|     :hidden      | 获取所有的不可见元素<br>css 属性：display: none; 或 visibility: hidden;<br>input 元素属性：type=hidden; | 元素集合 |
|     :visible     | 获取所有可见元素                                             | 元素集合 |



#### 属性过滤

![在这里插入图片描述](https://i.loli.net/2021/08/15/iZhgDRJLcEktxav.png)

#### 子元素过滤



### 表单选择器

![在这里插入图片描述](https://i.loli.net/2021/08/15/TVafEuUbrcJ3S1e.png)

#### 表单对象属性过滤选择器

![在这里插入图片描述](https://i.loli.net/2021/08/15/FLQAZrvR2nsaidw.png)

> `$("选择器")`

- 并集选择器——$("div,p,li")
- 交集选择器——$("li.current")



### jQuery筛选方法（重点）

- parent()——查找父级
- parents()——查找祖先
- children(selector)——最近一级（亲儿子）
- find(selector)——相当于后代选择器
- siblings(selector)——查找兄弟节点，不包括自己本身
- nextALl([expr ])——查找当前元素之后的所有同辈元素
- prevtAll([expr ])——查找当前元素之前的所有同辈元素
- hasClass(class)——检查当前的元素是否含有某个特定的，如果有，则返回true
- eq(index)——index从0开始



## jQuery中的DOM操作

> 任何对象都有属性，但是只有在DOM元素才有属性节点

### Jquery的文档处理

#### 内部插入

*会将元素添加到指定元素内部的最后*：

- append(content|fn)
- appendTo(content)

*会将元素添加到指定元素内部的最前面* ：

- prepend(content|fn)
- prependTo(content)

#### 外部插入

*会将元素添加到指定元素外部的后面【紧跟其后】*

- after(content|fn)
- insertAfter(content)

*会将元素添加到指定元素外部的前面【紧跟其前】*

- before(content|fn)
- insertBefore(content)

#### 删除

- empty()

  > 删除指定元素的内容和子元素, 指定元素自身不会被删除

- remove([expr\])——*删除指定元素*

- detach([expr\])——*作用和remove一样*

#### 替换节点[⭐]

> 替换所有匹配的元素为指定的元素            两者作用一样，知识调用的顺序不一样

- replaceWith(content|fn)            
- replaceAll(selector)            

#### 复制节点[⭐]

clone([Even[,deepEven\]])

浅复制clone(false)

> 仅复制节点，不会复制元素的事件   

深复制clone(true)

> 不仅复制节点元素，且复制事件





### 属性操作

#### 属性

官方推荐在操作属性节点时，具有true 和 false 两个属性的属性节点，如checked，selected，disabled 使用 prop()，其他使用 attr()

##### prop()

- prop方法， 特点和 `attr` 方法一致

- removeProp 方法，特点和removeAttr方法一致

> *不仅能够操作属性, 他还能操作属性节点*
>
> - prop("属性")——获取元素固有属性值
> - prop("属性","属性值")——设置元素（不仅可以操作属性值，还可以操作属性节点）



##### attr()

> removeAttr(name)：删除所有找到元素指定的属性节点

注意点:            

- 如果是获取:无论找到多少个元素, 都只会返回第一个元素指定的属性节点的值           
-  如果是设置:找到多少个元素就会设置多少个元素。若设置的属性节点不存在, 那么系统会自动新增

> `attr(name|pro|key,val|fn)`
>
> 作用：获取或者设置属性节点的值
>
> 1. 如果传递一个参数——属性，代表获取属性节点的值（都只会返回第一个元素指定的属性节点的值）
> 2. 如果传递两个参数，代表设置属性节点的值（若没有，则创建一个）



##### date()

> - date()——数据缓存，存放在元素内存中
> - date("name","value")——向被选元素附加数据
> - date("name")——向被选元素获取数据



##### Attribute()

> - setAttribute("name","value")——设置属性节点
> - getAttribute("name")——获取属性名称



#### css 样式操作

##### attr()

> 获取样式和设置样式

##### addClass()

> 追加样式

##### removeClass()

> 移除样式——*如果想删除多个, 多个类名之间用空格隔开即可*

##### 切换样式

> 1. toggle（）
> 2. toggleClass（）

##### hasClass()	

> toFixed(位数)——保留小数位

🌺原生 JavaScript 中 className会覆盖元素原先里面的类名。jQuery里面类操作只是对指定类进行操作，不影响原先类名。

排他思想=>注意隐式迭代

> 隐式迭代：遍历所有DOM元素（伪数组形式存储）的过程
>



##### jQuery文本值相关的方法

###### innerHTML

> 设置或获取标签所包含的HTML+文本信息(从标签起始位置到终止位置全部内容，包括HTML标签，但不包括自身)

###### html()

> 普通元素内容html()——相当于原生innerHTML
>
> - html()——获取元素内容
> - html("内容")——设置元素内容

###### innerText

> 设置或获取标签所包含的文本信息（从标签起始位置到终止位置的内容，去除HTML标签，但不包括自身）

###### text()

> 普通元素文本内容text()——相当于原生innerText
>
> - text()——获取元素的文本内容
> - text("文本内容")——设置元素的文本内容

###### val()

> 表单的值val()——相当于原生value
>
> - val()——获取表单的值
> - val("内容")——设置表单的值





#### CSS-DOM操作

##### css()

##### height(),width()

##### offset()

##### position()

##### scrollTop(),scrollLeft()





## jQuery中的事件

### 加载DOM

原生 JavaScript：

```js
window.onload = function() {
	……
}
```

jQuery：

```js
$(document).ready(function(){
	……
})
```

### 执行时机

> 1. 原生 JavaScript 是在网页中所有的元素（包括元素的所有关联文件）完全加载到浏览器后才执行
> 2. jQuery则是在DOM完全就绪时就可以被调用，然而所有元素关联的文件都不一定下载完毕



### 事件委托

> *可以添加多个相同或者不同类型的事件,不会覆盖*

1. eventName(fn)

   > 编码效率略高/ 部分事件 jQuery 没有实现,所以不能添加

2. on(eventName，fn)

   >  编码效率略低/ 所有js事件都可以添加

#### 改变绑定事件的类型

```js
$(function(){
	$("").on("click",function(){
		……
	}).on("mouseover",function(){
		……
	})
})
```

#### 简写绑定事件

```js
$(function(){
	$("").mouseover(function(){
		……
	}).mouseout(function(){
		……
	})
})
```



### 自定义事件

想要自定义事件, 必须满足两个条件：

1. 事件必须是通过on绑定的，不能通过eventName来绑定
2. 事件必须通过trigger或triggerHandler来触发、

```js
$(".son").on("myClick", function () {
    alert("son");
});
$(".son").triggerHandler("myClick");
```





### 事件切换

#### hover()

#### toggle()



### 事件移除

off()

> 1. $("p").off()——解绑p元素所有事件处理程序
> 2. $("p").off("click")——解绑p元素上面的点击事件
> 3. $("p").off("click","li");——解绑事件委托



### 移入移出事件

> 子元素被移入移出也会触发父元素的事件

##### mouseover

##### mouseout



### 事件冒泡

事件冒泡：指子标签中监听的事件会向父标签冒泡，即==触发子标签的事件时会自动触发父标签中的事件==

**阻止事件冒泡**

> 1. 在子元素事件中添加
>
>    ```js
>    return false;
>    ```
>
> 2. 子元素的事件对象
>
>    ```js
>    1. 监听事件的函数中传一个event参数【注意是写在子标签的监听事件中】
>    2. event.stopPropagation();
>    ```



默认行为： 比如a标签或提交按钮，a标签点击时会自动跳转到指定的页面，这就是a标签的默认行为

**阻止默认事件**

> 1. 在子元素事件中添加
>
>    ```js
>    return false;
>    ```
>
> 2. 子元素的事件对象
>
>    ```js
>    1. 监听事件的函数中传一个event参数
>    2. event.preventDefault();
>    ```
>
> 

事件命名空间

> 1. 事件是通过on来绑定的
> 2. 事件自定义名称
> 3. 可以通过trigger 来触发事件





### 事件自动触发

1. $(".father").trigger("click");

   > 如果利用trigger自动触发事件,会触发==事件冒泡、默认行为==

2.  $(".father").triggerHandler("click"); 

   > 如果利用triggerHandler自动触发事件, 不会触发事件冒泡、默认行为





### 命名空间

 想要事件的命名空间有效,必须满足两个条件

1. 事件是通过on来绑定的，eventName绑定的不行
2. 可手动或通过trigger触发事件

 `.zhangsan`和`.lisi`就是事件的命名空间，用来区分监听的标签和事件名一样时，达到可分别调用不同的人写的相同事件

```js
//手动触发click.zhangsan和click.lisi事件，分别弹出click1和click2
$(".son").on("click.zhangsan", function () {
    alert("click1");
});
$(".son").on("click.lisi", function () {
    alert("click2");
});

//自动触发click.zhangsan和click.lisi事件，分别弹出click1和click2
 $(".son").trigger("click.zhangsan");
 $(".son").trigger("click.lisi");
```

利用trigger触发：

> - 触发子元素带命名空间的事件, 那么父元素==带相同命名空间的事件也会被触发==. 而父元素没有命名空间的事件不会被触发            
>
> - 触发子元素不带命名空间的事件,那么子元素所有相同类型的事件和父元素所有相同类型的事件都会被触发



### 实时监听输入框值变化

> oninput / onpropertychange 

```js
$("body").on("input propertychange", "#comment", function(){
	...
}
```





## jQuery中的动画

🌺jQuery做动画效果要求要在标准模式下

> 速度参数："slow"，"normal"，"fast"

### 🌰常见**`效果`**

#### 显示隐藏

> - show()
> - hide()
> - toggle()

#### 滑动

> - slideDown()
> - slideUp()
> - slideToggle()

#### 淡入淡出：

> - fadeln()
> - fadeOut()
> - fadeToggle()
> - fadeTo()
>   //修改透明度

#### 自定义动画

> - animate()

1. 自定义简单动画

2. 累加、累减动画：`+=`、`-=`

3. 多重动画

   1. 同时执行多个动画

   ```js
   $(this).animate({letf: "200px",height: "200px"},3000)
   ```

   2. 按顺序执行多个动画

   ```js
   $(this).animate({letf: "200px"},3000)
   	   .animate({height: "200px"},3000)
   ```

4. 综合动画

5. 🐾回调函数



### 停止动画和判断是否处于动画状态

动画或效果一旦触发就会执行，如果多次触发就造成多个动画或效果排队执行

#### stop()

##### 判断元素是否处于动画状态——is(":animated")

##### 延迟动画——delay()





