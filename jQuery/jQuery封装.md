tip：

1. > - 

2. slice()

   > 如果slice方法什么参数都没有传递，会将数组中的元素怒放到一个新的数组中原样返回

3. 真数组转换为伪数组：[].push.apply(obj,arr)

4. 伪数组转换为真数组：[].slice.call(obj)






## 基本结构

1. jQuery的本质是一个闭包（为了避免多个框架的冲突）
2. 外部访问内部定义的局部变量：==window.xxx = xxx==
3. jQuery 接受 undefined 参数（ 为了方便后期压缩代码）

```js
(function( window, undefined ) {
    // selector 用于接收参数
    var njQuery = function(selector) {
        return new njQuery.prototype.init(selector);
    }
    njQuery.prototype = {
        constructor: njQuery,
        init: ...,
        ...		// 属性和方法
    }
    njQuery.prototype.init.prototype = njQuery.prototype
    window.njQuery = window.$ =njQuery
})( window );
```



## 入口函数

入口函数传入不同参数得到的实例：

1. 传入 '' null undefined NaN  0  fals — 返回==空的jQuery对象==

   ![image-20210815223837321](https://i.loli.net/2021/08/15/QsOKzaNx7AbhJVu.png)

2. 字符串：

   - html片段 — 会将创建好的==DOM元素==存储到jQuery对象中返回

     ```js
     console.log($('<p>1</p><p>2</p><p>3</p>'));
     ```

     ![image-20210815223922069](https://i.loli.net/2021/08/15/rxlYjDUnawsfmui.png)

   - 选择器 — 会将==找到的所有元素==存储到jQuery对象中返回

     ```html
     <ul>
         <li class="item">ul中的li</li>
     </ul>
     --------------------------------------
     console.log($('li'));
     ```

     ![image-20210815224053492](https://i.loli.net/2021/08/15/3DwTcMQedLAvm2b.png)

3. 数组/伪数组 —  会将==数组中存储的元素==依次存储到jQuery对象中立返回

   ```js
   var arr = [1, 2, 3, 4, 5, 6];
   console.log($(arr));
   
   var likeArr = {0:"lnj", 1:"33", 2:"male", length: 3};
   console.log($(likeArr));
   ```

   ![image-20210815224123528](https://i.loli.net/2021/08/15/4YbOdrhpGuVPqm3.png)

4. 其他：会将传入的 ==其他== 存储到jQuery对象中返回

   ![image-20210815224240287](https://i.loli.net/2021/08/15/oHdie4EMf8quLca.png)

   - 对象
   - DOM元素
   - 基本数据类型

```js
init: function(selector){
    //去除字符串两端空格
    selector = njQuery.trim(selector)
    //'' null undefined NaN 0 false传入
    if(!selector){
        return this	
     }
     // 方法
    else if(njQuery.isFunction(selector)) {
        njQuery.ready(selector)
    }
    //传入字符串
    else if (njQuery.isString(selector)){
        //判断是否是代码片段
        if(njQuery.isHTML(selector)){
            var temp = document.creatElement("div")
            temp.innerHTML = selector;
            //通过[].push找到数组中的push方法
            //通过apply(this,temp.children)将找到的push方法内部的this修改为自定义的对象
            //将传入数组中对的元素一次取出，传递给形参
            [].push.apply(this,temp.children)
        }
        //判断是否是选择器
        else {
            //根据传入的选择器找到对应的元素
            var res = document.querySelectorAll(selector);
            //将找到的与阿奴是添加到njQuery上
            [].push.apply(this,res)
            //返回加工好的this
        }
    }
    //数组
    else if (njQuery.isArray(selector)) {
        // 将自定义的伪数组转换为真数组
        var arr = [].slice.call(selector);
        // 将真数组转换为伪数组
        [].push.apply(this.arr)
    }
    //除上述类型外
    else {
        this[0] = selector
        this.length = 1
    }
    return this
}
```

```js
njQuery.extend = njQuery.prototype.extend = function(obj) {
    for(var key in obj){
        this[key] = obj[key]
    }
}
njQuery.extend({
    isString : function(str) {
        return typeof str ==="string"
    },
    isHTML : function(str) {
        return str.charAt(0) == "<" && str.cahrAt(str.length - 1) == ">" && str.length >=3;
    },
    trim : function(str){
        if(!njQuery.isString(str)) {
            return str 
        }
        if(str.trim) {
            return str.trim()
        } else {
            return str.replace(/^\s+|\s+$/g,"")
        }
    },
    isObject : function(sele) {
        return typeof sele === "object" 
    },
    isWindow : function(sele) {
        return sele === window
    },
    isArray : function(sele) {
        if(njQuery.isObject(sele) && !njQuery.isWindow(sele) && "length" in sele){
            return true
        }
        return false
    },
    isFunction : function(sele) {
        return typeof sele === "function"
    },
    ready : function(fn) {
        if(document.readyState == "complete"){
            fn()
        }else if (document.addEventListener){
            document.addEventListener('DOMContentLoaded',function(){
                fn() 
            })
        }
        else {
            document.attachEvent('onreadystatechange',function(){
                if(document.readyState == "complete"){
                   fn() 
                }
            })
        }
}
```



## apply call

apply和call方法的作用：专门用于修改方法内部的this

```js
function test() {
    console.log(this);
}
// 输出 window
test  //window.test();
```

```js
var obj = {"name": "张三"};

/*
    1.通过window.test找到test方法
    2.通过apply(obj)将找到的test方法内部的this修改为自定义的对象
*/
window.test.apply(obj);
window.test.call(obj);
```

![image-20210815231614296](https://i.loli.net/2021/08/15/5rq8aSMg73GNoxh.png)



格式：

- call（对象，参数1，参数2，……）
- apply（对象，`[数组]`）

```js
function sum(a, b) {
    console.log(this);
    console.log(a + b);
}
/*
    1.通过window.sum找到sum方法
    2.通过apply(obj)将找到的sum方法内部的this修改为自定义的对象
    3.将传入数组中的元素依次取出, 传递给形参
*/
window.sum.call(obj, 1, 2);
window.sum.apply(obj, [3, 5]);
```

![image-20210815232044128](https://i.loli.net/2021/08/15/SU8NQc5iOnt2RzL.png)



真数组装换为伪数组：

通过[].push找到数组中的push方法：

```js
var arr = [];
arr.push(1);
```

```js
// 真数组转换伪数组的一个过程
var arr = [1, 3, 5, 7, 9];
var obj = {};
/*
    1.通过[].push找到数组中的push方法
    2.通过apply(obj)将找到的push方法内部的this修改为自定义的对象
    3.将传入数组中的元素依次取出, 传递给形参
*/
[].push.apply(obj, arr);
console.log(obj);
```

![image-20210815232731699](https://i.loli.net/2021/08/15/mQkNBFTvtYqcKw4.png)



伪数组转换为真数组：

```js
window.onload = function (ev) {
    // 系统自带的伪数组
    var res = document.querySelectorAll("div");
    // 自定义的伪数组
    var obj = {0:"lnj", 1:"33", length: 2};
    // 如果想将伪数组转换为真数组那么可以使用如下方法
    var arr = [].slice.call(obj);
    console.log(arr);
}
```

**slice()**

```js
var arr2 = [1, 3, 5, 7, 9];
// 如果slice方法什么参数都没有传递, 会将数组中的元素放到一个新的数组中原样返回
var res2 = arr2.slice();
var res2 = arr2.slice(2);	// (3)[5,7,9]
var res2 = arr2.slice(2, 4);	//(2)[5,7]	从下标2开始截取但不包括下标4
console.log(res2);
```





## extend

```js
njQuery.extend = function (obj) {
    // 此时此刻的this就是njQuery这个类
    // console.log(this);
    for(var key in obj){
        // njQuery["isTest"] = function () {console.log("test");}
        this[key] = obj[key];
    }
}
njQuery.extend({
    isTest: function () {
        console.log("test");
    }
});
njQuery.isTest();	// test
```

```js
njQuery.prototype.extend = function (obj) {
    // 此时此刻的this是njQuery对象
    // console.log(this);
    for(var key in obj){
        // q["isDemo"] = function () {console.log("demo");}
        this[key] = obj[key];
    }
}
var q = new njQuery();
q.extend({
    isDemo: function () {
        console.log("demo");
    }
});
q.isDemo();
```

结论：

```js
njQuery.extend = njQuery.prototype.extend = function (obj) {
    // console.log(this);
    for(var key in obj){
        this[key] = obj[key];
    }
}
// njQuery.extend({});		// this 指向 f njQuery(){ }
var q = new njQuery();
q.extend({});		// this 指向 njQuery
```



## 监听DOM加载

1. onload事件会等到DOM元素加载完毕, 并且还会等到资源也加载完毕才会执行
2. DOMContentLoaded事件只会等到DOM元素加载完毕就会执行回调

> addEventListener、DOMContentLoaded：IE8以下不支持



document.readyState属性有如下的状态：

>  onreadystatechange事件就是专门用于监听document.readyState属性的改变的

- uninitialized - 还未开始载入
- loading - 载入中
- interactive - 已加载，文档与用户可以开始交互
- complete - 载入完成





## 原型上的属性和方法

jQuery 原型上的核心方法和属性：

1. jquery 获取jQ版本号
2. selector 实例默认的选择器取值
3. length 实例默认的长度
4. push 给实例添加新元素
5. sort 对实例中的元素进行排序
6. splice 按照指定下标指定数量删除元素，也可以替换删除的元素
7. toArray 把实例转换为数组返回
8. get  获取指定下标的元素，获取的是原生DOM
9. eq 获取指定下标的元素，获取的是jQuery类型的实例对象
10. first 获取实例中的第一个元素，是jQuery类型的实例对象
11. last 获取实例中的最后一个元素，是jQuery类型的实例对象
12. each 遍历实例，把遍历到的数据传给回调使用
13. map  遍历实例，把遍历到的数据传给回调使用，然后把回调的返回值收集起来组成一个新的数组返回

==each 和 map 静态方法的区别==：

> 1. each静态方法默认的返回值就是，遍历谁就返回谁——不支持在回调函数中对遍历的数组进行处理
> 2. map静态方法默认的返回值就是一个空数组——可以在回调函数中通过return对遍历的数组进行处理，然后生成一个新的数组返回

**njQuery.prototype**：

```js
njQuery : "1.1.0",
selector : "",
length : 0,
push : [].push,		// 相当于 [].push.apply(this),因为push需要被 njQuery 调用
sort : [].sort,
splice :[].splice,
toArray : function(){
    return [].slice.call(this)
},
get : function(num) {
    if(argument.length === 0){
        return this.toArray()
    }
    else if(num >= 0){
        return this[num]
    }
    else{
        return this[this.length + num]
    }
},
eq : function(num){
    //没有传递参数
    if(argument.length === 0){
        return new njQuery()
    }
    //传递非负数yu负数
    else {
        return njQuery(this.get(num))
    }
},
first : function(){
    return this.eq(0)
},
last : function(){
    return this.eq(-1)
},
each : function(fn){
    njQuery.each(this,fn)
}
```

**njQuery.extend**：

```js
each: function (obj, fn) {
    // 1.判断是否是数组
    if(njQuery.isArray(obj)){
        for(var i = 0; i < obj.length; i++){
           // var res = fn(i, obj[i]);
           var res = fn.call(obj[i], i, obj[i]);
           if(res === true){
               continue;
           }else if(res === false){
               break;
           }
        }
    }
    // 2.判断是否是对象
    else if(njQuery.isObject(obj)){
        for(var key in obj){
            // var res = fn(key, obj[key]);
            var res = fn.call(obj[key], key, obj[key]);
            if(res === true){
                continue;
            }else if(res === false){
                break;
            }
        }
    }
    return obj;
},
map: function (obj, fn) {
    var res = [];
    // 1.判断是否是数组
    if(njQuery.isArray(obj)){
        for(var i = 0; i < obj.length; i++){
            var temp = fn(obj[i], i);
            if(temp){
                res.push(temp);
            }
        }
    }
    // 2.判断是否是对象
    else if(njQuery.isObject(obj)){
        for(var key in obj){
            var temp =fn(obj[key], key);
            if(temp){
                res.push(temp);
            }
        }
    }
    return res;
}
```



## DOM 操作方法

DOM 操作:

1. empty ==> 清空指定元素中的所有内容
2. remove ==> 删除所有的元素或指定元素
3. html ==> 设置所有元素的内容，获取第一个元素的内容
4. text ==> 设置所有元素的文本内容，获取所有元素的文本内容
5. 元素.appendTo.指定元素 ==> 将元素添加到指定元素内部的最后
6. 元素.prependTo.指定元素 ==> 将元素添加到指定元素内部的最前面
7. 指定元素.append.元素 ==> 将元素添加到指定元素内部的最后
8. 指定元素.prepend.元素 ==> 将元素添加到指定元素内部的最前面
9. 元素.insertBefore.指定元素  ==>将元素添加到指定元素外部的前面
10. 元素.insertAfter.指定元素  ==>将元素添加到指定元素外部的后面
11. 元素.replaceAll.指定元素 ==> 替换所有指定元素
12. clone: 复制一个元素

```js
// 来源: http://www.w3school.com.cn/xmldom/prop_node_nextsibling.asp
get_nextsibling: function (n) {
    var x = n.nextSibling;
    while (x != null && x.nodeType!=1)
    {
        x=x.nextSibling;
    }
    return x;
},
get_previoussibling: function (n) {
    var x=n.previousSibling;
    while (x != null && x.nodeType!=1)
    {
        x=x.previousSibling;
    }
    return x;
}
```

```js
// DOM操作相关方法
njQuery.prototype.extend({
    empty: function () {
        // 1.遍历指定的元素
        this.each(function (key, value) {
            value.innerHTML = "";
        });
        // 2.方便链式编程
        return this;
    },
    remove: function (sele) {
        if(arguments.length === 0){
            // 1.遍历指定的元素
            this.each(function (key, value) {
                // 根据遍历到的元素找到对应的父元素
                var parent = value.parentNode;
                // 通过父元素删除指定的元素
                parent.removeChild(value);
            });
        }else{
            var $this = this;
            // 1.根据传入的选择器找到对应的元素
            $(sele).each(function (key, value) {
                // 2.遍历找到的元素, 获取对应的类型
                var type = value.tagName;
                // 3.遍历指定的元素
                $this.each(function (k, v) {
                    // 4.获取指定元素的类型
                    var t = v.tagName;
                    // 5.判断找到元素的类型和指定元素的类型
                    if(t === type){
                        // 根据遍历到的元素找到对应的父元素
                        var parent = value.parentNode;
                        // 通过父元素删除指定的元素
                        parent.removeChild(value);
                    }
                });
            })
        }
        return this;
    },
    html: function (content) {
        if(arguments.length === 0){
            return this[0].innerHTML;
        }else{
            this.each(function (key, value) {
                value.innerHTML = content;
            })
        }
    },
    text: function (content) {
        if(arguments.length === 0){
            var res = "";
            this.each(function (key, value) {
                res += value.innerText;
            });
            return res;
        }else{
            this.each(function (key, value) {
                value.innerText = content;
            });
        }
    },
    appendTo: function (sele) {
        // 1.统一的将传入的数据转换为jQuery对象
        var $target = $(sele);
        var $this = this;
        var res = [];
        // 2.遍历取出所有指定的元素
        $.each($target, function (key, value) {
            // 2.遍历取出所有的元素
            $this.each(function (k, v) {
                // 3.判断当前是否是第0个指定的元素
                if(key === 0){
                    // 直接添加
                    value.appendChild(v);
                    res.push(v);
                }else{
                    // 先拷贝再添加
                    var temp = v.cloneNode(true);
                    value.appendChild(temp);
                    res.push(temp);
                }
            });
        });
        // 3.返回所有添加的元素
        return $(res);
    },
    prependTo: function (sele) {
        // 1.统一的将传入的数据转换为jQuery对象
        var $target = $(sele);
        var $this = this;
        var res = [];
        // 2.遍历取出所有指定的元素
        $.each($target, function (key, value) {
            // 2.遍历取出所有的元素
            $this.each(function (k, v) {
                // 3.判断当前是否是第0个指定的元素
                if(key === 0){
                    // 直接添加
                    value.insertBefore(v, value.firstChild);
                    res.push(v);
                }else{
                    // 先拷贝再添加
                    var temp = v.cloneNode(true);
                    value.insertBefore(temp, value.firstChild);
                    res.push(temp);
                }
            });
        });
        // 3.返回所有添加的元素
        return $(res);
    },
    append: function (sele) {
        // 判断传入的参数是否是字符串
        if(njQuery.isString(sele)){
            this[0].innerHTML += sele;
        }else{
            $(sele).appendTo(this);
        }
        return this;
    },
    prepend: function (sele) {
        // 判断传入的参数是否是字符串
        if(njQuery.isString(sele)){
            this[0].innerHTML = sele + this[0].innerHTML;
        }else{
            $(sele).prependTo(this);
        }
        return this;
    },
    insertBefore: function (sele) {
        // 1.统一的将传入的数据转换为jQuery对象
        var $target = $(sele);
        var $this = this;
        var res = [];
        // 2.遍历取出所有指定的元素
        $.each($target, function (key, value) {
            var parent = value.parentNode;
            // 2.遍历取出所有的元素
            $this.each(function (k, v) {
                // 3.判断当前是否是第0个指定的元素
                if(key === 0){
                    // 直接添加
                    parent.insertBefore(v, value);
                    res.push(v);
                }else{
                    // 先拷贝再添加
                    var temp = v.cloneNode(true);
                    parent.insertBefore(temp, value);
                    res.push(temp);
                }
            });
        });
        // 3.返回所有添加的元素
        return $(res);
    },
    insertAfter: function (sele) {
        // 1.统一的将传入的数据转换为jQuery对象
        var $target = $(sele);
        var $this = this;
        var res = [];
        // 2.遍历取出所有指定的元素
        $.each($target, function (key, value) {
            var parent = value.parentNode;
            var nextNode = $.get_nextsibling(value);
            // 2.遍历取出所有的元素
            $this.each(function (k, v) {
                // 3.判断当前是否是第0个指定的元素
                if(key === 0){
                    // 直接添加
                    parent.insertBefore(v, nextNode);
                    res.push(v);
                }else{
                    // 先拷贝再添加
                    var temp = v.cloneNode(true);
                    parent.insertBefore(temp, nextNode);
                    res.push(temp);
                }
            });
        });
        // 3.返回所有添加的元素
        return $(res);
    },
    replaceAll: function (sele) {
        // 1.统一的将传入的数据转换为jQuery对象
        var $target = $(sele);
        var $this = this;
        var res = [];
        // 2.遍历取出所有指定的元素
        $.each($target, function (key, value) {
            var parent = value.parentNode;
            // 2.遍历取出所有的元素
            $this.each(function (k, v) {
                // 3.判断当前是否是第0个指定的元素
                if(key === 0){
                    // 1.将元素插入到指定元素的前面
                    $(v).insertBefore(value);
                    // 2.将指定元素删除
                    $(value).remove();
                    res.push(v);
                }else{
                    // 先拷贝再添加
                    var temp = v.cloneNode(true);
                    // 1.将元素插入到指定元素的前面
                    $(temp).insertBefore(value);
                    // 2.将指定元素删除
                    $(value).remove();
                    res.push(temp);
                }
            });
        });
        // 3.返回所有添加的元素
        return $(res);
    }
});
```

```js
	// 筛选相关方法
    njQuery.prototype.extend({
        next: function (sele) {
            var res = [];
            if(arguments.length === 0){
                // 返回所有找到的
                this.each(function (key, value) {
                    var temp = njQuery.get_nextsibling(value);
                    if(temp != null){
                        res.push(temp);
                    }
                });
            }else{
                // 返回指定找到的
                this.each(function (key, value) {
                    var temp = njQuery.get_nextsibling(value)
                    $(sele).each(function (k, v) {
                        if(v == null || v !== temp) return true;
                        res.push(v);
                    });
                });
            }
            return $(res);
        },
        prev: function (sele) {
            var res = [];
            if(arguments.length === 0){
                this.each(function (key, value) {
                    var temp = njQuery.get_previoussibling(value);
                    if(temp == null) return true;
                    res.push(temp);
                });
            }else{
                this.each(function (key, value) {
                    var temp = njQuery.get_previoussibling(value);
                    $(sele).each(function (k, v) {
                        if(v == null || temp !== v) return true;
                        res.push(v);
                    })
                });
            }
            return $(res);
        }
    });
```





## 属性操作相关方法

1. attr(): 设置或者获取元素的属性节点值

   > - 传递一个参数, 返回第一个元素属性节点的值
   > - 传递两个参数, 代表设置所有元素属性节点的值，并且返回值就是方法调用者
   > - 传递一个对象, 代表批量设置所有元素属性节点的值

2. prop(): 设置或者获取元素的属性值

   > - 传递两个参数, 代表设置所有元素属性节点的值，并且返回值就是方法调用者
   > - 传递一个参数, 返回第一个元素属性节点的值
   > - 传递一个对象, 代表批量设置所有元素属性节点的值

3. css(): 设置获取样式

   > - 传递一个参数, 返回第一个元素指定的样式
   > - 传递两个参数, 代表设置所有元素样式，并且返回值就是方法调用者
   > - 传递一个对象, 代表批量设置所有元素样式

4. val(): 获取设置value的值

   > - 不传递参数, 返回第一个元素指定的样式
   > - 传递两个参数, 代表设置所有元素样式，并且返回值就是方法调用者

5. hasClass(): 判断元素中是否包含指定类

   > - 传递参数, 只要调用者其中一个包含指定类就返回true,否则返回false
   > - 没有传递参数, 返回false

6. addClass(): 给元素添加一个或多个指定的类

   > - 传递参数, 如果元素中没有指定类就添加, 有就不添加
   > - 没有传递参数,不做任何操作,返回this
   > - 会返回this方便链式编程 

7. removeClass(): 删除元素中一个或多个指定的类

   > - 传递参数, 如果元素中有指定类就删除
   > - 没有传递参数, 删除所有类
   > - 会返回this方便链式编程

8. toggleClass(): 没有则添加,有则删除

   > 1. 传递参数, 如果元素中没有指定类就添加, 有就不添加
   > 2. 没有传递参数, 删除所有类
   > 3. 会返回this方便链式编程



```js
	// 属性操作相关的方法
    njQuery.prototype.extend({
        attr: function (attr, value) {
            // 1.判断是否是字符串
            if(njQuery.isString(attr)){
                // 判断是一个字符串还是两个字符串
                if(arguments.length === 1){
                    return this[0].getAttribute(attr);
                }else{
                    this.each(function (key, ele) {
                        ele.setAttribute(attr, value);
                    });
                }
            }
            // 2.判断是否是对象
            else if(njQuery.isObject(attr)){
                var $this = this;
                // 遍历取出所有属性节点的名称和对应的值
                $.each(attr, function (key, value) {
                    // 遍历取出所有的元素
                    $this.each(function (k, ele) {
                        ele.setAttribute(key, value);
                    });
                });
            }
            return this;
        },
        prop: function (attr, value) {
            // 1.判断是否是字符串
            if(njQuery.isString(attr)){
                // 判断是一个字符串还是两个字符串
                if(arguments.length === 1){
                    return this[0][attr];
                }else{
                    this.each(function (key, ele) {
                        ele[attr] = value;
                    });
                }
            }
            // 2.判断是否是对象
            else if(njQuery.isObject(attr)){
                var $this = this;
                // 遍历取出所有属性节点的名称和对应的值
                $.each(attr, function (key, value) {
                    // 遍历取出所有的元素
                    $this.each(function (k, ele) {
                        ele[key] = value;
                    });
                });
            }
            return this;
        },
        css: function (attr, value) {
            // 1.判断是否是字符串
            if(njQuery.isString(attr)){
                // 判断是一个字符串还是两个字符串
                if(arguments.length === 1){
                    return njQuery.getStyle(this[0], attr);
                }else{
                    this.each(function (key, ele) {
                        ele.style[attr] = value;
                    });
                }
            }
            // 2.判断是否是对象
            else if(njQuery.isObject(attr)){
                var $this = this;
                // 遍历取出所有属性节点的名称和对应的值
                $.each(attr, function (key, value) {
                    // 遍历取出所有的元素
                    $this.each(function (k, ele) {
                        ele.style[key] = value;
                    });
                });
            }
            return this;
        },
        val: function (content) {
            if(arguments.length === 0){
                return this[0].value;
            }else{
                this.each(function (key, ele) {
                    ele.value = content;
                });
                return this;
            }
        },
        hasClass: function (name) {
            var flag = false;
            if(arguments.length === 0){
                return flag;
            }else{
                this.each(function (key, ele) {
                    // 1.获取元素中class保存的值
                    var className = " "+ele.className+" ";
                    // 2.给指定字符串的前后也加上空格
                    name = " "+name+" ";
                    // 3.通过indexOf判断是否包含指定的字符串
                    if(className.indexOf(name) != -1){
                        flag = true;
                        return false;
                    }
                });
                return flag;
            }
        },
        addClass: function (name) {
            if(arguments.length === 0) return this;

            // 1.对传入的类名进行切割
            var names = name.split(" ");
            // 2.遍历取出所有的元素
            this.each(function (key, ele) {
                // 3.遍历数组取出每一个类名
                $.each(names, function (k, value) {
                    // 4.判断指定元素中是否包含指定的类名
                    if(!$(ele).hasClass(value)){
                        ele.className = ele.className + " " + value;
                    }
                });
            });
            return this;
        },
        removeClass: function (name) {
            if(arguments.length === 0){
                this.each(function (key, ele) {
                    ele.className = "";
                });
            }else{
                // 1.对传入的类名进行切割
                var names = name.split(" ");
                // 2.遍历取出所有的元素
                this.each(function (key, ele) {
                    // 3.遍历数组取出每一个类名
                    $.each(names, function (k, value) {
                        // 4.判断指定元素中是否包含指定的类名
                        if($(ele).hasClass(value)){
                            ele.className = (" "+ele.className+" ").replace(" "+value+" ", "");
                        }
                    });
                });
            }
            return this;
        },
        toggleClass: function (name) {
            if(arguments.length === 0){
                this.removeClass();
            }else{
                // 1.对传入的类名进行切割
                var names = name.split(" ");
                // 2.遍历取出所有的元素
                this.each(function (key, ele) {
                    // 3.遍历数组取出每一个类名
                    $.each(names, function (k, value) {
                        // 4.判断指定元素中是否包含指定的类名
                        if($(ele).hasClass(value)){
                            // 删除
                            $(ele).removeClass(value);
                        }else{
                            // 添加
                            $(ele).addClass(value);
                        }
                    });
                });
            }
            return this;
        }
    });
```









## 事件操作相关方法

1. on(type, callback): 注册事件

2. off(type, callback): 移出事件

   > 注册多个相同类型事件, 后注册的不会覆盖先注册的
   > 注册多个不同类型事件, 后注册的不会覆盖先注册的

```js
	// 事件操作相关的方法
    njQuery.prototype.extend({
        on: function (name, callBack) {
            // 1.遍历取出所有元素
            this.each(function (key, ele) {
                // 2.判断当前元素中是否有保存所有事件的对象
                if(!ele.eventsCache){
                    ele.eventsCache = {};
                }
                // 3.判断对象中有没有对应类型的数组
                if(!ele.eventsCache[name]){
                    ele.eventsCache[name] = [];
                    // 4.将回调函数添加到数据中
                    ele.eventsCache[name].push(callBack);
                    // 5.添加对应类型的事件
                    njQuery.addEvent(ele, name, function () {
                        njQuery.each(ele.eventsCache[name], function (k, method) {
                            method.call(ele);
                        });
                    });
                }else{
                    // 6.将回调函数添加到数据中
                    ele.eventsCache[name].push(callBack);
                }
            });
            return this;
        },
        off: function (name, callBack) {
            // 1.判断是否没有传入参数
            if(arguments.length === 0){
                this.each(function (key, ele) {
                    ele.eventsCache = {};
                });
            }
            // 2.判断是否传入了一个参数
            else if(arguments.length === 1){
                this.each(function (key, ele) {
                    ele.eventsCache[name] = [];
                });
            }
            // 3.判断是否传入了两个参数
            else if(arguments.length === 2){
                this.each(function (key, ele) {
                    njQuery.each(ele.eventsCache[name], function (index, method) {
                        // 判断当前遍历到的方法和传入的方法是否相同
                        if(method === callBack){
                            ele.eventsCache[name].splice(index,  1);
                        }
                    });
                });
            }
            return this;
        }
    });
```











































































