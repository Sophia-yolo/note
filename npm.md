# 全称：Node Package Manager

> Node包管理工具

![image-20210407193138099](https://i.loli.net/2021/07/26/AI7ShHKcXd1eWxy.png)



# npm 的使用

**变量：**

- <name>|<pkg> 模块名
- <version> 版本号
- <version range> 版本范围
- <@scope> 作用域。所有 npm 软件包都有一个名称。某些软件包名称也有作用域。

## 常用命令

> 1. npm init		//在项目中引导创建一个package.json文件
> 2. npm search mkdir    //寻找包使用
> 3. npm search命令npm help //查看某条命令的详细帮助 
> 4. npm root //查看包的安装路径
> 5. npm config //管理npm的配置路径
> 6. npm prefix -g   //查看全局安装的包位置  -g全局
> 7. npm cache  //管理模块的缓存 ,可以使用下面命令，偶尔清楚一下缓存：      eg: npm cache clean
> 8. npm info webpack   //查看webpack 版本信息
> 9. npm update   // 更新模块   npm update underscore
> 10. npm outdated  //检查模块是否已经过时
> 11. npm ls   //查看安装的模块 
> 12. npm list  //可以查看全局路径下的所有包    
>                       eg:   npm list --global
>     	          //也可以使用--depth=0来缩短返回的结果  
>                        eg:     npm list -g --depth=0
> 13. npm stop  //停止模块
> 14. npm restart  //重新启动模块
> 15. npm test //测试模块 
> 16. npm version //查看模块版本
> 17. npm publish //发布模块



简写:

> ​	npm i – 安装包
> ​	npm i -g – 安装包到全局下
> ​	npm un – 删除本地下包
> ​	npm up – 更新包
> ​	npm t – 运行测试
> ​	npm ls – 罗列已经安装包
> ​	npm ll or npm la – 罗列包时显示额外信息

    npm i express momemt lodash mongoose  webpack   //也可以一次安装多个包



基本命令：

```text
# 查看 npm 命令列表
$ npm help

# 查看各个命令的简单用法
$ npm -l

# 查看 npm 的版本
$ npm -v

# 查看 npm 的配置
$ npm config list -l

```



## npm init 

> 初始化 package.json 文件

如果使用了`-f`（代表`force`）、`-y`（代表`yes`），则跳过提问阶段，直接生成一个新的`package.json`文件。

package.json 好处：

> 1.  以json文件格式定义项目所依赖的包；
>
> 2. 确定每个包的使用版本；
>
> 3. 项目构建可重复，多人协助公用一套基础代码；
>
> 4. npm init 初始化 【必须含有的两个：name 和 version】
>
>    ```json
>     {
>         "name": "react-redux-webpack",
>         "version": "1.1.0",
>      }
>    ```



## npm 包环境

### devDependencies 

> 发环境和测试环境所依赖的包列表

**运行时依赖**，在我们开发的时候会用到的一些包，只是在开发环境中需要用到，但是在别人引用我们包的时候，不会用到这些内容，放在 devDependencies 的包，在别人引用的时候不会被 npm 下载。

#### dependencies 

> 在生产环境使用的依赖包列表

是npm 核心一项内容，**开发时依赖**，依赖管理，这个对象里面的内容就是我们这个项目所依赖的 js 模块包。常见的例如react jquery等，即及时项目打包好了、上线了， 这些也是需要用的，否则程序无法正常执行。 



##  npm install

> 1. 寻找包版本信息文件（packag.json），依照他来进行安装
> 2. 查 package.json 中的依赖，并检查项目中的其他版本信息文件
> 3. 如果发现了新包，就更新版本信息文件

每个模块可以“全局安装”，也可以“本地安装”。

1. “全局安装”指的是将一个模块安装到系统目录中，各个项目都可以调用。一般来说，全局安装只适用于工具模块，比如`eslint`和`gulp`。
2. “本地安装”指的是将一个模块下载到当前项目的`node_modules`子目录，然后只有在项目目录之中，才能调用这个模块

```text
# 读取package.json里面的配置单安装  
$ npm install 
//可简写成 npm i

# 通过Github代码库地址安装
$ npm install <tarball url>
//eg:npm install git://github.com/package/path.git

# 强制重新安装
$ npm install <packageName> --force

# 如果你希望，所有模块都要强制重新安装，那就删除node_modules目录，重新执行npm install
$ rm -rf node_modules
$ npm install
```

#### 安装不同版本

install 命令总是安装模块的最新版本，如果要安装模块的特定版本，可以在模块名后面加上 @ 和版本号。

```text
$ npm install sax@latest / npm install sax
$ npm install sax@0.1.1
$ npm install sax@">=0.1.0 <0.2.0"
```

install 命令可以使用不同参数，指定所安装的模块属于哪一种性质的依赖关系，即出现在 packages.json 文件的哪一项中。

包（package)和模块（module）

包：package.json 文件所描述的文件夹或者文件，符合CommonJS规范

模块：任何被node.js中的`require`所载入的文件

> **–save：模块名将被添加到 dependencies，可以简化为参数-S。
> –save-dev：模块名将被添加到 devDependencies，可以简化为参数-D。**

```text
$ npm install sax --save
$ npm install node-tap --save-dev
# 或者
$ npm install sax -S
$ npm install node-tap -D
```



## npm uninstall

npm uninstall命令，卸载已安装的模块

```text
#卸载当前项目或全局模块 
$ npm uninstall <name> [-g] 

eg: npm uninstall gulp --save-dev  
    npm i gulp -g

卸载后，你可以到 /node\_modules/ 目录下查看包是否还存在，或者使用以下命令查看：
npm ls 查看安装的模块
```



## npm set 设置环境变量

```text
  $ npm set init-author-name 'Your name'
  $ npm set init-author-email 'Your email'
  $ npm set init-author-url 'http://yourdomain.com'
  $ npm set init-license 'MIT'
```

上面命令等于为`npm init`设置了默认值，以后执行`npm init`的时候，`package.json`的作者姓名、邮件、主页、许可证字段就会自动写入预设的值。这些信息会存放在用户主目录的`~/.npmrc`文件，使得用户不用每个项目都输入。

如果某个项目有不同的设置，可以针对该项目运行`npm config`。

```text
$ npm set save-exact true
```

上面命令设置加入模块时，`package.json`将记录模块的确切版本，而不是一个可选的版本范围。



## npm config

```text
$ npm config set prefix $dir
```

上面的命令将指定的`$dir`目录，设为模块的全局安装目录。如果当前有这个目录的写权限，那么运行`npm install`的时候，就不再需要`sudo`命令授权了。

```text
$ npm config set save-prefix ~
```

上面的命令使得`npm install --save`和`npm install --save-dev`安装新模块时，允许的版本范围从克拉符号（^）改成波浪号（~），即从允许小版本升级，变成只允许补丁包的升级。

```text
$ npm config set init.author.name $name
$ npm config set init.author.email $email
```

上面命令指定使用`npm init`时，生成的`package.json`文件的字段默认值。



## npm info

`npm info`命令可以查看每个模块的具体信息

```text
$ npm info underscore
$ npm info underscore description
$ npm info underscore homepage
$ npm info underscore version
```



## npm search

`npm search`命令用于搜索npm仓库，它后面可以跟字符串，也可以跟正则表达式

```text
$ npm search <搜索词> [-g]
```



## npm list

```text
# 当前项目安装的所有模块
$ npm list


# 加上 global 参数，会列出全局安装的模块
$ npm list -global

#列出全局安装的模块 带上[--depth 0] 不深入到包的支点 更简洁
$ npm list -g --depth 0
```



## npm update

npm update命令可以更新本地安装的模块

```text
# 升级当前项目的指定模块
$ npm update [package name]

# 升级全局安装的模块
$ npm update -global [package name]
```

它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本较新，就会安装。

使用`-S`或`--save`参数，可以在安装的时候更新`package.json`里面模块的版本号。

注意，从`npm v2.6.1`开始，npm update只更新顶层模块，而不更新依赖的依赖，以前版本是递归更新的。如果想取到老版本的效果，要使用下面的命令。

```text
$ npm --depth 9999 update
```



## npm run

package.json 文件有一个 scripts 字段，可以用于指定脚本命令，供npm直接调用。

npm run 命令会自动在环境变量 $PATH 添加 node_modules/.bin 目录，所以 scripts 字段里面调用命令时不用加上路径，这就避免了全局安装 NPM 模块。

npm run 如果不加任何参数，直接运行，会列出 package.json 里面所有可以执行的脚本命令。

npm内置了两个命令简写，npm test 等同于执行 npm run test，npm start 等同于执行 npm run start。

```text
$ npm i eslint --save-dev
```



## npm bin

> 显示相对于当前目录的，Node 模块的可执行脚本所在的目录（即 .bin 目录）。

```node
# 项目根目录下执行
$ npm bin
./node_modules/.bin
```

## npm adduser

```text
$ npm adduser
Username: YOUR_USER_NAME
Password: YOUR_PASSWORD
Email: YOUR_EMAIL@domain.com
```



## pre- 和 post- 脚本

npm run 为每条命令提供了 pre- 和 post- 两个钩子（ hook ）。

> 以 npm run lint 为例，执行这条命令之前， npm 会先查看有没有定义 prelint 和 postlint 两个钩子，如果有的话，就会先执行 npm run prelint ，然后执行 npm run lint ，最后执行 npm run postlint 。

```json
{
 "name": "myproject",
 "devDependencies": {
   	"eslint": "latest"
   	"karma": "latest"
 },
"scripts": {
   "lint": "eslint --cache --ext .js --ext .jsx src",
   "test": "karma start --log-leve=error karma.config.js --single-run=true",
   "pretest": "npm run lint",
   "posttest": "echo 'Finished running tests'"
 }
}
```

上面代码是一个 package.json 文件的例子。如果执行 npm test，会按下面的顺序执行相应的命令。

```
pretest
test
posttest
```

如果执行过程出错，就不会执行排在后面的脚本，即如果 prelint 脚本执行出错，就不会接着执行 lint 和 postlint 脚本。



### 语义化版本

- ^version：中版本和小版本

eg：^1.0.1 - >  1.x.x

- ~version：小版本

eg：~1.0.1 -> 1.0.x

- version：特定版本



## **scripts 脚本**

可以通过 npm run script-key 来调用，例如在这个 package.json 的文件夹下使用 npm run dev 就相当于运行了 node build/dev-server.js 这一段代码。使用 scripts 的目的就是为了把一些要执行的代码合并到一起，使用 npm run 来快速的运行，方便省事。

npm run 是 npm run-script 的缩写，一般都使用前者，但是后者可以更好的反应这个命令的本质。

```js
// 脚本
"scripts": {
   "dev": "node build/dev-server.js",
   "build": "node build/build.js",
   "docs": "node build/docs.js",
   "build-docs": "npm run docs & git checkout gh-pages & xcopy /sy dist\\* . & git add . & git commit -m 'auto-pages' & git push & git checkout master",
   "build-publish": "rmdir /S /Q lib & npm run build &git add . & git commit -m auto-build & npm version patch & npm publish & git push",
   "lint": "eslint --ext .js,.vue src"
}
```

npm run 如果不加任何参数，直接运行，会列出 package.json 里面所有可以执行的脚本命令。
npm 内置了两个命令简写， npm test 等同于执行 npm run test ，npm start 等同于执行 npm run start。

```
"build": "npm run build-js && npm run build-css"
```

> **上面的写法是先运行 npm run build-js ，然后再运行 npm run build-css ，两个命令中间用 && 连接。如果希望两个命令同时平行执行，它们中间可以用 & 连接。**

写在 scripts 属性中的命令，也可以在 node_modules/.bin 目录中直接写成 bash 脚本。下面是一个 bash 脚本。

```bash
#!/bin/bash
cd site/main
browserify browser/main.js | uglifyjs -mc > static/bundle.js
```

假定上面的脚本文件名为 build.sh ，并且权限为可执行，就可以在 scripts 属性中引用该文件。

```js
"build-js": "bin/build.sh"
```