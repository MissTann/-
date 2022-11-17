# Node.js - day02

> 今天是第`2`天



## 回顾 和 目标

> 内容回顾 和 今天的学习目标

### 回顾

1. 内置模块:
   1. 不仅仅只有第一天学习的内容

2. `fs`模块
   1. `readFileSync`读取文件
   2. `writeFileSync`写入文件

3. `path`模块
   1. `path.join(__dirname,'路径1','路径2'...)`:将多个路径片段,拼接到一起
   2. 大部分时候相对路径是ok的:
      1. `终端`中,向外跳一级:**cd ../**
      2. `node 文件夹名/文件.js`-->相对路径,相对的是`小黑窗(终端)`所在的路径

4. `http`模块
   1. web服务器
   2. `serve.on('request',(request,response)=>{})`
      1. 浏览器发送请求到服务器之后,触发
      2. `request`请求
         1. 获取请求的信息
            1. `url`
            2. `method`

         2. `request` 请求报文的信息--->http模块存到了这个变量中--->给开发者

      3. `response`响应
         1. `statusCode`状态码
         2. `setHeader(key,value)`
         3. `end()`
         4. 通过这个对象,生成 -->**响应报文**

5. 自己写服务器:
   1. 不需要背下来代码
   2. 理解步骤即可




### 目标

1. **模块化**
   1. 代码-->大-->小
   2. 还可以拆分的代码--->组合起来

2. **npm**
   1. 用更优雅的方式下包
   2. 命令-->下包

3. 同源跨域
   1. 工作中,很多时候可以让**后端**来完成

# 模块化

## 模块化的概念

> 随着前端代码越来越多，如何更好的拆分，管理代码呢？这里就需要用到模块化咯
>
> [传送门：掘金前端模块化详解](https://juejin.cn/post/6844903744518389768)

**概念：**

1. 把一个大的程序拆分成`互相依赖`的若干**小文件**

2. 这些小文件还可以通过**特定的语法**组合到一起

3. 这个过程称之为**模块化**

   1. `index.html`
      1. `xxx.js`

      2. `xx.css`

4. **优点：**

   1. 更好维护
   2. 更好的复用性

5. **缺点：**

   1. 没有缺点😁

   1. 学习对应的模块化语法(目前有**2种**主流,最终会变为**一种**)

   1. 文件会很多,初期可能会出现找不到的情况

      



**分析：**

1. 功能写完只有`10`行代码，模块化没啥必要！
2. 功能写完有`100`行，或者`1000`行代码，里面有`好几段`逻辑在其他地方也要用
   1. `c+v`一把梭？
      1. **c+v**的逻辑,有一个地方需要调整
   2. 模块化！！！！
3. 逻辑都写在一起，并且越写越多

![bg2012102601](assets/bg2012102601.jpg)

4. 进行模块化之后

![bg2012102602](assets/bg2012102602.jpg)





### 模块化的概念

这一节咱们介绍了什么是模块化,他的优势会在代码逐步增多的情况下逐渐体现:

1. 所有逻辑都写在一起，是否可以实现功能？
   1. 可以--->不好维护

2. 模块化可以让代码更好维护，更好___？
   1. 复用









## 模块化的规范

> 前端发展的过程中，出现过一些不同的模块化规范咱们来**认识**一下他们,不用都掌握,重点学习其中的**2个**
>
> [传送门：前端模块化](https://juejin.cn/post/6844903576309858318)

### 前端模块化规范：

- `AMD`：--知道名字即可

  - `AMD`规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。
  - 聊到`AMD`主要指的是通过`require.js`实现的模块化
  - 项目中看到类似代码说明用的是`AMD`规范
  - 目前用的`很少`，`很少`，了解即可

  ```javascript
  // 执行基本操作
  require(["jquery","underscore"],function($,_){
    // some code here
  });
  ```

  

- `CMD`：--目前没人用了

  - CMD是另一种js模块化方案，它与AMD很类似。
  - 不同点在于：AMD 推崇依赖前置、提前执行，CMD推崇依赖就近、延迟执行。
  - 项目中看到类似代码说明用的是`CMD`规范
  - 目前用的`很少`，`很少`，`了解`即可(**sea.js**)

  ```javascript
  define(function(require, exports, module) {
      var a = require('./a'); //在需要时申明
      a.doSomething();
      if (false) {
          var b = require('./b');
          b.doSomething();
      }
  });
  ```

- `CommonJS`

  - `Node.js`是`CommonJS`规范的主要实践者
  - 咱们目前能接触到用`commonJS`规范的也就是`Node.js`

- **`ESM`**

  - 也叫做`ES6 Module`
  - **ES6** 在语言标准的层面上，实现了模块功能，逐步会成为**浏览器**和**服务器**通用的模块解决方案👍👍
  - 之后基本上所有的代码都是用这个方案！！



### 规范:

1. **规范的含义**:约定了如何**导出/导入**模块
2. **遵守**规范,需要实现**规范约定**的功能





### 模块化的规范

这一节咱们介绍了前端开发中出现过的一些不同模块化规范,咱们学习其中两个即可**CommonJS**,**ESM**

1. `Node.js`是哪个规范的主要实践者？
   1. `CommonJS`


2. `ESM`也叫做什么？
   1. ES6 Module--->之后的唯一标准



## Node.js中的模块分类

> 学习了模块化之后，咱们写的`JS`文件就有了一个更好听的名字-**模块**。而在Node.js中除了咱们**自己写**的模块,还有一些其他的**模块**



![image-20220311091033084](assets/image-20220311091033084.png)

`Node.js`中的模块主要有3个分类：

- **自定义模块**
  - NodeJS中，创建的`JS`文件都是自定义模块。（也就是处处皆模块）
- [内置模块](http://nodejs.cn/api/)（核心模块）
  - 安装Node之后，自带了很多内置模块。我们可以直接加载使用他们。
- **第三方**模块
  - 其他人编写的模块，发布到 [npm 网站](https://www.npmjs.com/) 上，我们可以下载使用。















### Node.js中的模块分类

1. Node.js中咱们自己的JS文件是什么模块？
   1. 自定义模块

2. Node.js中的模块还有哪些分类？
   1. 内置
   2. 第三方








## CommonJS模块

> `Node.js`是`CommonJS`规范的主要实践者,咱们需要如何使用呢？
>
> [传送门:Node.js-CommonJS模块](https://nodejs.org/api/modules.html)

### 模块作用域

* 在 `Node.js` 中，用户创建的每个 `.js` 文件都是**自定义模块**。

* 在自定义模块中定义的**变量、方法**等成员，只能在当前模块内被访问
* 这种模块级别的访问限制，叫做**模块作用域**。
* 正因为如此,才需要**导入/导出**





### 语法：

1. 通过**module.exports**导出(暴露)内容
   1. `module` 是Node中的一个全局对象，对象包含当前模块的详细信息。
   2. `module.exports` 是模块的出口，通俗的说，就是导出内容用的，默认值是 `{}`
2. 通过**require**加载内容
   1. `require`是`Node`中的一个全局方法,可以用来导入模块
   2. `const 结果 = require('模块路径')` 
   3. **只能**加载模块暴露的内容





### 测试:

1. 创建模块`/module/myModule.js`
2. 添加**变量**,**方法**,并通过`module.exports`**导出**
3. 通过`require`**导入**模块
4. 测试能否获取**导出**的内容







### CommonJS模块

这一节咱们学习**CommonJS**的模块化语法,核心就是**导入**和**导出**

1. `CommonJS`中**导出**模块的语法是？
   1. `module.exports`

2. `CommonJS`中加载(**导入**)模块的语法是？
   1. `require`








## 数据模块-封装

> 基于刚刚学习的知识,咱们来封装一个功能模块

### 需求:

1. 基于提供的数据实现`db`模块
   1. 调用方法,返回对应的数据
2. 数据在`02-其他资料`中

```javascript
const db = require('db.js')
db.news() // 返回新闻数据 数组
db.students() // 返回 所有的同学信息 数组
db.lucystar()// 返回随机的同学 对象 count累加,保存回数据
```



### 分析:

1. **准备**
   1. 需要导入什么?

   2. fs,path

2. **逻辑:**
   1. `news()`:绝对路径-->读取(**新闻**)->转数组->返回
   1. `students()`:绝对路径-->读取(**学员**)->转数组->返回
   1. `lucystar()`:绝对路径-->读取(**学员**)->转数组->随机->count++->返回同学->保存回去

3. **导出:**







### 数据模块-封装

这一节咱们基于提供的数据和之前作业的内容封装了一个数据模块

1. 封装的目的是?

   1. 方便复用,更好维护

2. 使用封装好的模块时是否需要看懂**源码**?

   1. 只需要知道:**方法-->功能**

   



# npm

## npm是什么？

> 开发中一般不会什么功能都自己写，如何**优雅**的下载第三方模块呢?---**npm**
>
> [传送门：如何使用npm](https://docs.npmjs.com/cli/v8/using-npm)

### 概念：

* **npm 是 管理（下载、卸载、发布）第三方模块的工具。**
* `npm`（node  package  manage）node 包 管理器。管理node包的工具。
* **包**是什么？包就是模块。（**包约等于模块**，一个包可以包括一个或多个模块）
* npm这个工具，在安装 node 的时候，就已经安装到你的计算机中了。（捆绑安装）

* 命令行中执行： `npm -v` ，如果看到**版本号**，说明安装成功了。

![npm01](assets/npm01.gif)









### npm是什么?

这一节咱们介绍了之后会经常使用的一个包管理工具-`npm`

1. `npm`是什么?
   1. node的包管理工具

   2. 前端的第三方模块.也可以用它下载

2. 输入什么命令可以确认`npm`的版本?
   1. `npm -v`












## npm基本使用

> 上一节介绍了`npm`的概念，如何使用他呢?
>
> [传送门:淘宝镜像站更换新域名啦](https://zhuanlan.zhihu.com/p/432578145)

### 基本步骤:

1. **初始化**项目
2. 下载需要的**第三方**模块



### 详细步骤：

1. 初始化命令的**两种**写法

   ```bash
   npm init -y
   # 或
   npm init
   # 然后一路回车
   ```

   **注意：**	

   1. `npm init`默认会读取文件夹名作为`项目名-package name`

   - **package name** 
     - 不能有**中文**

     - 不能有**特殊符号** 

     - 不能和需要安装的**第三方模块**同名
   - 

2. 初始化之后，会在项目目录中生成 `package.json` 的文件。

3. 初始化完毕之后就可以在**当前文件夹**安装第三方模块

   1. 为了保证安装速度，建议执行这个命令
   2. 命令的作用是切换第三方模块的下载地址为`淘宝镜像`

   ```bash
   建议在安装第三方模块之前，先执行如下命令。
   下面的命令只需要执行一次即可（不管以后重启vscode还是重启电脑，都不需要执行第二次）
   npm config set registry https://registry.npmmirror.com
   ```

4. 下载的命令

   ```bash
   # 正常的下载安装
   npm install 模块名
   
   # 简写install为i
   npm i 模块名
   
   # 一次性安装多个模块
   npm i 模块名 模块名 模块名
   # 可以通过@版本号,不设置默认是最新
   npm i 模块名@版本号
   ```

5. 卸载的命令

   ```bash
   npm uninstall 模块名
   npm un 模块名
   npm un 模块名 模块名 模块名
   ```

6. 测试`下载`和`卸载`

   1. `axios`
   1. `dayjs`

7. 观察下载之后项目中**下列文件**发生的变化

   1. `package.json`
      1. 保存下载的模块信息

   2. `package-lock.json`

   3. `node_modules`






### npm基本使用:

这一节咱们演示了npm的最常用命令,这些操作在后期会**经常出现**

1. `npm`初始化的项目名是否有要求？
   1. 不能为中文,不能有特殊符号,不能有大写字母

2. 下载模块的命令是？
   1. npm i 模块名

   2. npm i 模块名@版本号

3. 移除模块的命令是？
   1. npm un 模块名








## dayjs-基本使用

> 上一节咱们下载了`dayjs`,咱们来看看这个库的作用是什么,并且来测试一下
>
> [传送门:dayjs](https://dayjs.fenxianglu.cn/)
>
> [传送门:解析规则](https://dayjs.fenxianglu.cn/category/parse.html#%E5%AD%97%E7%AC%A6%E4%B8%B2)

### 需求:

1. 根据文档确认用法并测试使用
2. 将提供数据中的日期转为`2022-07-18 17:35:53`这种格式







### 步骤:

1. 参考**文档**,测试并使用

2. 将如下日期转为`2022-07-18 17:35:53`这种格式

   1. ```bash
      1658136953000
      1658220536000
      ```




### dayjs-基本使用

这一节咱们学习了日期格式化库-`dayjs`的基本使用:

1. 任何库的使用套路都是类似的:
   1. 基于文档的示例->**c+v**运行
   2. 根据文档,传入不同的**参数**

2. 如何进阶?
   1. 基本使用:**入门**
   2. 重度使用:**熟练-->精通**
   3. 修复**框架/库**的bug:**开源框架贡献者**
   4. 实现**框架/库**:**开源框架作者**




# 上午回顾

> 上午的重点内容有哪些呢?

1. 模块化
   1. 作用:
      1. 大的-->小的
      2. 小-->组合到一起
   2. 规范:
      1. **CommonJS**
      2. **ESM**
   3. 语法:
      1. module.exports--->导出(暴露)
      2. require()-->导入
      3. 只能在`Node.js`中
2. npm:
   1. 查看版本:`npm -v`
   2. 下包:
      1. `npm i 包名`
      2. `npm i 包名@版本号`
   3. 用包
      1. 跟着文档使用--`dayjs`
   4. 删包
      1. `npm un 包名`

3. 多行**c+v**
   1. `ctrl+d`选中相同的
   2. `ctrl+shift +左/右` 选中 单词/数字
   3. `ctrl+enter`换行





## package.json和package-lock.json的作用

> 项目中中多出来的`package.json`和`package-lock.json`的作用是什么呢？
>
> [传送门:package.json](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)
>
> [传送门:package-lock.json](https://docs.npmjs.com/cli/v8/configuring-npm/package-lock-json)
>
> [传送门:详解package.json和package-lock.json](https://juejin.cn/post/6870426598605062152)

### package.json

**保存项目的信息:**

1. `name`：项目名
2. `version`:项目版本
3. `description`：项目描述
4. `main`：项目入口
5. `scripts`:
   1. 示例中的:`test`可以通过`npm run test`执行
6. `author`:作者
7. `license`:开源协议
8. `dependencies`:项目中用到的第三方模块(依赖)

```json
{
  "name": "03",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "dayjs": "^1.11.0",
    "jquery": "^3.6.0"
  }
}

```

### package-lock.json

1. 更为详细的第三方模块模块
   1. 版本信息
   2. 甚至**下载地址**
   3. ...







### 实际应用

1. 共享的`node`项目一般会删除`node_modules`
2. 只要项目目录中有`package.json`说明项目是完整的
3. **项目根目录**,执行`npm i`即可读取`package.json`中保存的`dependencies`(**依赖信息**),重新下载
   1. 命令执行的目录和`package.json`同级













### package.json和package-lock.json的作用

1. 哪个命令会读取`package.json`中保存的依赖信息,并下载?
   1. `npm i`

2. 执行这个命令**路径是否**有要求?
   1. 和`package.json`同级





## require的加载机制

> 现在Node中的3种模块咱们都见过啦，使用`require`加载的时候遵循什么顺序呢？
>
> [传送门:require方法](https://nodejs.org/api/modules.html#requireid)
>
> [传送门:从Node_modules加载](https://nodejs.org/api/modules.html#loading-from-node_modules-folders)
>
> [传送门:require的缓存](http://nodejs.cn/api/modules.html#requirecache)

### 加载机制：

1. **缓存:**

   1. 判断缓存中有没有，如果**有**，使用缓存中的内容
   2. 缓存中没有，那么表示第一次加载，加载完会缓存

2. **是否带路径**:

   1. **有路径：**
      1. 加载自定义模块
      2. 优先加载同名文件，加载一个叫做 xx 的文件
      3. 再次加载js文件，加载 **xx.js** 文件
      4. 再次加载json文件，加载 **xx.json** 文件
      5. 如果上述文件都没有，则报错 “Cannot find module './xx'”
   2. **没有路径：**
      1. 优先加载核心模块，没有核心模块，加载第三方模块

3. **第三方模块**的查找方式：

   1. 第三方模块**命名避免和内置模块同名**

   2. 优先查找当前文件夹中的`nodu_modules`里面查找模块

   3. 找到了，读取`package.json`中`main`字段对应的文件

   4. 如果找不到，**依次逐级**的向上级目录查找第三方模块

   5. 找到最顶级位置

   6. 确认代码:

      ```javascript
      console.log(module.paths)
      ```

      


### 测试

1. **缓存**
1. **不给后缀名**
1. **第三方模块**
1. 是否和描述的一致?



### require的加载机制

1. `require`加载的模块是否会缓存
   1. 会->重复加载,没有问题

2. `require`查找第三方模块时，会找到哪个目录为止？
   1. 根目录为止







## 全局模块

> 第三方模块除了项目中直接下载使用的模块以外,还有一种叫做全局模块的,咱们来认识一下,并且安装几个试试
>
> [传送门:nrm官网](https://www.npmjs.com/package/nrm)
>
> [传送门:serve](https://www.npmjs.com/package/serve)

### 和本地模块的差异

- 全局安装的模块，不能通过 `require()` 加载使用。
- 全局安装的模块，一般都是命令或者工具。

### 安装卸载命令

- 安装命令（多一个 `-g`）

  ```bash
  npm i 模块名 -g
  # 或
  npm i -g 模块名
  
  ### mac 系统如果安装不上，使用下面的命令提高权限
  sudo npm i -g 模块名
  ```

- 卸载命令（也是多一个 `-g`）

  ```bash
  npm un 模块名 -g
  # 或者
  npm uninstall 模块名 -g
  ```

- 全局安装的模块，在系统盘（C盘）

  - 通过命令 `npm root -g` 可以查看全局安装路径

### nrm介绍

![image-20210122120308133](assets/202203291725626.png)



`nrm` 是作用是切换镜像源（模块下载地址；模块下载的网站）。

### nrm安装

1. 执行命令
   1. 不需要记忆哪些模块需要`-g`或者不需要
   2. 直接可以通过[官方文档](https://www.npmjs.com/package/nrm)确认

```bash
npm i -g nrm   （mac系统前面加 sudo）
```

2. 使用`nrm`

```bash
nrm --help   # 查看帮助
nrm ls    # 查看全部可用的镜像源
nrm test # 测试各个源的速度
nrm use taobao  # 切换到淘宝镜像
nrm use npm  # 切换到npm主站
```



### serve

1. 功能和昨天自己编写的web服务器类似
2. 参考文档**安装+使用** 
3. 分别将
   1. **clock**和**数据可视化**
   2. 通过`serve`托管并测试访问









### 常见错误及解决方案:

* `mac`安装:
  * sudo npm i -g nrm
  * 输入密码:

- 运行 `nrm ls` 或者 `nrm use taobao` 等命令，如果报错如下：

  “无法加载文件 C:......................，**因为在此系统上禁止运行脚本**。................”

  - **解决办法：**
    - `管理员`方式，打开命令行（powershell）窗口
    - 执行 `set-ExecutionPolicy RemoteSigned;` 
    - 在出现的选项中，输入 `A`，回车。即可。

- 如果报错如下: “**无法将 nrm 识别为 cmdlet、函数、脚本文件或可运行程序的名称**。xxxxxxxxxxx”

  - **解决办法:**
    - 重启vscode，win7可能要重启电脑。



### 全局模块

这一节咱们安装并使用了几个全局模块:

1. 全局模块在安装命令是?比如安装`nrm`模块
   1. `npm i nrm -g`

2. 如何确认某个模块是全局模块还是本地模块？
   1. 文档




# 写接口

> 基于目前完成的内容,来实现一个返回数据的接口,并测试调用

### 需求:

1. 请求方法统一为`get`
2. `/api/news`返回新闻数据(日期转为`2022-07-18 17:35:53`)
3. `/api/students`返回全部同学
4. `/api/lucystar`返回随机的同学



### 基础模板:

* 这部分内容直接**c+v**

```javascript
// 1. 导入 http 模块
const http = require('http')

// 2. 创建 web 服务器实例
const server = http.createServer()

// 3. 启动服务器
server.listen(8848, () => {
  console.log('my server start work')
})

// 4. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', (request, response) => {
  // 设置响应的内容为JSON
 response.setHeader('Content-Type', 'application/json; charset=utf-8')
  // 不能直接响应 对象/数组 需要转为字符串
})

```

### 分析:

1. **接收**
   1. 如何判断请求方法?`request.method`
   2. 如何判断请求地址?`request.url`
2. **响应**
   1. 如何获取对应的数据?
      1. 调用上午封装的`db`数据模块的对应方法
   2. 如何响应内容?
      1. `response.end()`
3. **逻辑:**
   1. `/api/students`
      1. 返回`db.students()`

   2. `/api/luckstar`
      1. 返回`db.lucystar()`

   3. `/api/news`
      1. 转化`dayjs(时间戳).format('YYYY-MM-DD HH:mm:ss')`






### 测试:

1. 运行本节代码
   1. `node xxx.js`

2. **网页**直接打开接口
   1. `JSON`美化需要安装插件
3. 用接口测试工具测试
4. **写个页面**来测试:
   1. **会报错**
   2. ![image-20220811170431140](assets/image-20220811170431140.png)






### 写接口

咱们是前端开发工程师,虽然这一节咱们自己实现了几个简单的接口:

1. 工作中是否需要咱们写接口?
   1. 不需要--后端

2. 本节写接口的目的是?
   1. 理解后端的接口大概的工作原理




# 同源&跨域

## 同源和同源策略

> 上一节的接口之所以调用不了,原因就是因为打开的页面和接口**不同源**,这一节咱们来介绍一下什么是**同源**,以及浏览器的**同源策略**

### 同源

同源指的是**两个URL**地址具有相同的**协议地址**、**主机名**、**端口号**。

**相对于** http://www.test.com/index.html 页面的 5 个同源检测结果：

| URL                                | 是否同源 | 原因            |
| ---------------------------------- | -------- | --------------- |
| http://www.test.com/other.html     | **同源** | 端口默认都是80  |
| https://www.test.com/about.html    | 否       | 协议不同        |
| http://blog.test.com/movie.html    | 否       | 主机不同        |
| http://www.test.com:7001/home.html | 否       | 端口不同        |
| http://www.test.com:80/main.html   | **同源** | http:不写也是80 |









### 什么是同源策略?

同源策略（英文全称 **Same origin policy**）是**浏览器**提供的一个安全功能。
浏览器的同源策略规定：不允许非同源的 URL 之间进行资源的交互。

**地址1:** 网页的URL

**地址2:**请求的资源地址(**接口地址**)

![158547242055](assets/ty-2.png)







### 同源和同源策略

这一节咱们介绍了同源和同源策略:

* 同源指的是2个地址,**协议**,**主机名**和什么都相同?
  * 端口号:
* 如果没有浏览器，还会有同源策略吗？
  * **没有-->浏览器的限制**



## 跨域及主流跨域方法

> 有了同源安全策略之后,只要2个不同源就会涉及到**跨域**

### 概念:

* 同源指的是两个 URL 的**协议、主机名、端口号**完全一致
* 反之，则是**跨域**。

* 浏览器的同源策略不允许非同源的 URL 之间进行资源的交互。例如：

- **网页**：http://www.test.com/index.html
- **接口**：http://www.api.com/userlist
- 



### 浏览器对跨域请求的拦截过程?

浏览器允许发起跨域请求。但跨域请求回来的数据，会被浏览器拦截，无法被页面获取到！示意图如下：

![158547242055](assets/ty-3.png)



### 主流跨域方法

**代理服务器** 和 **CORS** 是目前最为流行的**实现跨域数据请求**的两种技术方案。

1) **代理服务器**跨域在后面vue课程中会讲到--**Vue的第二个项目(人资)**

2) **CORS** 是跨域的主流技术解决方案

3) 还有一些其他的跨域方案---[传送门](https://juejin.cn/post/6844904126246027278)





### 跨域及主流跨域方法

这一节咱们介绍了什么是跨域以及主流的跨域方法:

1. **跨域**指的是浏览器请求**同源 or 不同源**的资源?
   1. **不同源**
2. 除了本节说明**2种**跨域方案以外还有其他的吗?
   1. 还有很多,目前主流的是这两个2



## CORS

> 接下来咱们就来介绍一下什么是`CORS`,以及在Node.js中如何使用它
>
> [传送门:CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)

#### 概念

1) `CORS` 是解决跨域数据请求的终极解决方案，全称是 `Cross-origin resource sharing`。

2) `CORS` 技术需要**浏览器**和**服务器**同时支持

- 浏览器要**支持** CORS 功能（主流的浏览器全部支持，IE 不能低于 IE10）

  - **前端开发者**什么不都需要做

- 服务器要**开启** CORS 功能（需要**后端开发者**为接口开启 CORS 功能）

  

#### 工作原理

服务器端通过 `Access-Control-Allow-Origin` 响应头，来告诉浏览器当前的 API 接口是否允许跨域请求。

![158547242055](assets/ty-4.png)

检查一下之前调用的接口是否有该**响应头:**





#### 主要优势

1) **CORS** 是真正的 Ajax 请求，支持 GET、POST、DELETE、PUT、PATCH 等这些常见的 Ajax 请求方式
2) 只需要后端开启 `CORS` 功能即可，前端的代码无须做任何改动
3) `Node.js`中可以通过设置如下的请求头**允许跨域**,添加到**响应之前**

```javascript
  // response.setHeader('Access-Control-Allow-Origin', '*')
```



### CORS

这一节咱们演示了如何使用`CORS`来实现跨域:

1. 使用`CORS`前端是否需要调整代码?
   1. 不用,一行都不用改

2. 工作中谁来处理**跨域问题**
   1. **开发**:
      1. 要么后端设置**CORS**
      2. 后端不设置,前端自己用**代理服务器跨域**
   2. **生产**(上线)
      1. 后端/运维
      2. **linux**



# 补充

## 补充-开发属于自己的包

> 咱们已经学习了如何下载第三方模块，作为作业咱们写了一个自己的模块，可以发布到网上吗？自信一些！！！
>
> [传送门:package.json说明](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)
>
> [传送门:yarn-创建一个module](https://classic.yarnpkg.com/en/docs/creating-a-package)
>
> [传送门:license许可协议说明]( https://www.jianshu.com/p/23e61804d81e)



### 规范的包结构

```
📂 - my_module
    📃 - package.json  （package.json包的配置文件）
    📃 - index.js      （入口文件）
    📃 - README.md     （说明文档）
    
```

一个规范的包结构，需要符合以下 **3 点**:

1. 以单独的目录存在
2. 顶级目录下必须包含 `package.json` 配置文件
3. package.json 中必须包含如下属性
   - `name`: 包的名字，我们使用 require()加载模块的时候，使用的就是这个名字
   - `version` 版本
   - `main` 入口文件。默认是index.js 。如果不是，需要使用main指定

**注意:**以上 3 点要求是一个规范的包结构必须遵守的格式，关于更多的约束，可以参考传送门中的网址:



### 开发属于自己的包

- 1. 初始化 `package.json`
     1. 执行命令`npm init -y`
     2. 然后根据需求调整内部属性即可
     3. **注意，JSON文件不能有注释，下面加注释，是为了理解**。

  ```json
  {
    "name": "my_module",  // 包（模块）的名字，和文件夹同名。别人加载我们的包，找的就是这个文件夹
    "version": "1.0.0",
    "description": "我开发的包哦",
    "main": "index.js", // 别人加载我们的模块用，require加载的就是这里指定的文件
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [ // 在npm网站中，通过关键字可以搜索到我们的模块，按情况设置
      "my",
      "itcast",
      "test"
    ],
    "author": "autumnfish", // 作者
    "license": "ISC" // 开源协议
  }
  ```

  

- `index.js` 中定义功能方法

  ```javascript
  
  ```

- 编写`README.md`

  - 包的使用说明文档。
  - 以`markdown`的格式把包的作用、用法、注意事项等描述清楚即可
  - 具体写什么内容，没有强制性的要求
  - 比如

  



### 格式调整

1. 将今天写的**数据模块**调整为规范格式




### 开发属于自己的包

1. `package.json`中哪个配置是模块的入口？
   1. **main**

2. `README.md`里面可以写作者的兴趣爱好吗？
   1. 写什么都可以
   2. 合法合规即可






## 补充-发布npm

> 上一节咱们已经把咱们写好的模块调整为较为规范的包的格式啦，接下来咱们把他发布到`npm`上！`(￣y▽￣)╭ Ohohoho.....`
>
> [传送门:Npm命令](https://docs.npmjs.com/cli/v8/commands)

### 步骤1 - 注册npm账号

- 访问 https://www.npmjs.com/ 网站
- 点击` sign up` 按钮，进入注册用户界面
- 填写账号相关的信息
- 点击 Create an Account 按钮，注册账号
- 注册完账号，需要到邮箱中认证一下

### 步骤2 - 连接npm

* 执行命令：登录账号

```bash
npm adduser
```

- 这个命令只需要执行一次

- 根据提示依次输入你的注册信息即可

- ![image-20200904155145641](assets/image-20200904155145641-16476779727471.png)

- 看到`Logged in as xxx`最后一行说明成功啦

- 查看用户信息可以使用如下命令

  ```bash
  npm who am i
  ```

- 登出可以使用如下命令

  ```bash
  npm logout
  ```

### 步骤3 - 确保镜像源是npm

1. 输入如下命令进行确认

```bash
# 查看当前的npm的registry配置，确保是https://registry.npmjs.org
npm config get registry

# 如果不是，可以通过如下命令来设置 或者用nrm切换
npm config set registry https://registry.npmjs.org 

```

### 步骤4 - 确保包名不重复

1. 方法1:直接去`npm`搜索
2. 方法2:通过命令查看,看到如下图内容说明不存在

```bash
npm view 包名
```

![image-20200904155558356](assets/202203291725848.png)



### 步骤5 - 发布

- 确保上述内容全部完成执行发布命令

  ```bash
   npm publish 
  ```

- 看到类似这样的内容说明发布完成

- ![image-20220319162726057](assets/202203291725058.png)

### 测试使用

1. 确保上述操作完成之后,即可下载咱们刚刚发布的模块啦

   ```bash
   npm i 模块名
   ```

2. 稍等片刻之后确认

   1. `nodule_modules`
   2. `package.json`
   3. 是否多了刚刚下载的模块
   4. 😁😁😁



### 更新:

1. 模块的目录下,执行` npm publish`
2. 版本要**+**





### 常见错误

1. 自己的模块名不能和已存在的模块名同名。（可以先去npm网站搜索是否同名）

2. `24`小时内不能重复发布

3. 新注册的账号，必须先邮箱（邮件可能是垃圾邮件）验证，然后才能发布

4. 删除已发布的包

   - 运行 `npm unpublish` 包名 --force 命令，即可从 npm 删除已发布的包。

5. **其他注意事项:**

   - npm unpublish 命令只能删除 72 小时以内发布的包

   - npm unpublish 删除的包，在 24 小时内不允许重复发布

   - 发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包!



### 发布npm

1. 如何下载咱们刚刚发布的模块？
   1. `npm i 模块名`

2. 如何使用咱们刚刚发布的模块?
   1. 照着文档用


