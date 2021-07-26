## 预习知识

1. 实例对象、函数对象

2. 回调函数

   - 同步回调：立即执行，完全执行完了才结束，不会放入回调队列中

     > 数组遍历相关的回调 / Promise的executor函数

   - 异步回调：不会立即执行，会放入回调队列中将来执行

     > 定时器回调 / `ajax`回调 / Promise成功或失败的回调

   ⭐**`js 引擎先把初始化的同步代码都执行完成后，才执行回调队列中的代码`**



## 优缺点

### 优点

1. 支持链式调用，解决回调地狱问题

2. 指定回调函数的方式更加灵活

   `promise`：构造函数

### 缺点

1. 无法取消 Promise，一旦新建它就会立即执行，无法中途取消
2. 如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。
3. 当处于 Pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。



## promise初体验

```js
var promise = new Promise(function(resolve, reject) {
    // 异步处理
    // 处理结束后、调用resolve 或 reject
});
```

```js
new promise((resolve,reject)=>{	//excutor执行器函数
    setTimeout(()=>{
        if(...) {
           resolve('成功的数据')	//resolve()函数
        }else{
            reject('失败的数据')	//reject()函数
        }
    },1000)
    }).then(
	value=>{	//onResovled()函数
        console.log(value)	//成功的数据
    }
).catch(
	reason => {	//onRejected()函数
        console.log(reason)	//失败的数据
    }
)
})
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210210134357696.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjAwOA==,size_16,color_FFFFFF,t_70)



## API

### Promise 构造函数：Promise(executor) {}

1. executor 函数：同步执行 (resolve, reject) => {}
2. resolve 函数：内部定义成功时调用的函数 resove(value)
3. reject 函数：内部定义失败时调用的函数 reject(reason)

说明：executor 是执行器，会在 Promise 内部立即同步回调，异步操作 resolve/reject 就在 executor 中执行



### Promise.prototype.then方法：链式操作——(onResolved, onRejected)=>{}

指定两个回调（成功+失败）

1. onResolved 函数：成功的回调函数 (value) => {}


1. onRejected 函数：失败的回调函数 (reason) => {}


说明：指定用于得到成功 value 的成功回调和用于得到失败 reason 的失败回调，返回一个新的 promise 对象



### Promise.prototype.catch方法：捕捉错误——(onRejected)

指定失败的回调

`onRejected` 函数：失败的回调函数 `(reason) => {}`

说明：这是`then()` 的语法糖，相当于 `then(undefined, onRejected)`



### Promise.resolve()——（value）=>{}

```js
var p = Promise.resolve('Hello');

p.then(function (s){
  console.log(s)
});
// Hello
```

1. 如果传入的参数为 非Promise类型的对象, 则返回的结果为成功promise对象
2. 如果传入的参数为 Promise 对象, 则参数的结果决定了 resolve 的结果

> value：将被 Promise 对象解析的参数，也可以是一个成功或失败的 Promise 对象



### Promise.reject()——（reason）=>{}

```js
var p = Promise.reject('出错了');

p.then(null, function (s){
  console.log(s)
});
// 出错了
```

reason：失败的原因

- Promise.resolve()/Promise.reject() 方法就是一个语法糖
- 用来快速得到Promise对象

> 说明：返回一个失败的 promise 对象



### Promise.all(iterable)

```js
var p = Promise.all([p1,p2,p3]);
```

> iterable：包含 n 个 promise 的可迭代对象，如 Array或String

说明：返回一个新的 promise，只有所有的 promise 都成功才成功，只要有一个失败了就直接失败



### Promise.race(iterable)

```js
var p = Promise.race([p1,p2,p3]);
```

> 说明：返回一个新的 promise，第一个完成的 promise 的结果状态就是最终的结果状态
>
> ​	**谁先完成就输出谁(不管是成功还是失败)**





## Promise的状态

三种状态：

- pending: 初始状态，不是成功或失败状态。
- fulfilled: 意味着操作成功完成。
- rejected: 意味着操作失败。

实例对象promise中的一个属性 `PromiseState`

1. pending 变为 resolved/ fulfilled
2. pending 变为 rejected

注意

1. 对象的状态不受外界影响
2. 只有这两种，且一个 promise 对象只能改变一次
3. 一旦状态改变，就不会再变，任何时候都可以得到这个结果——`PromiseResult`
4. 无论成功还是失败，都会有一个结果数据。成功的结果数据一般称为 value，而失败的一般称为 reason。







## 关键问题

### 改变Promise的状态

(1)`resolve(value)`：如果当前是 pending 就会变为 `resolved`

(2)`reject(reason)`：如果当前是 pending 就会变为 `rejected`

(3)抛出异常：如果当前是 `pending` 就会变为 `rejected`

⭐当 promise **改变**为对应状态时**都会调用**



### 改变 promise 状态和指定回调函数

先后顺序：常规是先指定回调再改变状态，但也可以先改状态再指定回调

- 如何先改状态再指定回调？

(1)在执行器中直接调用 `resolve()`/`reject()`

(2)延迟更长时间才调用 `then()`

```js
let p = new Promise((resolve, reject) => {
  // setTimeout(() => {
      resolve('OK');
  // }, 1000); // 有异步就先指定回调，否则先改变状态
});

p.then(value => {
  console.log(value);
},reason=>{
  
})
```

- 什么时候才能得到数据？

(1)如果先指定的回调，那当状态发生改变时，回调函数就会调用得到数据

(2)如果先改变的状态，那当指定回调时，回调函数就会调用得到数据





### promise.then() 返回的新 promise 的结果状态由什么决定？

1. 简单表达：由 `then()` 指定的回调函数执行的结果决定

2. 详细表达：

    ① 如果抛出异常，新 `promise` 变为 `rejected`，`reason` 为抛出的异常

    ② 如果返回的是非 `promise` 的任意值，新 `promise` 变为 `resolved`，`value` 为返回的值

    ③ 如果返回的是另一个新 `promise`，此 `promise` 的结果就会成为新 `promise` 的结果



## promise 串联多个操作任务

1. promise 的 then() 返回一个新的 promise ，可以并成 then()  的链式调用
2. 通过 then 的链式调用串联多个同步/异步任务

```js
let p =new Promise((resolve,reject)=>{
    resolve("ok")
})
p.then(value=>{
    return new Promise((resolve,reject)=>{
        resolve("success")
    })
}).then(value=>{
    console.log(value)		//打印 success 
}).then((value=>{
    consol.log(value)		//打印 undefined
}))
```



## Promise 异常传透

1. 当使用 promise 的 `then` 链式调用时，可以在最后指定失败的回调
2. *前面任何操作出了异常*，都会传到最后失败的回调中处理

相当于这种写法：`reason => {throw reason}`

> 所以失败的结果是一层一层处理下来的，最后传递到 catch 中。或者，将 `reason => {throw reason}` 替换为 `reason => Promise.reject(reason)` 也是一样的



## 中断 promise 链

当使用 promise 的 then 链式调用时，在中间中断，不再调用后面的回调函数

（then）办法：在回调函数中返回一个 `pending` 状态的 `promise` 对象



为了在 catch 中就中断执行，可以这样写：

```js
return new Promise(()=>{})
```

由于，返回的新的 promise 结果决定了后面 then 中的结果，所以后面的 then 中也没有结果。





> 同步任务：直接调用 resolve ， reject ， throw





## util.promisify函数

http://nodejs.cn/api/util.html



## async函数

1. 函数的返回值为 Promise 对象
2. Promise 对象的由 async 函数执行的返回值决定
   - 如果返回值是一个非 Promise 类型的数据 ==>  resolved/fulfilled 
   - 如果返回值是一个 Promise 类型的数据 ==>  同Promise





## await 表达式

1. await 右侧的表达式一般为 Promise 对象 ，但也可以是其他的值
2. 如果表达式是 Promise 对象，await 返回的是Promise成功的值
3. 如果表达式是其他值，直接将此值作为 await 的返回值



## 注意

- await 必须写在async 函数中，但在async 函数中可以没有await 
- 如果 await 的promise 失败了，就会抛出异常，需要通过 try ... catch 捕获处理
