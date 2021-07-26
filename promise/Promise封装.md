

# 构造函数

```js
// 声明构造函数
function Promise(executor){
	//添加属性：PromiseState、PromiseResult
	this.PromiseState = "pedding"
	this.PromiseResult = null;
	
	let that = this;
	
	// 声明一个属性
	this.callbacks = []
	
	// resolve函数
	function resolve(data){
		// 表示状态只能改变一次,判断状态
		if(that.PromiseState !== "pedding") return
		// 1. 修改对象状态
		that.PromiseState = "resolved"
		// 2. 设置对象结果值
		that.PromiseResult = data
		// 调用成功的回调函数
		setTimeout(()=>{
			that.callbacks.forEach(item =>{
				item.onResolve(data)
			})
		})
		
	}
	// reject函数
	function reject(data){
		// 表示只能改变一次,判断状态
		if(that.PromiseState !== "pedding") return
		// 1. 修改对象状态
		that.PromiseState = "rejected"
		// 2. 设置对象结果值
		that.PromiseResult = data
		// 调用失败的回调函数
		setTimeout(()=>{
			that.callbacks.forEach(item =>{
				item.onReject(data)
			})
		})
	}
	try{
		// 同步调用[执行器函数]
		executor(resolve,reject)
	}catch(e){
		reject(e)
	}
}
```





# then 方法

```js
//添加 then 方法(异步执行)
Promise.prototype.then = function(onResolved,onRejected){
	const that = this;
	// 判断回调函数参数
	if(typeof onRejected !== "function"){
		onRejected = reason => {
			throw reason
		}
	}
	if(typeof onResolved !== "function"){
		onResolved = value => value
	}
    // 满足promise对象
	return new Promise((resolve,reject) => {
		// 封装调用的回调函数
		function callback(type){
			// 捕捉异常
			try{
				// 获取回调函数的执行结果
				let result = type(that.PromiseResult);
				// 判断
				if(result instanceof Promise){
					// 如果是promise对象
					result.then(v=>{
							resolve(v)
						},r=>{
							reject(r)
						})
					}else {
						// 结果的对象状态是成功的
						resolve(result)
					}
			}catch(e){
				reject(e)
			}
		}
        //判断 Promise 对象的状态
		if(this.PromiseState == "resolved"){
            //设置定时器执行then方法的异步任务
			setTimeout(()=>{
				callback(onResolved)
			})
		}
		if(this.PromiseState == "rejected"){
			setTimeout(()=>{
				callback(onRejected)
			})
				}
		if(this.PromiseState == "pedding"){
			// 保存异步任务的回调函数
			// 执行多步回调
			this.callbacks.push({
				onResolve: function(){
					callback(onResolved)
				},
				onReject: function(){
					callback(onRejected)
				}
			})
		}
	})
}
```





# catch 方法

```js
//添加 catch 方法
Promise.prototype.catch =function(onRejected){
    //捕捉异常
	return this.then(undefined,onRejected)
}
```





# resolve 方法

```js
//添加 resolve 方法
Promise.resolve = function(value){
	// 返回 Promise 对象
	return new Promise((resolve,reject) => {
        //判断
		if(value instanceof Promise){
			value.then(v=>{
				resolve(v)
			},r=>{
				reject(r)
			})
		}else{
			//状态设置为成功
			resolve(value)
		}
	})
}
```



# reject 方法

```js
//添加 reject 方法
Promise.reject = function(reason){
	return new Promise((resolve,reject)=>{
		//无论什么情况直接调用reject函数
		reject(reason)
	})
}
```





# all 方法

```js
//添加 all 方法
Promise.all = function(promises){
	//返回的是promise对象
	return new Promise((resolve,reject)=>{
		// 声明变量
		let count = 0;
		let arr = [];
		// 遍历all中的参数
		for( let i = 0;i<promises.length;i++){
			// 判断对象状态
			promises[i].then(v=>{
				// 得知每个对象的状态是成功
				//若每个对象的状态成功则+1
				count++;
				//将成功的对象按顺序存入数组 arr 中
				arr[i] = v;
				//判断对象的状态是否和all方法中一致
				if(count == promises.length){
					//修改状态
					resolve(arr)
				}
			},r => {
				reject(r)
			})
		}
	})
}
```





# race 方法

```js
//添加 race 方法
Promise.race = function(promises){
    //返回的是 promise 对象
	return new Promise((resolve,reject) => {
		for(let i = 0; i<promises.length; i++){
			//取决于Promise对象的状态只能执行一次
			promises[i].then(v=>{
				//修改返回的对象状态为【成功】
				resolve(v)
			},r=>{
				// 修改放回的对象状态为【失败】
				reject(r)
			})
		}
	})
}
```







# Class 封装

```js
class Promise{
	// 构造方法
	constructor(executor) {
		...
        ...
		// resolve函数
	    function resolve(data){
            ...
        }
        
        // reject函数
	    function reject(data){
            ...
        }
        
        // then方法构造
		then(onResolved,onRejected){
            ...
        }
        
        // catch方法
		catch(onRejected){
            ...
        }
        
        // resolve 方法——实例对象
		static resolve(value){
            ...
        }
        
        // reject 静态方法
		static reject(reason){
            ...
        }
        
        // all 方法
		static all(promises){
            ...
        }
        
        // race 方法
		static race(promises){
            ...
        }
	}
}
```

