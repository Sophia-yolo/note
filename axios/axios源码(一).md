# axios 对象创建过程

```js
function Axios(config){
            //初始化
            this.defaults = config; //为了创建 default 默认属性
            this.intercepters = {
                request:{},
                response:{}
            }
        }

        //原型添加相关方法
        Axios.prototype.request = function(config){
            console.log('发送AJAX请求，请求类型为'+ config.method)
        }

        Axios.prototype.get= function(config){
            return this.request({method:'GET'})
        }

        Axios.prototype.post = function(config){
            return this.request({method:'POST'})
        }

        //声明函数
        function createInstance(config){
            //实例化对象
            let content = new Axios(config) //content能调用原型属性：content.get()  但是不能当做函数使用
            //创建请求对象函数
            let instance = Axios.prototype.request.bind(content);//instance 是一个函数，并且可以 instance({}) 此时 instance 不能使用 instance.get
            //将 Axios.prototype 对象中的方法添加到instance函数对象中
            Object.keys(Axios.prototype).forEach(key=>{
                 instance[key] = Axios.prototype[key].bind(content)
            }) 
            Object.keys(content).forEach(key=>{
                instance[key] = content[key]
            })
            return instance
        }

        let axios = createInstance()
        //发送请求
        axios.get()
```

结果：

![image-20210713175639051](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210713175639051.png)

