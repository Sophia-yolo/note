

# 渐进式 JavaScript 框架

中文文档：https://cn.vuejs.org/v2/guide/

## 优点

1. 体积小
2. 更高的运行效率
3. 双向数据绑定
4. 生态丰富、学习成本低



## 特点

1. 组件化模块
2. 声明式编码
3. 虚拟DOM + Diff 算法



![image-20210628165047875](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210628165047875.png)





# 模板语法

`vue`模板

## 创建第一个vue应用

```html
<div id="app"> {{ message }} </div>
```

```js
const app = new Vue({  
    el: '#app',  
    data: {    
        message: 'Hello Vue!'  
    }
})
```

**响应式的**：打开你的浏览器的 JavaScript 控制台 (就在这个页面打开)，并修改 `app.message` 的值，你将看到上例相应地更新。

> 1. 容器与vue实例一一对应
>
> 2. Mustache插值操作——`{{}}`：响应式
>
>    > 语法
>    >
>    > - 可以直接写变量
>    > - 可以用 `+` 连接简单的 表达式



## 插值语法

1. 功能：用于解析标签体内容

2. 写法：{{xxx}}  xxx中填写 `js表达式`，“xxx”可以直接读取data 中的属性

   ```js
   {{ number + 1 }}
   {{ ok ? 'YES' : 'NO' }}
   {{ message.split('').reverse().join('') }}
   ```

   

### 插值

`v-once`：不希望界面随意跟随改变

> 1. v-once 所在节点在初次动态渲染后，就视为静态内容
> 2. 以后数据的改变不会引起 v-once 所在的结构更新，可以用于优化性能 

`v-html`：解析出HTML展示（存在安全性问题——容易导致 XSS 攻击）

`v-text`

> 1. 作用：向其所在的节点中渲染文本内容
> 2. 与插值语法的区别：v-text会替换掉节点中的内容，而{{xxx }} 不会

```html
<div v-text="name"></div>
```

`v-pre`：跳过这个元素和他子元素的编译过程，用于显示原来的Mustache语法

`v-cloak`

> 1. 本质是一个特殊属性，Vue 实例创建完毕并接管容器后，会删除掉 v-cloak 属性
> 2. 使用 css 配合 v-cloak 可以解决网速慢时页面展示出 {{ xxx }} （未经解析）的问题



## 指令语法

功能：用于解析标签（包括：标签属性、标签体内容、绑定事件....)

指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute。它们会在渲染的 DOM 上应用特殊的响应式行为。

### v-bind(动态绑定属性)

基本使用  `v-bind:src="imgURL"`

语法糖 `:` 

> 🌰	:src="imgURL"

### 条件与循环

`v-for`：列表的展示

> 🌰：v-for = "变量名  in  列表名"

### [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

函数何时调用？

1. 指令与元素成功绑定时
2. 指令所在的模板被重新解 析时 



## 数据绑定

单向绑定：v-bind

双向绑定：v-model

v-model ：

> 1. 只能应用在表单元素（输入类元素）
> 2. 简写：v-model
>



## el 的两种写法

> - 类型：string | HTMLElement
> - 作用：决定之后 Vue 实例会管理哪一个DOM

1. $mount(' ')

   ```js
   //1. 创建Vue实例
   const v = new vue({
   	data: {
   		name: "法外狂徒张三"
   	}
   })
   v.$mount("#root")
   ```

2. el: "#root"

   > 直接在 `new Vue`的时候配置el属性



## methods

- 类型：{ [key：string]：Function}
- 作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用。



## data 的两种写法

1. 对象式

   ```js
   data: {
   	name: "法外狂徒张三"
   }
   ```

2. 函数式⭐

   > 不可以写成箭头函数
   
   ```js
   data: function(){
       //此处的this 是vue 实例对象
   	return{
   		name: "法外狂徒张三"
   	}
   }
   ```
   
   

# vue中的MVVM

MVVM：Model View ViewModel

![img](https://upload-images.jianshu.io/upload_images/17785488-1640581647696975.png?imageMogr2/auto-orient/strip|imageView2/2/w/758/format/webp)

1. M：对应data中的数据
2. V：模板
3. VM：Vue实例对象





# 数据代理

[Object.defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

🌰：

```js
let number = 18
const object1 = {
	name: '法外狂徒',
	sex: '男'
}

Object.defineProperty(object1, 'property1',{
	//value: 18,
	//enumerable: true, //控制属性是否可以枚举，默认值是false
    //writable: true,	//控制属性是否可以被修改，默认值是false
    //configurable:true	//控制属性是否可以被删除，默认值是false
    
    get: function(){
		return number
	}
})
```



vue中的数据代理：

> 通过 v 对象来代理 data 对象中属性的操作（读/写）

基本原理：

1. 通过Object.defineProperty()把data 对象中所有属性添加到v 对象上
2. 为每个添加到v 上的属性，都指定一个getter/setter
3. 在 getter/setter 内部区操作（读/写）data 中对应的属性





# 事件处理

> 用 `v-on` 指令添加一个事件监听器

`v-on:click`：监听点击事件

🌰：

```html
<div id="app-5">
  <p>{{ message }}</p>
  //添加 prevent 阻止标签的默认行为
  <a href="http://baidu.com" v-on:click.prevent="reverseMessage(666,$event).prevent">反转消息</a>
</div>
```

```js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage(number,e) {
		//e（event）是事件对象：MosesEvent
        //此处的 this 是 app5
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

`@click`：用于监听某个元素的点击事件，并且需要制定当发生点击时候，执行的方法（方法通常是methods中定义的方法



### 事件修饰符

1. prevent：阻止默认行为（常用）
2. stop：阻止事件冒泡（常用）
3. once：事件只触发一次（常用）
4. capture：事件的捕获模式
5. self：只有 `event.target` 是当前操作的元素时才触发事件
6. passive：事件的默认行为立即执行，无需等待回调执行完毕（更适用与移动端）



### 键盘事件：keyup/keydown

🌰：

```js
	Vue.config.productionTip = false;
		//创建 vue 实例
        const v = new Vue({
            el: "#root" ,// 用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符
            data: {     //data 中用于存储数据，数据供el所指定的容器去使用
                name: '张三'
            },
            methods:{
                showinfo(e){
                    console.log(e.target.value);
                }
            }
        })
```

1. vue 常用的按键别名：

> 1. 回车 =>  enter（原名：Enter）
> 2. 删除 => delete（捕获“删除”和“退格”键）
> 3. 退出 => esc
> 4. 空格 => space
> 5. 换行 => tab ————> (特殊：必须配合`keydown`)
> 6. 上 => up
> 7. 下 => down
> 8. 左 => left
> 9. 右 => right

2. Vue 未提供别名的按键，可以使用原始的key 值去绑定，但注意要转为 kebab-case（短横线命名）
3. 系统修饰键：ctrl 、alt、shift、meta(start)
   - 配合 keyup 使用：按下修饰键的同时，在按下其他按键，再释放其他按键，事件才被触发
   - 配合 keydown 使用
4. * Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别







# 计算属性和侦听器

## 计算属性：computed

`computed`：get()、set()

1. 定义：要用的属性不存在，要通过已有属性计算得来
2. 原理：底层借组了`Object.defineproperty` 方法提供的 getter 和 setter

get()

1. 作用：当有人读取计算属性时，get 就会被调用，而且返回的是计算属性的返回值
2. 什么时候调用？
   - 初次读取计算属性时
   - 所依赖的数据发生变化时
3. 优势：与methods 实现相比，内部有缓存机制（复用），效率高，调试方便
4. 备注：
   - 计算属性最终会出现在v上，直接读取使用即可
   - 如果计算属性要被修改，那必须写set 函数去响应修改，且set 中要引起计算时依赖的数据发生改变

🌰：

```html
	<div id="root">
        姓：<input type="text" v-model="firstName" >
        名：<input type="text" v-model="lastName">
        姓名如下：<span>{{fullName}}</span>
    </div>
```

```js
		const v = new Vue({
            el: "#root",
            data: {
                firstName: '',
                lastName: ''
            },
            computed:{
                fullName:{
                    get(){
                        return this.firstName + '-' + this.lastName
                    },
                    set(value){
                        const arr = value.split('-')
                        this.firstName = arr[0]
                        this.lastName = arr[1]
                    }
                }
                //简写的形式
                fullName(){
                    return this.firstName + '-' + this.lastName

                }
            }
```

![image-20210715001441683](https://i.loli.net/2021/07/29/JD5lSo7zpfULQR9.png)



## 监视属性：watch

可以

1. 当被监视的属性变化时，回调函数自动调用，进行相关操作
2. 监视的属性必须存在，才能进行监视
3. 监视的两种写法
   - .new Vue 时传入 watch 配置
   - 通过 v.$watch配置

handler

> 什么时候调用？当相关属性发生改变时

immediate：立即执行

🌰：

```html
 	<div id="root">
        <h1>今天天气很{{info}}</h1>
        <!-- 绑定事件的时候 @xxx = "yyy" yyy可以写有些简单的语句 -->
        <button @click="isHot = !isHot">点击切换</button>
    </div>
```

```js
	<script>
        Vue.config.productionTip = false;

        const v = new Vue({
            el: "#root",
            data: {
                isHot: true
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            // 第一种写法
            watch: {
                isHot: {
                    immediate: true,
                    handler(newvalue,oldvalue){
                        console.log(newvalue,oldvalue);
                    }
                }
            },
            //第一种写法的简写形式
            watch: {
            	isHot(newvalue,oldvalue){
            		console.log(newvalue,oldvalue);
        		}
        	}
        })
        //第二种写法
        v.$watch('isHot',{
            immediate: true,
            handler(newvalue,oldvalue){
                console.log(newvalue,oldvalue);
            }
        })
		//第二种的简写写法
		v.$watch('isHot',function(newvalue,oldvalue){
            console.log(newvalue,oldvalue);
        })
        
    </script>
```



### 深度监视

1. Vue 中的 watch 默认不监视对象内部值的改变（一层）
2. 配置 `deep：true`  可以监视对象内部值改变（多层）

备注：

1. Vue 自身可以监视对象内部值的改变，但Vue提供的 watch 默认不可以
2. 使用 watch 时根据数据的具体结构，决定是否采用深度监视

🌰：

```html
	<div id="root">
        <h1>a 的值是 {{number.a}}</h1>
        <button @click="number.a++">点击实现 a+1</button>
    </div>
```

```js
	<script>
        Vue.config.productionTip = false;
        const v = new Vue({
            el: "#root",
            data: {
                number: {
                    a: 1,
                    b: 1
                }
            },
            watch: {
                number: {
                    deep: true,
                    handler(){
                        console.log('number被改变了');
                    }
                }
            }
        })
    </script>
```



computed 和 watch 之间的区别

1. computed能完成的功能，watch 都可以完成
2. watch 能完成的功能，computed 不一定能完成，例如：watch 可以进行异步操作

两个重要的小原则：

1. 所被 Vue 管理的函数，最好写成普通函数这样this的指向才是 v 或 组件实例对象
2. 所有不被 Vue 所管理的函数（定时器回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样this 的指向才是 v 或 组件实例对象





# Class 与 style 绑定

- 在应用界面中, 某个(些)元素的样式是变化的 
- class/style 绑定就是专门用来实现动态样式效果的技术

绑定Class 样式

1. 字符串写法，适用于：样式的类名不确定、需要动态指定

   ```js
   :class = "classA"
   ```

2. 数组写法，适用于：要绑定的样式个数不确定、名字也不确定

   ```js
   :class = "classArr"
   ```

   ```js
   data: {
   	classArr: ['active','text-danger']
   }
   ```

   渲染结果：

   ```html
   <div class="active text-danger"></div>
   ```

3. 对象语法，适用于：要绑定的样式个数确定、名字也确定、但需要动态决定用不用

   ```js
   :class = "classObj"
   ```



绑定style 样式

1. 对象写法

   ```js
   :style="{ color: activeColor, fontSize: fontSize + 'px' }"
   //（其中 activeColor/fontSize 是 data 属性 ）
   ```

2. 数组写法

   ```js
   :styel = [a,b]	//其中a、b是样式对象
   ```





# 条件渲染

## v-show

1. 写法：v-show = "表达式"

   ```js
   v-show="false"
   v-show="1 === 3"
   ```

2. 适用于：切换频率较高的场景

3. 特点：不展示DOM元素未被移除，仅仅是使用样式隐藏掉



## v-if

1. 写法
   - v-if = "表达式"
   - v-else-if = "表达式"
   - v-else = "表达式"
   - 与 template 元素配合使用
2. 适用于：切换频率较低的场景
3. 特点：不展示DOM元素直接被移除
4. 注意：v-if 可以和：v-else-if、v-else 一起使用，但要求结构不能被打断





# 列表渲染：v-for

1. 遍历数组
2. 遍历对象
3. 遍历字符串
4. 遍历指定次数

## key内部原理

#### 虚拟DOM中key 的作用

> 虚拟DOM对象的标识，当状态中的数据发生改变时，Vue 会根据【新数据】生成【新的虚拟DOM】，随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较



#### 对比规则

1. 旧虚拟DOM中找到了与新虚拟DOM相同的key
   - 旧虚拟DOM中内容没变，直接使用之前的真实DOM
   - 若虚拟DOM中内容变了，则生成新的DOM，随后替换页面中之前的真实DOM
2. 旧虚拟DOM中未找到与新虚拟DOM相同的key
   - 创建新的真实DOM，随后渲染到页面



#### 用index作为 key 可能会引发的问题

1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作

   > 会产生没有必要的真实DOM更新 ==> 界面效果没问题，但效率低

2. 如果结构中包含输入类的DOM：会产生错误DOM更新 ==> 界面有问题



#### 开发中如何选择key？

id 作为 key：

![列表排序 key 的作用(id)](https://i.loli.net/2021/07/29/OGFQMPqLX6c9f7e.jpg)

index 作为 key值：

![列表排序 key 的作用(index)](https://i.loli.net/2021/07/29/9BUDewRK1Y7HZpA.jpg)

1. 最好使用每条数据的唯一标识作为key，比如 id，手机号，身份证号，学号等唯一值
2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的



## 列表过滤

![image-20210715230413162](https://i.loli.net/2021/07/29/6ePGCA2NQRIKp8M.png)

```html
<div id="root">
    <h1>列表渲染</h1>
    <input type="text" v-model="keyWord">
    <ul v-for="(item,index) in restudents" :key="item.id>
        <li>{{item.name}}-{{item.sex}}-{{item.age}}</li>
    </ul>
</div>
```

### 监视属性：watch

```js
	const v = new Vue({
            el: "#root",
            data: {
                keyWord:"",
                students:[
                    {id:1813023001,name:'王小二',sex:"男",age:"18"},
                    {id:1813023002,name:'张三',sex:"女",age:"18"},
                    {id:1813023003,name:'李小四',sex:"男",age:"18"},
                    {id:1813023004,name:'王五',sex:"女",age:"18"}
                ],
                restudents:[]
            },
            watch:{
                keyWord:{
                    immediate:true,
                    handler(value){
                        this.restudents = this.students.filter((S)=>{
                        	//当输入为 “”时，indexOf的值为0，则可以显示原页面
                            return S.name.indexOf(value) !== -1
                        })
                    }
                }
            }
        })
```

### 计算属性：computed

```js
	const v = new Vue({
            el: "#root",
            data: {
                keyWord:"",
                students:[
                    {id:1813023001,name:'王小二',sex:"男",age:"18"},
                    {id:1813023002,name:'张三',sex:"女",age:"18"},
                    {id:1813023003,name:'李小四',sex:"男",age:"18"},
                    {id:1813023004,name:'王五',sex:"女",age:"18"}
                ]
            },
            computed:{
                restudents(){
                    return this.students.filter((S)=>{
                        return S.name.indexOf(this.keyWord) !== -1
                    })
                }
            }
        })
```



### 列表排序

```html
	<div id="root">
        <h1>列表渲染</h1>
        <button @click="sortType = 2">升序</button>
        <button @click="sortType = 1">降序</button>
        <button @click="sortType = 0">原顺序</button>
        <input type="text" v-model="keyWord">
        <ul v-for="(item,index) in restudents" :key="item.id">
            <li>{{item.name}}-{{item.sex}}-{{item.age}}</li>
        </ul>
    </div>
```

```js
	const v = new Vue({
            el: "#root",
            data: {
                keyWord:"",
                sortType: 0,
                students:[
                    {id:1813023001,name:'王小二',sex:"男",age:"0"},
                    {id:1813023002,name:'张三',sex:"女",age:"180"},
                    {id:1813023003,name:'李小四',sex:"男",age:"3"},
                    {id:1813023004,name:'王五',sex:"女",age:"120"}
                ]
            },
            computed:{
                restudents(){
                    //对姓名进行过滤，类似模糊查询
                    const arr = this.students.filter((S)=>{
                        return S.name.indexOf(this.keyWord) !== -1
                    })
                    if(this.sortType){
                        arr.sort((S1,S2)=>{
                            return this.sortType === 1 ? S2.age - S1.age : S1.age - S2.age
                        })
                    }
                    return arr
                }
            }
        })
```





# 监视数据

1. vue 会监视data中所有层次的数据

2. 如何监测对象中的数据？

   ​	通过 setter 实现监视，且要在 new vue 时就传入要监测的数据

   - 对象中后追加的属性，Vue 默认不做响应式处理

   - 如需给后添加的属性做响应式，则使用如下AP：

     > 1. Vue.set(target, propertyName/index, value)
     > 2. v.$set(target, propertyName/index, value)

3. 如何监测数组中的数据？

   通过包裹数据更新元素的方法实现，本质就是做了两件事：

   - 调用原生对应的方法对数组进行更新
   - 重新解析模板，进而更新页面

4. 在 Vue 修改数组中的某个元素一定要用如下方法：

   - 使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
   - Vue.set()  或  v.$set()

5. 特别注意：Vue.set() 或  v.$set()  不能给v 或者v的根数据对象添加属性



# 收集表单数据

```html
	<div id="root">
        <form @submit.prevent="demo">
            账号：<input type="text" v-model.trim="userInfo.account"><br><br>
            密码：<input type="password" v-model="userInfo.password"> <br><br>
            年龄：<input type="number" v-model.number="userInfo.age"> <br><br>
            性别：
            男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
            女<input type="radio" name="sex" v-model="userInfo.sex" value="female"><br><br>
            爱好：
            学习<input type="checkbox" v-model="userInfo.hobby" value="study">
            睡觉<input type="checkbox" v-model="userInfo.hobby" value="sleep">
            吃饭<input type="checkbox" v-model="userInfo.hobby" value="food"><br><br>
            信息：
            //lazy 懒加载——失去焦点的瞬间获取数据
            <textarea v-model.lazy="userInfo.msg"></textarea><br><br>
            <input type="checkbox" v-model="userInfo.agree">同意<a href="http://baidu.com">《oooo》协议</a><br><br>
            <button style="display: inline-block; width: 200px; height: 50px; line-height: 50px;">注册</button>
        </form>
    </div>
```

```js
        Vue.config.productionTip = false;
        const v = new Vue({
            el: "#root",
            data:{
                userInfo:{
                    account:'',
                    password:'',
                    age:'',
                    sex:'',
                    hobby:[],
                    msg:'',
                    agree:''
                }
            },
            methods:{
                demo(){
                    console.log(JSON.stringify(this.userInfo))
                }
            }
        })
```



# 过滤器

定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）

语法：

1. 注册过滤器：`Vue.filter(name, callback)` 或  `new Vue(filter:{ })`

   ```js
   //全局过滤器 
   Vue.filter('myslice', function(value){
   	return value.silce(0,4)
   })
   //局部过滤器,str 表示在没有传参的前提下规定格式
   filter:{
   	timeFormat(vallue,str="YYYY年MM月DD日 HH:mm:ss"){
   		return dayjs(value).format(str)
   	}
   }
   ```

2. 使用过滤器：{{ xxx  |  过滤器名}}  或 v-bind属性 = “ xxx | 过滤器名”

   ```html
   {{ time | timeFormaster('YYYY-MM-DD') | mysilce}}
   ```

   

备注；

1. 过滤器也可以接受额外参数、多个过滤器也可以实现串联
2. 并没有改变原本的数据，是产生新的对应的数据





# [生命周期](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90)

![生命周期](https://i.loli.net/2021/07/29/kZHgsNfWzq8BGTp.png)

常用的生命周期钩子：

1. mounted ：发送 ajax 请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】
2. beforeDestroy：清除定时器、解绑自定义事件、取消订阅等【收尾工作】

> 1. 又名：生命周期回调函数，生命周期函数，生命周期钩子
> 2. 生命周期是：Vue在关键时刻帮我们调用的一些特殊名称的函数
> 3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
> 4. 生命周期函数中的 this 指向是 v 或者 组件实例对象

`debugger`——断点 

## **vue 生命周期分析** 

1) 初始化显示 

> -  beforeCreate() 
> - created() 
> - beforeMount()  
> - mounted() 

2) 更新状态: this.xxx = value 

> - beforeUpdate() 
> - updated()

3) 销毁 vue 实例:  vm.$destory()调用时 

> - beforeDestory() 
> - destoryed() 

关于销毁 vue 实例：

1. 销毁后借助 vue 开发者工具看不到消息
2. 销假后自定义事件会失效，但原生DOM 事件依然生效
3. 一般不会在 beforeDestroy 操作数据，因为即便操作数据，也不会在除非更新流程了







# 组件

传统组成：

![传统组成](https://i.loli.net/2021/07/29/oGXzl7Ys9AVEHyc.png)

vue中的组件方式：

![组件](https://i.loli.net/2021/07/29/OPlJIVHxd95CU4j.png)

## [基本实例](https://cn.vuejs.org/v2/guide/components.html)

组件的定义：实现应用中**局部**功能**代码**和**资源**的集合

```html
	<div id="root">
        <school></school>
    </div>
```

```js
	const school = Vue.extend({
            template: `
                <div>
                    <h3>{{name}}</h3>
                    <h3>{{address}}</h3>
                </div>
            `,
        	// data 必须是个函数
            data(){
               return({
                name: 'oooo',
                address: 'china'
               })
            }
        })
        Vue.config.productionTip = false;
        new Vue({
            el:'#root',
            components:{
                school
            }
        })
```



## VueComponent（非单文件组件）

1. 上述代码中的school 组件本质上是一个名为 VueComponent 的构造函数，且不是程序员定义的，是 Vue.extend 生成的

2. 我们只需要写 <school></school>  或 <school> ,Vue 解析时会帮我们创建school 组件的实例对象（即 Vue 帮我们执行的： new VueComponent（option）

3. 特别注意：每次调用 Vue.extend ，返回的都是一个个全新的 VueComponent

4. 关于 this 的执行：

   - 组件配置中：data 函数、methods 中的函数、watch 中的函数，computed 中的函数，他们的this 均是【VueComponent实例对象】
   - .new Vue() 配置中：data 函数、methods 中的函数、watch 中的函数，computed 中的函数，他们的this 均是【Vue 实例对象】

5. VueComponent的实例对象，以后简称 vc （也可称之为：组件实例对象）

   Vue的实例对象，以后简称 vm





## 原型对象

```js
//定义一个构造函数
function Demo(){
	this.a = 1;
	this.b = 1;
}

//创建一个 Demo 的实例对象
const d = new Demo()

console.log(Demo.prototype)	//显示原型属性
console.log(d.__proto__) 	//隐式原型属性
```

> 1. 一个内置关系：VueComponent.prototype.__proto__ === Vue.prototype
> 2. 让组件实例对象（vc）可以访问到 Vue 中的属性和方法





## [单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)

`XXX.vue`



## Vue CLI

### 脚手架文件结构

```markdown
├── node_modules 
├── public 
│ 		├── favicon.ico: 页签图标 
│ 		└── index.html: 主页面 
├── src 
│ 	  ├── assets: 存放静态资源 
│ 	  │ 	└── logo.png 
│ 	  │── component: 存放组件 
│ 	  │ 	└── HelloWorld.vue 
│ 	  │── App.vue: 汇总所有组件 
│ 	  │── main.js: 入口文件 
├── .gitignore: git 版本管制忽略的配置 
├── babel.config.js: babel 的配置文件 
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件 
├── package-lock.json：包版本控制文件
```



### 不同版本的vue

vue.js 和 vue.runtime.xxx.js 的区别

1. vue.js 是完整版的 vue，包含：核心功能+模板解析器
2. vue.runtime.xxx.js 是运行版的 Vue ，只包含核心功能，没有模板解析器（无法使用 template 配置项，需要使用 [`render`]([render](https://cn.vuejs.org/v2/api/#render))

> ([render](https://cn.vuejs.org/v2/api/#render))
>
> 1. 是一个函数，需要一个返回值
>
> 2. ```js
>    render(createElement){
>    	return createElement(App)
>    }
>    ```

### [修改默认配置](https://cli.vuejs.org/zh/config/#vue-config-js)

1. 使用 `vue inspect > output.js` 可以查看到 Vue 脚手架的默认配置
2. 使用 [vue.config.js](https://cli.vuejs.org/zh/config/#vue-config-js) 可以对脚手架进行个性化定制

> 语法检查(添加在vue.config.js)： [lintOnSave](https://cli.vuejs.org/zh/config/#lintonsave)
>
> ```js
> module.exports = {
> 	pages: {
> 		...
> 	},
> 	lintOnSave: false,	//关闭语法检查
>     ....
> }
> ```
>
> 



## ref 和 props 配置

### ref 

1. **作用：**用于给节点打标识 

   > - 被用来给元素或子组件注册引用信息（id 的替代者）
   > - 应用在 html 标签上获取的是真实 DOM 元素，应用在组件标签上是组件实例对象（vc）

2. **读取方式：**this.$refs.xxxxxx 

   > 1. ```
   >    <h1 ref="xxx"> </h1>
   >    ```
   >
   > 2. ```
   >    <School ref="xxx"></School>
   >    ```



### [props](https://cn.vuejs.org/v2/api/#props)

**作用：**用于父组件给子组件传递数据 

- 传递数据： <Demo name="xxx">

- 接受数据：

  1. 读取方式一: 只指定名称

     ```vue
     props: ['name', 'age', 'setName'] 
     ```

  2. 读取方式二: 指定名称和类型 

     ```vue
     props: {
         name: String, 
         age: Number, 
         setNmae: Function 
     } 
     ```

  3. 读取方式三: 指定名称/类型/必要性/默认值

     ```vue
     props: {
     	name: {
             type: String, 
             required: true, 
             default:xxx
     	}, 
     }
     ```

备注：

> props 是只读的， Vue 底层会检测你对props 的修改，如果进行了修改，若业务需求确实需要修改，那么就复制 props 的内容到 data 中一份，然后修改 data 中的数据，如下
>
> ```html
> <h2>{{myName}}</h2>
> <button @click="changeName">修改name</button>
> ```
>
> ```vue
> data(){
> 	myName: this.name
> },
> props: ['name'],
> methods:{
> 	changeName(){
> 		this.myName = '张三'
> 	}
> }
> ```





# [混入：mixin](https://cn.vuejs.org/v2/guide/mixins.html)

功能：把多个组件共用的配置提取成一个混入对象

mixin.js

```js
export const mixin1 = {
    methods:{
        showName(){
            alert(this.name);
        }
    }
}
export const mixin2 = {
    data(){
        return {
            x:100,
            y:200
        }
    }
}
```

全局混合：

在 main.js 中添加以下代码：

```js
import {mixin1,mixin2} from './mixin'

Vue.mixin(mixin1)
Vue.mixin(mixin2)
```

局部混合：

```javascript
// 在需要的 vue 页面 引入混合
import {mixin,mixin2} from '../mixin'
export default {
    mixins:[mixin,mixin2]

}
```

## 选项合并







# 插件

功能：用于增强 vue

本质：包含 install 方法的一个对象，install 的第一个参数是 Vue，第二个以后的参数是插件使用者传递的数据

定义插件：

```js
export.default{
	install(Vue,option){
		//添加全局过滤器
		Vue.filter(...)
		
		//添加全局指令
		Vue.directiove(...)
		
		//配置全局混入
		Vue.mixin(...)
		
		//添加实例方法
		Vue.protorype.$myMetthod = function (){...}
		Vue.prototype.$myProperty = xxxx
	}
}
```

使用插件(main.js)：

```js
import plugin from './plugin.js'

//使用插件
Vue.use(plugin)
```





# scoped样式

作用：让样式在局部生效，防止冲突（样式冲突时，按引入顺序应用样式）

写法：`<style scoped>`（公共样式不适合使用）

- <style lang= "less"></style> //能解析，但不能使用，需要下载loader

- 查看版本： `npm view XXX versions`





# 浏览器本地存储(webStorage)

### cookie

![Chrome-cookie](https://i.loli.net/2021/07/29/orNGAmhvEFYK5XO.jpg)

![其他浏览器cookie](https://i.loli.net/2021/07/29/ndADbH5ORecUEkw.jpg)

### 概念

1. 存储内容大小一般支持5MB左右（不同浏览器可能不太一样）

2. 浏览器通过 Window.localStorage 和 Window.sessionStorage 属性来实现本地存储机制

3. 相关 API

   > - xxxxxxStorage.setItem('key','value')
   > - xxxxxxStorage.getItem('key','value')      
   > - xxxxxxStorage.removeItem('key','value')
   > - xxxxxxStorage.clear()

### localStorage

> 存储的内容需要手动清除才会消失

```html
	<h2>loaclStorage</h2>
    <button onclick="saveData()">保存数据</button>
    <button onclick="readData()">读取数据</button>
    <button onclick="deleteData()">删除数据</button>
    <button onclick="deleteAllData()">清空数据</button>

    <script>
        const p ={ 
            name: '张三',
            age: 18
        }
        function saveData(){
            localStorage.setItem('msg','hello')
            localStorage.setItem('msg2',666)
            localStorage.setItem('msg','hello!!!!')
            localStorage.setItem('person',JSON.stringify(p))
        }
        function readData(){
            console.log(localStorage.getItem('msg'));
            const result = localStorage.getItem('person')
            console.log(JSON.parse(result));		// JSON.parse(null)也为null
            console.log(localStorage.getItem('msg3'));	//输出 null
        }
        function deleteData(){
            localStorage.removeItem('msg2')
        }
        function deleteAllData(){
            localStorage.clear()
        }
    </script>
```

![image-20210727101938273](https://i.loli.net/2021/07/27/yVqE6UsvoxXH3Cz.png)



### sessionStorage

> 存储的内容随着浏览器窗口的关闭而消失

### 备注

1. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。
2. ```JSON.parse(null)```的结果依然是null。



# 自定义事件

1. 一种组件间通信的方式，适用于：==子组件 -----> 父组件==

2. 使用场景：A是父组件，B是子组件，B想给A 传数据，那么就要在A 中给B绑定自定义数据（事件的回调在A中）

3. 绑定自定义事件

   - 第一种方式，在父组件中：`<Demo @atguigu="test"/>` 或 `<Demo v-on:atguigu="test"/>`

   - 第二种方式：在父组件中：

     ```
     <Demo ref="demo"/>
     ．．．．．．
     mounted(){
     	this.$ref.demo.$on('atguigu',this.test)
     }
     ```

   - 若想让自定义事件只能触发一次，可以使用`once`修饰符，或`$once`方法

4. 触发自定义事件：**this**.$emit('**atguigu**', 数据)

5. 解绑自定义事件：this.$off('atguigu')

6. 组件也可以绑定原生DOM事件，需要使用native 修饰符

7. 注意：通过 `this.$refs.xxx.$on('atguigu',回调)`绑定自定义事件时，回调==要么配置在methods，要么用箭头函数==，否则 this 指向出问题！！



# 全局事件-GlobalEventBus

> 一种组件间通信的方式，适用于任意组件间通信

Vue 原型对象上包含事件处理的方法 

> 1. $on(eventName, listener): 绑定自定义事件监听 
> 2. $emit(eventName, data): 分发自定义事件 
> 3. $off(eventName): 解绑自定义事件监听 
> 4. $once(eventName, listener): 绑定事件监听, 但只能处理一次 
>

所有组件实例对象的原型对象的原型对象就是 Vue 的原型对象

1. 所有组件对象都能看到 Vue 原型对象上的属性和方法 

2. `Vue.prototype.$bus = new Vue()`, 所有的组件对象都能看到$​bus 这个属性 对象 

安装全局事件总线

全局事件总线 

1. 包含事件处理相关方法的对象(只有一个) 
2. 所有的组件都可以得到

main.js：

```js
new Vue({ 
	......
	beforeCreate () { // 尽量早的执行挂载全局事件总线对象的操作
		Vue.prototype.$bus = this	//安装全局事件总线，$bus 就是当前应用的 vm
	}, 
	......
}).$mount('#root')
```

使用事件总线

1. 接受数据，A组件想接受数据，则在A组件中给 $bus 绑定自定义事件，事件的回调留在 A 组件自身

   ```js
   methods(){
   	demo(data){......}
   }
   ......
   mounted(){
   	this.$bus.$on('xxx',this.demo)
   }
   ```

2. 提供数据：`this.$bus.$emit('xxx',数据)`

最好在 beforeDestroy 钩子中，用$soff 去解绑当前组件所用到的事件

```js
this.$globalEventBus.$off('deleteTodo')
```





# 消息订阅与发布

1.  这种方式的思想与全局事件总线很相似 

   > 一种组件间通信的方式，适用于任意组件间通信

2. 它包含以下操作: 

   - 订阅消息 --对应绑定事件监听 
   - 发布消息 --分发事件 
   - 取消消息订阅 --解绑事件监听 

3. 需要引入一个消息订阅与发布的第三方实现库: **PubSubJS**

### [PubSubJS](https://github.com/mroderick/PubSubJS )

> 下载安装: npm install -S pubsub-js 

相关语法 

1.  引入：import PubSub from 'pubsub-js'  

2. 接受数据，A数组想接受数据，则在A组件中订阅消息，订阅的回调留在A 组件自身

   ```js
   methods(){
   	demo(data){......}
   }
   ......
   mounted(){
   	this.pid = PubSub.subscribe(‘msgName’,this.demo) 
   }
   ```

3. 提供数据，发布消息 ：`PubSub.publish(‘msgName’, data)`

4. 取消订阅：`PubSub.unsubscribe(token)`，==最好在beforeDestroy 钩子中==



# nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。





# [过渡与动画](https://cn.vuejs.org/v2/guide/transitions.html)

> 作用：在插入、更新或移除DOM元素时，在合适的时候给元素添加样式类名

```js
export default {
    name: 'Test',
    data(){
        return {
            isShow: true
        }
    }
}
```

### 动画效果

> 1. 操作 css 的 trasition 或 animation 
>
> 2. vue 会给目标元素添加/移除特定的 class 
>
> 3. 过渡的相关类名： 
>
>    > -  xxx-enter-active: 指定显示的 transition  
>    >
>    > - xxx-leave-active: 指定隐藏的 transition 
>    >
>    > - xxx-enter/xxx-leave-to: 指定隐藏时的样式

```html
	<div>
        <button @click="isShow = !isShow">显示/隐藏</button>
        <transition appear>
            <h1 v-show="isShow">你好哇</h1>
        </transition>
    </div>
```

```css
	h1{
        background-color: pink;
    }
    .v-enter-active{
        animation: show 1s linear;
    }
    .v-leave-active {
        animation: show 1s reverse;
    }
    @keyframes show {
        from{
            transform: translateX(-100%);
        }
        to{
            transform: translateX(0px);
        }
    }
```



### 过渡效果

1. 在目标元素外包裹<transition name="xxx"> 
2. 定义 class 样式 
   - 指定过渡样式: transition 
   - 指定隐藏时的样式: opacity/其它

```html
	<div>
        <button @click="isShow = !isShow">显示/隐藏</button>
        <transition name="hello" appear>
            <h1 v-show="isShow">法外狂徒</h1>
        </transition>
    </div>
```

```css
	h1{
        background-color: pink;
        /* transition: 0.5s linear; */

    }
    /* 进入的起点,离开的终点 */
    .hello-enter,.hello-leave-to {
        transform: translateX(-100%);
    }
	/* 进入过程中 */
    .hello-enter-active,.hello-leave-active{
        transition: 0.5s linear;
    }
    /* 进入的终点,离开的起点 */
    .hello-enter-to,.hello-leave {
        transform: translateX(0);
    }
```



### 多个元素过渡

```css
	<transition-group >
		/* 以下两个元素互斥 */
    	<h1 v-show="!isShow" key="1">你好哇</h1>
    	<h1 v-show="isShow" key="2">法外狂徒</h1>
    </transition>
```



### animate动画库的使用

##### 1. 导入animate.css文件

```vue
import 'animate.css'	//先下载安装相关css
```

##### 2. animate动画使用

> 1.enter-active-class="指定进入的时候绑定的动画类名" 2.leave-active-class="指定离开的时候绑定的动画类名" 注意:如果元素默认就是显示的,那么第一次不会触发动画,如果想第一次就触发动画.可以再添加一个appear属性

```
<transition 
	enter-active-class="animate__fadeInRight"
	leave-active-class="animate__fadeOutRight"
    appear
>
    <h1 v-show="flag1">动起来！</h1>
</transition>
```

##### 3. animate官网

> https://animate.style/

##### 4. mode in-out先进后出 out-in先出后进

```
<transition appear mode='out-in'>
	<!-- :is后面跟的是变量,通过变量来指定组件 -->
	<component :is="jilin"></component>
</transition>
```







# 配置代理

![image-20210727224722796](https://i.loli.net/2021/07/27/gLhc2IpjD5nFWfa.png)

> 使用 `node server1`  `node server2` 开启服务器

发送ajax请求的库：

1. xhr

2. jQuery

3. axios⭐

4. fetch（与xhr平级）

5. vue-resource（vue1.0使用较多,**官方已不维护**）

   > 1. 安装（npm i vue-resource）
   >
   > 2. 引入（main.js）
   >
   >    ```js
   >    import vueResource from 'vue-resource'
   >    
   >    Vue.use(vueResource)
   >    ```
   >
   > 3. 使用
   >
   >    ```
   >    axios.get ----->  this.$http.get
   >    ```
   >
   >    

跨域（协议名、端口号、主机名不一致）——如下报错：

![image-20210727230138863](https://i.loli.net/2021/07/27/2EdAbiNx6HPT9gz.png)

解决方法：

1. cors

2. jsonp

3. 代理服务器⭐

   ![web_proxy](https://st.imququ.com/i/webp/static/uploads/2015/11/web_proxy.png.webp)

   > 实现工具：
   >
   > - ngnix
   > - [vue-cli](https://cli.vuejs.org/zh/config/#devserver-proxy)

### vue脚手架配置代理

```html
  <div id="app">
    <button @click="getStudent">获取学生信息</button>
  </div>
```

`vue.config.js` 中的[ devServer.proxy](https://cli.vuejs.org/zh/config/#devserver-proxy) 选项来配置。

方法一：

```js
module.exports = {
  devServer: {
    proxy: 'http://localhost:4000'
  }
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么请求会转发给服务器（优先匹配前端资源）

方式二：

app.vue的相关写法：

```js
import axios from 'axios'

export default {
  name: 'App',
  methods:{
    getStudent(){
      axios.get('http://localhost:8080/api/students').then(
        response => {
          console.log('请求成功了',response.data);
        },
        error => {
          console.log('请求失败了',error.message);
        }
      )
    }
  }
}
```

vue.config.js：

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {		//匹配所有以 '/api' 开头的请求路径
        target: 'http://localhost:5000',	//代理目标的基本路径
        pathRewrite: {'^/api': ''},
        ws: true,
        changeOrigin: true
      },
      '/foo': {
        target: '<other_url>'
      }
    }
  }
}
```

> - changeOrigin 为 true（默认值） 时，服务器收到的请求头中的host ，localhost：5000
>
> - changeOrigin 为 false 时，服务器收到的请求头中的host ，localhost：8080

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理
2. 缺点：配置略微繁琐，请求资源时必须加前缀



# slot 插槽

1. 作用：让父组件可以向子组件指定位置插入 ==html 结构==，也是一种组件间通信的方式，适用于 **`父组件 ===>  子组件`**

2. 分类：默认插槽、具名插槽、作用域插槽

3. 使用方式：

   ​	![image-20210728133055085](https://i.loli.net/2021/07/28/g2s5w4h3QyxL7WC.png)

   1. 默认插槽

      父组件(App.vue)：

      ```vue
      <Category>
          <div>html 结构</div>
      </Category>
      ```

      子组件(Category.vue)

      ```vue
      <template>
      	<div>
      		<!-- 定义一个插槽） -->
      		<slot>插槽默认内容，当使用者没有传递具体结构时，我会出现</slot>
      	</div>
      </template>
      ```

   2. 具名插槽

      父组件：

      ```vue
      <Category>
          <template slot="center">
          	<div>html 结构</div>
          </template>
          
          <template v-slot:"footer">
          	<div>html 结构</div>
          </template>
      </Category>
      ```

      子组件：

      ```vue
      <template>
      	<div>
      		<!-- 定义一个插槽） -->
      		<slot name="center">插槽默认内容</slot>
      		<slot name="footer">插槽默认内容</slot>
      	</div>
      </template>
      ```

   3. 作用域插槽

      > 数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。
      >
      > ag：game数据在 Category 组件中，但使用数据所遍历出来的结构由App 组件决定

      父组件：

      ```vue
      <Category>
          <template scope=“scopeData>
          	<!-- 生成的是ul列表 -->
              <ul>
                  <li v-for="g in scopeData.games" :key="g">{{g}}</li>
              </ul>
          </template>
      </Category>
      <Category>
          <template scope=“scopeData>
          	<!-- 生成的是h4标题 -->
              <h4  v-for="g in scopeData.games" :key="g">{{g}}</h4>
          </template>
      </Category>
      ```

      子组件：

      ```vue
      <template>
      	<div>
      		<slot :games="games"></slot>
      	</div>
      </template>
      
      <script>
      	export default {
      		name:'Category',
      		props:['title'],
      		data() {
      			return {
      				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
      			}
      		},
      	}
      </script>
      ```

      



# [Vuex](https://vuex.vuejs.org/zh/)

github地址：https://github.com/vuejs/vuex

## 概念

### 全局事件总线

<img src="https://i.loli.net/2021/07/28/2fBbPXHkYyv4AV6.png" alt="img" style="zoom: 67%;" />

### Vuex实现

专门在 Vue 中实现集中式状态（数据）管理的一个 Vue 插件，对 vue 应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

> 何时使用？——多个组件需要共享数据时

![img](https://i.loli.net/2021/07/28/pCgDQEBU7RPNrdh.png)



## 工作原理

![](https://i.loli.net/2021/07/28/FzwYnZUTfvQ8qpC.png)

## 环境搭建

1. 安装 vuex

   ```vue
   npm i vuex
   ```

2. 引用(main.js)

   ```vue
   import Vuex from 'vuex'
   
   Vue.use(Vuex)
   ```

3. Vuex 环境搭建

   1. 创建文件：`src/store/index.js`

   ```js
   //该文件用于创建Vuex中最为核心的store
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //应用Vuex插件,因为在main.js中首先执行import
   Vue.use(Vuex)
   
   //准备actions——用于响应组件中的动作
   const actions = {}
   //准备mutations——用于操作数据（state）
   const mutations = {}
   //准备state——用于存储数据
   const state ={}
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

   2. 在 `main.js` 中创建 vm 传入 ==store== 配置项

   ```js
   ......
   //引入store
   import store from './store'
   ......
   
   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

## 基本使用

1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)
   
   const actions = {
       //响应组件中加的动作
   	jia(context,value){
   		// console.log('actions中的jia被调用了',miniStore,value)
   		context.commit('JIA',value)
   	},
   }
   
   const mutations = {
       //执行加
   	JIA(state,value){
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }
   
   //初始化数据
   const state = {
      sum:0
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取vuex中的数据：```$store.state.sum```

3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

   >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```

**vue的开发者工具**：

![image-20210728170803374](https://i.loli.net/2021/07/28/Z71IHYVNqW5RBOs.png)



## vuex 核心概念和 API

### **state** 

1. vuex 管理的状态对象 

2. 它应该是唯一的

3. 配置如下：

   ```js
   const state = {
   	XXX: initValue
   }
   ```

### actions

1. 值为一个对象，包含多个响应用户动作的回调函数  

2. 通过 commit( )来触发 mutation 中函数的调用, 间接更新 state

3. 如何触发 actions 中的回调？ 在组件中使用: $store.dispatch('对应的 action 回 

4. 可以包含异步代码（定时器, ajax 等等） 

5. 配置如下：

   ```js
   const actions = {
   	zzz({commit,state},data1){
   		commit('YYY',{data1})
   	}
   }
   ```

### mutations 

1. 值是一个对象，包含多个直接更新 state 的方法 

2. 谁能调用 mutations 中的方法？如何调用？ 

> 在 action 中使用：`commit('对应的 mutations 方法名')` 触发 

3. mutations 中方法的特点：不能写异步代码、只能单纯的操作 state 

4. 配置如下：

   ```js
   const mutations = {
   	YYY(state,value){
   		//更新 state 的某个属性
   	},
   }
   ```

### getters

> 当 state 的数据需要经过加工后在使用，可以使用 getter 加工
>
> 值为一个对象，包含多个用于返回数据的函数

1. 在```store.js```中追加```getters```配置

```js
......
const getters ={
	xxx(state){
		return state.sum * 10
	}
}

//创建并暴露store
expore default new Vuex.Store({
	......
	getters
})
```

2. 如何使用（组件中读取数据）？—— `$store.getters.xxx`

### modules

1. 包含多个 module 
2. 一个 module 是一个 store 的配置对象 
3. 与一个组件（包含有共享数据）对应 



## 四个 map 方法的使用

引入：`import { mapState,mapGetter,mapActions,mapMutations } from 'vuex'`

#### mapState/mapGetter

1. ==mapState==方法：用于帮助我们映射 state 中的数据为计算属性

   ```js
   computed:{
   	//对象写法：借助 mapState 生成计算属性，sum、school、subject
   	...mapState({sum:'sum',school:'school',subject:'subject'})
   	//数组写法：用于帮助我们映射 getter 中的数据为计算属性
   	...mapState(['sum','school','subject'])
   }
   ```

2. ==mapGetter==方法：用于帮助我们映射 getter 中的数据为计算属性

   ```js
   computed:{
   	//对象写法：借助 mapGetter 生成计算属性：xxx
   	...mapGetter({xxx:'xxx'})
   	//数组写法：借助 mapGetter 生成计算属性：xxx
   	...mapGetter(['xxx'])
   }
   ```

#### mapActions/ mapMutations

```vue
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
```

> 备注：mapActions 与 mapMutations 使用时，若需要传递参数，在模板中绑定事件时传递好参数，否则参数是事件对象

1. ==mapActions==：用于帮助我们生成与 actions 对话的方法，即：包含`$store.dispatch(xxx)` 的函数

   ```js
   methods{
   	//对象形式：靠 mapActions 生成
   	...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   	//数组形式
   	...mapActions(['jiaOdd','jiaWait'])
   }
   ```

2. ==mapMutations==方法：用于帮助我们生成与 mutations 对话的方法，即：包含：`$store.commit(xxx)` 的函数

   ```js
   methods:{
   	//对象形式
   	...mapMutations({increment:'JIA',decrement:'JIAN'}),
   	//数组形式
   	...mapMutations(['JIA',"JIAN"])
   }
   ```

   

## 模块化+命名空间

> 目的：让代码更好维修，让多种数据分类更加明确

1. 修改 store.js：

   ```js
   const countAbout = {
       //命名空间开启
       namespcaed:true,
   	state: {x:1},
   	mutations:{...},
   	actions:{...},
   	getters:{
   		bigSum(state){
   			return state.sum * 10
   		}
   	}
   }
   
   const personAbout ={
       namespaced:true		//命名空间开启
   	state: {...},
   	mutations: {...},
   	actiosn:{...}
   }
   
   const store = new Vuex.Store({
   	modules{
   		countAbout,
   		personAbout
   	}
   })
   ```

2. 开启命名空间，组件中读取state数据：

   ```js
   //方式一：自己读取
   this.$store.state.personAbout.list
   //方式二：借助 mapState读取
   ...mapStates('countAbout',['sum','school','subject'])
   ```

3. 开启命名空间，组件读取getter数据：

   ```js
   //方式一：自己读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助 mapGetters 读取
   ...mapGetters('countAbout',['bigSum'])
   ```

4. 开启命名空间，组件中调用dispatch 

   ```js
   //方式一：自己直接 dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions
   ...mapActiosn('countAbput',({incrementOdd:'jiaOdd',incrementWait:'jiaWait'}))
   ```

5. 开启命名空间后，组件中调用 commit

   ```js
   //方式一：自己直接 commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助 mapMutations
   ...mapMutations('countAbout',({increment:'JIA',decrement:'JIAN'}))
   ```



# vue-router 

## 理解 

vue-router是vue 的一个插件库，专门用来实现 SPA 应用

#### SPA 应用的理解 

1. 单页 Web 应用（single page web application，SPA）。 
2. 整个应用只有**一个完整的页面**。 
3. 点击页面中的导航链接**不会刷新**页面，只会做页面的**局部更新。** 
4. 数据需要通过 ajax 请求获取



## 路由

> 1. 一个路由（route）就是一组映射关系（key - value） ，多个路由需要路由器（router）进行管理
> 2. key 为路径, value 可能是 function 或 component 

### 路由分类 

后端路由： 

1. 理解：value 是 function, 用于处理客户端提交的请求。 
2. 工作过程：服务器接收到一个请求时, 根据**请求路径**找到匹配的**函数** 来处理请求, 返回响应数据。 

前端路由： 

1. 理解：value 是 component，用于展示页面内容。 

2. 工作过程：当浏览器的路径改变时, 对应的组件就会显示。

   ![img](https://i.loli.net/2021/07/28/DmEP1C7sBeGQySh.png)

### 基本使用

1. 安装 vue-router

   ```npm
   npm i vue-router
   ```

2. 应用插件

   ```vue
   import VueRouter from ’vue-router
   
   Vue.use(VueRouter)
   ```

3. 编写 router 配置项（路径：src/router/index.js）

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入路由组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建 router 实例对象，去管理路由规则
   export default new VueRouter({
   	routes:[
   		{
   			path:'/about',
   			compontent:About
   		},
   		{
   			path:'/home',
   			compontent:Home
   		}
   	]
   })
   ```

4. 实现切换（active-class可配置高亮样式）

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```vue
   <router-view></router-view>
   ```

### 几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。



### 嵌套路由（多级路由）

1. 配置路由规则，使用children配置项：

   ```js
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```vue
   <router-link to="/home/news">News</router-link>
   ```



### 路由传参

#### 路由的query参数

1. 传递参数

   ```vue
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="`/home/message/detail?id=${item.id}&title=${item.title}`">跳转</router-link>
   				
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link 
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		   id:item.id,
              title:item.name
   		}
   	}"
   >
       跳转
   </router-link>
   ```

2. 接收参数：

   ```js
   $route.query.id
   $route.query.title
   ```

#### 路由的params参数

1. 配置路由，声明接收params参数

   ```js
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```vue
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！

3. 接收参数：

   ```js
   $route.params.id
   $route.params.title
   ```



### 命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                          name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```vue
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>
      
      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>
      
      <!--简化写法配合传递参数 -->
      <router-link 
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
                  title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```





### 路由的props配置

作用：让路由组件更方便的收到参数

组件内写入：

```
props: ['id',''title']
```

index.js：

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props($route){
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```



### $router对象

> $router对象是全局路由的实例，是router构造方法的实例。

##### push（默认）

push方法其实和<router-link :to="...">是等同的。

> 注意：push方法的跳转会向 history 栈添加一个新的记录，当我们点击浏览器的返回按钮时可以看到之前的页面。

```js
// 1. 字符串
this.$router.push('home')

// 2. 对象
this.$router.push({path:'home'})

// 3. 命名的路由
this.$router.push({name:'user',params:{userId:123}})

// 4.带查询参数，变成 
/register?plan=123this.$router.push({path:'register',query:{plan:'123'}})
```

##### go

>  页面路由跳转 ——前进或者后退

```
this.$router.go(-1) // 后退
```

##### replace

> 作用：控制路由跳转时操作浏览器历史记录的模式
>
> - push方法会向 history 栈添加一个新的记录，而replace方法是替换当前的页面，不会向 history 栈添加一个新的记录，一般使用replace来做404页面

- 如何开启```replace```模式：```<router-link replace .......>News</router-link>```

```js
this.$router.replace('/')
//配置路由时path有时候会加 '/' 有时候不加,以'/'开头的会被当作根路径，就不会一直嵌套之前的路径。
```



#### 区别

> #### $router
>
> $router是去全局的一个路由实例(全局变量),
>
> 1. `this.$router.push({path: '/login'}); // 路由跳转, 向 history 中增加一条记录`
> 2. `this.$router.go(-1); // 路由前进(正数)或者后退(负数), 0刷新当前页面`
> 3. `this.$router.replace({path: '/login'}); // 在 history记录中替换当前路径, 不记录.`
>
> #### $route
>
> $router是一个跳转的路由对象(局部变量), 每一个路由都有自己的route, route中记录了当前路由的跳转的name, path, params, query; 获取的时候, `this.$route.path, this.$route.query`



### 编程式路由导航

1. 作用：不借助`<router-link> ——> <a>`实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
   this.$router.push({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   
   this.$router.replace({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go(number) //可前进 number 步也可后退 number 步
   ```



### 缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```vue
   //缓存多个路由组件
   <keep-alive :inclide="['News','Message']"></keep-alive>
   //缓存一个路由组件
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   ```



### 两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. ```activated```路由组件被激活时触发。
   2. ```deactivated```路由组件失活时（切换页面）触发。



### 路由守卫

> 在 src/router/index.js

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫:

   ```js
   
   ...
   {
   	path:'/About',
   	computent:About,
   	meta:{	
           isAuth: true,
           title:'关于'
       }
   }
   ...
   
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   ```

4. 独享守卫:

   ```js
   {
   	path:'/About',
   	computent:About,
   	beforeEnter(to,from,next){
           console.log('beforeEnter',to,from)
           if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
               if(localStorage.getItem('school') === 'atguigu'){
                   next()
               }else{
                   alert('暂无权限查看')
                   // next({name:'guanyu'})
               }
           }else{
               next()
           }
       }
   }
   
   ```

5. ==组件==内守卫（==About.vue==）：

   ```js
   //进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {
   },
   //离开守卫：通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {
   }
   ```



### 路由器的两种工作模式

1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。

2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。

3. hash模式(默认）：

   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。

4. history模式：

   ```
   mode:'history'
   ```

   1. 地址干净，美观 。

   2. 兼容性和hash模式相比略差。

   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

   4. 解决刷新办法（后端）：

      > 1. nodeJs的解决办法：[connect-history-api-fallback](https://www.npmjs.com/package/connect-history-api-fallback)
      > 2. nginx

5. 项目打包：

> build：将vue 文件打包
>
> ```
> npm run build
> ```

微型服务器

1. 创建一个文件夹 ：demo

2. 进入vscode 终端，输入以下命令：

   ```
   npm init 
   npm i express
   node server
   ```

3. ![image-20210729171142684](https://i.loli.net/2021/07/29/U8yxd7bJmQoO1iu.png)







# Vue UI组件库

### 移动端常见 UI 组件库

NutUI

[Vant](https://gitee.com/amateur_gang/vant#https://vant-contrib.gitee.io/vant)

[Cube UI](https://gitee.com/mirrors/cube-ui#https://didi.github.io/cube-ui/#/zh-CN/docs)

Mint UI



### PC端常见 UI组件库

[Element UI](https://element.eleme.cn/#/zh-CN)

[IView UI](https://gitee.com/icarusion/iview?_from=gitee_search#https://www.iviewui.com)



