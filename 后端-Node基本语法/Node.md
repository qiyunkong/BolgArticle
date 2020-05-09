

# Node

## 1.Node开发概述

 1.1为什么要学习服务器端开发基础

- 能够和后端程序员更加紧密的配合
- 网站业务逻辑前置，学习前前端技术需要后端技术支撑（Ajax）
- 扩宽知识视野，能够站在更高的角度审视整个项目

1.2服务器开发要做的事情

- 现实网站业务逻辑
- 数据的增删改查

1.3为什么选择Node

- 使用JavaScript语法开发后端应用
- 一些公司要求前端工程师掌握Node开发
- 生态系统活跃，有大量开源库可以使用

1.4Node 是什么

<span style="color:red">Node</span> 是一个基于Chrome V8引擎的JavaScript代码运行环境

运行环境

- 浏览器(软件) 能够运行JavaScript代码，浏览器就是JavaScript代码的运行环境
- Node（软件）能够运行JavaScript代码，Node 就是JavaScript代码的运行环境

## 2.Node运行环境搭建

 2.1Node.js运行环境安装   Node.js[官网](http://nodejs.cn/)

- LTS = Long Term Support 长期支持版 稳定版 （推荐下载）
- Current 拥有最新特性实验版

[安装步骤](https://www.cnblogs.com/liuqiyun/p/8133904.html)

安装注意：目录一般不要出现有中文的文件夹，系统是多少位。

Node是否安装成功 （cmd中敲命令行）

```node
查看Node版本     node -v 
```

2.2Node环境安装失败解决办法

1. 错误代码2502、2503 失败原因:系统账号权限不足

   解决方法：

   1. 以管理员身份运行cmd命令行工具
   2. 输入运行安装包命令msiexec/package node安装包位置

2. 执行命令报错

   失败原因：Node安装目录写如环境变量失败

   解决方法：将Node安装目录添加到环境变量中

2.3 PATH环境变量

存储系统中的目录，在命令中执行命令的时候系统会自动去这些目录中查找命令的位置

## 3.Node.js快速入门

3.1Node.js的组成

- JavaScript由三部分组成 ECMAScript( <span style="color:red">核心</span>),DOM,Bom
- Node.js是由<span style="color:red">ECMAScript</span>及Node环境提供的一些附加API组成的,包括文件,网络,路径等等一些更强大的API

3.2Node.js基础语法

所有ECMAScript语法在Node环境中都可以使用

3.3 Node.js全局对象global

在浏览器中全局对象是window,在Node中全局对象global.

Node中全局对象下有以下方法，可以在任何地方使用，global可以省略

- console.log() 	 在控制台中输出
- setTimeout()       设置超时定时器
- chearTimeout()   清除超时定时器
- setInterval()        设置间隔定时器
- clearInterval()      清除间隔定时器

代码示例

```java
global.console.log('我是global对象下的console.log方法输出的内容')
```




## 4.Node.js模块化开发

4.1JavaScript开发弊端

 JavaScript在使用时存放在两大问题，文件依赖和命名冲突

4.2生活中的模块开发

 比如：电脑主机组成，显卡，内存，电源，主板，CPU，如果由一个坏了，只需换一个硬件

4.3 软件中的模块化开发

 一个功能就是一个模块，多个模块可以组成完整应用，抽离一个模块不会影响其他功能的运行

|                |                   | app.js      |                  |                 |
| -------------- | ----------------- | ----------- | ---------------- | --------------- |
| **user.js**    |                   | **post.js** |                  | **goods.js**    |
| **addUser.js** | **deleteUser.js** |             | **findGoods.js** | **addGoods.js** |
|                |                   |             |                  |                 |

4.4Node.js中模块化开发规范

- Node.js规定一个JavaScript文件就是一个模块，模块内部的变量和函数默认情况下在外部无法得到
- 模块内部可以使用exports对象进行成员导出，使用require方法导入其他模块

4.5模块成员导出

```javascript
//a.js
//在模块内部定义变量
let version = 1.0;
//在模块内部定义方法
const sayHi = name => `你好${name}`;
//向模块外部导出数据
exports.version = version;
exports.sayHi = sayHi;

```

 语法：

```javascript
exports.命名 = 函数; //exports作用进行成员导出 导出是对象
```

4.6模块成员的导入

```javascript
//b.js
//在b.js模块值导入模块a
let a = require('./b.js'); //路径也可以写成为'./b'
//输出b模块中的version变量
console.log(a.version);
//调用b模块中的sayHi方法 并输出其返回值
console.log(a.sayHi('web云空'))
```

语法:

```javascript
const obj  = require('相对路径') //require作用导入其他模块 返回值是对象
```

1.7模块成员导出的另一个方式

```javascript
module.exports.version = version;
module.exports.sayHi = sayHi;
```

exports是module.exports的别名(地址引用关系),导出对象最终以modlule.exports为准

1.8模块导出两种方式的联系与区别

 exports 

 module.exports 可以修改对象中的值

```javascript
//当export对象和moudle.exports对象指向的不是同一个对象时 以module.exports为准
module.exports={
	name:'yunkong'
}
exports ={
    name:'yunfei'
}
```

## 5.Nodex.js系统模块

5.1什么是系统模块

​	Node运行环境提供API 因为这些API都是以模块化的方式进行开发的,所以我们又称Node运行环境提供的API为系统模块

 https://www.bilibili.com/video/av81455397?p=8 

文件模块(fs)

1. 读取文件
2. 写入文件
3. 创建文件夹

5.2系统模块fs文件操作

 f:file 文件 ， s system 系统 文件操作系统。

```javascript
const fs = require('fs');
```

读取文件内容语法

```javascript
//语法：具有[ ]这个符号的意思是 可选参数  callback是回调函数
fs.reaFile('文件路径/文件名称'[,'文件编码'],callback);
```

读取文件语法示例

```javascript
//读取上一级css目录下中的base.css
fs.readFile('../css/base.css','utf-8',(err,doc)=>{
    //如果文件读取发生错误 参数err的值为错误对象 否则err的值就为null
    //doc参数为文件内容
    if(err == null){
        //在控制台中输出内容
        console.log(doc);
    }
})
//node中AIP 是错误优先的， err是是否成功 doc是读取结构 使用fs.readFile()方法必须先引入 fs模块
```

写入文件内容语法

```javascript
fs.writeFile('文件路径/文件名称','数据',callback);
```

写入文件语法示例

```javascript
const content = '<h3>正在使用fs.writeFile写入文件内容<h3>';
fs.writeFile('../index.html',content,err =>{ //如果没有这个文件(index.html)就是生成该文件。
    if(err != null){
        console.log(err);
        return;
    }
    console.log('文件写入成功')
})
```

5.3系统模块path路径操作

为什么要进行路径拼接

- 不同操作系统的路径分隔符不统一

- /public/uploads/avatar

- Windows 上是 \ /

- Linux 上是 / （推荐）

路径拼接语法

```javascript
path.join('路径','路径',....)
```

路径拼接语法示例

```javascript
//导入path模块
const path = require('path');
//路径拼接
let finialPath = path.join('itcast','a','b','c.css');
//输出结果itcast\a\b\c.css
console.log(finialPath)
```

5.4 相对路径vs绝对路径

- 大多数情况下使用绝对路径，因为相对路劲又时候相对的是命令工具的当前工作目录
- 在读取文件或者设置文件路径时都会选择绝对路径
- 使用__dirname获取当前文件所在的绝对路径
- require()方法是用相对路径

```javascript
path.join(__dirname,'文件');
```

## 6.第三方模块

6.1什么是第三方模块

别人写好的、具有特别功能的、我们能直接使用的模块即第三方模块、由于第三方模块通常都是由多个文件组成并且被放置在一个文件夹中、所以又命名为包。

第三方模块有两种存在形式

- 以js文件的形式存在，停供现实项目具有体功能的API接口
- 以命令行工具形式存在，辅助项目开发

6.2获取第三方模块

npmjs.com:第三方模块的存储和发放仓库

npm(node package manager):node 的第三方模块管理工具

npm模块下载

```javascript
//npm:指令 install:下载 
npm install 模块名称

//会出现一个node_modules文件夹 和 一个package-lock.json文件
//node_modules文件夹是放置所有的包

```

npm模块卸载

```javascript
npm uninstall package 模块名称
```

6.3 第三方模块 nodemon

nondemon是一个命令行工具，用以辅助项目开法。

在Node.js中，每次修改文件都要在命令工具中重新执行该文件，非常繁琐。

使用步骤

1. 使用npm install nodemon -g 下载模块
2. 在命令行工具中用nodemon命令代替node命令执行文件

6.4 第三方模块 nrm
nrm (npm registry manager): npm 下载地址切换工具
npm默认的下载地址在国外，国内下载速度慢

使用步骤

1. 使用npm install nrm -g 下载它
2. 查询可用下载的地址列表nrm ls
3. 切换npm 下载地址 nrm use 下载地址名称（taobao）

6.5 第三方模块 Gulp

基于ndoe平台开发的前端构建工具
将机器化操作编程任务,想要执化机器化操作时执行一个命令行命令任务就能自动执行了
用机器代替手工，提高开发效率

Gulp 能做什么

- 项目上线 HTML，CSS ，JS文件压缩合并
- 语法转换（es6、less）
- 公共文件抽离
- 修改文件浏览器自动刷新

Gulp 使用

1. 使用npm install gulp 下载gulp库文件
2. 在项目根目录下建立gulpfile.js文件
3. 重构项目的文件夹机构src目录放置源代码文件 dist目录放置构建后文件
4. 在gulpfile.js文件中编写任务
5. 在命令行工具执行gulp任务

Gulp 中提供的方法

- gulp.src() :获取任务处理的文件
- gulp.dest() :输出文件
- gulp.task() :建立gulp任务
- gulp.watch() :监控文件的变化

Gulp语法示例

```js
//引入Gulp 模块
cosnt gulp = require('gulp');
//使用gulp.task()方法建立任务
//第一个任务名称
//第二个任务的回调函数
gulp.task('first',()=>{
    //获取要处理的文件
    gulp.src('./src/css/base.css')
    //将来处理后的文件输出到dist目录
    .pipe(gulp.dest('./dist/css'));
});
```

安装命令工具

```js
//全局安装指令
npm install gulp-cli -g
//执行命令 任务
gulp first
```

Gulp插件

- gulp-htmlmin : html 文件压缩
- gulp-csso : css 文件压缩
- gulp-babel: JavaScript 语法转化
- gulp-less : less 语法转化
- gulp-uglify: 压缩混淆JavaScript
- gulp-file-include 公共文件包含
- browsersync 浏览器实现同步

下载插件

```js
npm install gulp-htmlmin  //下载 html 文件压缩
npm install gulp-file-include //下载 公共文件包含 
//其他下载就换名字
```

HTML任务语法示例

```js
const htmlmin = require('gulp-htmlmin');
const fileinclude = require('gulp-file-include');
//html 任务
gulp.task('htmlmin',() = >{
    gulp.src('./src/*.html')
        //提取公共代码
        .pipe(fileinclude())
        //压缩html文件中代码 collapseWhitespace 是否压缩空格
        .pipe(htmlmin({collapseWhitespace:true}))
        .pipe(gule.dest('dist'));
})
```

```html
公共的html写道另一个html文件中
通过@@include('路径') 引用公共代码
<div>
    我是公共代码
    我是写在a.html
</div>

<!--另一个文件html 代码-->
@@include('./a.html') <!--引用公共的html 代码-->
<div>
    我是另一个代码
</div>
```

CSS任务语法示例

```js
//npm install gulp-less 首先下载 代码写在gulpfile.js中
//npm install gulp-csso
const less = require('gulp-less')  //less 模块是 less转成css
const csso = require('gulp-csso') //csso 模块是csso css文件的压缩
gulp.task('cassmin',()=>{
    //选择css目录下所有less文件以及css文件
    gulp.src('./src/css/*.less') //src 可以传数组 src(['./src/css/*.less','./src/css/*.css'])
        .pipe(less()) //将less语法转化为css语法
        .pipe(csso()) //css代码进行压缩
        .pipe(gule.dest('dist/css')); //将处理的结果进行输出
})
```

JavaScript任务语法示例

```js
//npm install gulp-uglify
//npm install gulp-babel @babel/core @babel/preset-env
const babel = require('gulp-babel'); //babel模板是 ES6转化成ES5
const uglify = require('gulp-uglify'); //uglify模块是 js代码的压缩
const less = require('gulp-less')
gulp.task('jsmin',()=>{
     //选择js目录下所有js文件
	gulp.src('./src/js/*.js')
      	.pipe(babel({
        	//它可以判断当前代码的运行环境 将代码转换为当前运行环境所支持的代码
        	presets:['@babel/env']
    	}))
    	.pipe(uglif());
        .pipe(gule.dest('dist/css')); //将处理的结果进行输出
    	
})
```

文件夹任务语法示例

```js
gulp.task('copy',()=>{
	gulp.src('./src/images/*')
    	.pipe(gulp.dest('dist/images'));
    gulp.src('./src/lib/*')
    	.pipe(gulp.dest('dist/lib'));
})
```

构建任务语法示例

```js
//一个指令 把所有的指令一起执行 默认为default
gulp.task('default',['htmlmin','cssmin','jsmin','copy']);
//gulp default
```

6.6 第三方模块 router

功能:实现路由 下载:npm install router

使用步骤

1.  获取路由对象 const router = getRouter();
2. 调整路由对象提供的方法创建路由
3. 启用路由,使路由生效

```js
const getRouter = require('router')
const router = getRouter();
router.get('/add',(req,res)=>{
    // req 是页面发来的数据
    // res 是响应给页面的数据
    res.end('Hello World!')
})
server.on('request',(req,res)=>{
    router(req,res);
})

```

6.7 第三方模块 Express

Express是一个基于Node平台的web应用开发框架，它提供一系列的强大特性,帮助你创建各种web应用。

我们可以使用 npm install express 命令进行下载

 Express 框架特性

- 提供了方便简洁的路由定义方式
- 对获取HTTP请求参数进行了简化处理
- 对模板引擎支持程序高，方便渲染动态HTML页面
- 提供了中间件机制有效控制HTTP请求
- 拥有大量第三方中间件对功能进行扩展

原生Node.js 与 Express 框架对比之获取请求参数

原生

```js
app.on('request',(req,res)=>{
    //获取GET参数
    let {query} = url.parse(req.url,true);
    //获取POST参数
    let postData = '';
    req.on('data',(chunk)=>{
        postData += chunk;
    })
    req.on('end',()=>{
        console.log(querystring.parse(postDate))
    })
})
```

框架

```js
app.get('/',(req,res)=>{
 	//获取GET参数
    console.log(req.query);
})
app.post('/',(req,res)=>{
    //获取POST参数
    console.log(req.body);
})
```

代码示例

```js
//引入express 框架
const express = require('express');
//创建网站服务器
const app = express();

app.get('/',(req,res)=>{
    //send()
    //1. send 方法内部会检测响应内部的类型
    //2. send 方法会自动设置http状态码
    //3. send 方法会帮我们自动设置响应的内容类型及编码
    res.send('Hello.Express');
})

//监听端口
app.list(3000);
console.log('网站服务器启动成功');
```



## 7.package.json文件

7.1 node_modeules 文件夹的问题

1. 文件夹以及文件过多过碎，当我们将项目整体拷贝给别人的时候，传输速度会很慢很慢
2. 复杂的模块依赖关系需要被记录，确保模块的版本和当前保持一致，否则会导致当前项目运行报错

7.2 package.json文件的作用

项目描述文件，记录了当前项目信息，例如项目名称，版本，作者，github地址，当前项目依赖了那些第三方模块等。

初始化 node_modeules 

```js
npm init -y //命令生成 
```

```json
{
    "name":"description",
    "version":"1.0.0", //版本号
    "description":"",
    "main":"index.js",//默认文件下index.js 入口程序
    "scripts":{ //存储命令的别名
        "test":"echo\"Error: no test specified \" && exit 1",   
    },
    "keywords":[], //
    "author":"", //项目作者
    "license":"ISC" //开源
    "dependencies":{ //依赖的模块
    	"formidable":"^1.2.1",
         "mime":"^2.3.1"
	}
}
```

通过package.json中dependencies依赖的模块 直接下载需要的

直接就可以生成需要的包

```js
npm install
```

7.3项目依赖

- 在项目的开发阶段和上线运营阶段，都需要依赖的第三方包，称为项目依赖
- 使用npm install 包名命令下载的文件会默认添加到package.json 文件的 dependencies 字段中

```json
{
	"dependencies":{
		"jquery":"^3.3.1"
	}
}
```

7.4项目开发依赖

- 在项目的开发阶段需要依赖,线上运营阶段不需要依赖的第三方包，称为开发依赖
- 使用npm install 包名 --save-dev 命令将包添加到package.json 文件的devDependencies字段中

```js
npm install gulp --save-dev
```

生产环境

```
npm install --production
```

7.5 package-lock.json 文件

- 锁定包的版本，确保在次下载时会因为包的版本不同而产生问题
- 加快下载速度，因为该文件中已经记录了项目所依赖第三方包的树状结构和包下载地址，重新安装时只需下载即可，不需要做额外的工作

## 8.模块加载机制

8.1 模块查找规则-当模块拥有路径但没有后缀时

```js
require('./find.js');
```

require方法根据路径查找模块，如果是完整路径，直接引入模块。

```js
require('./find')
```

如果模块后缀省略,先找同名js文件找同名js文件夹

如果找到同名文件件,找文件中的index.js

如果文件中没有index.js 就会去当前文件夹中的package.js文件中查找main选项的入口文件

如果找指定的入口文件不存在或者没有指定入空文件就会报错，模块没有被找到

8.2 模块查找规则--当模块没有路径且没有后缀时

```js
require('find');
```

1. Node.js会假设它是系统模块
2. Node.js会去node_moduless 文件夹中
3. 首先看是否该名字的JS文件
4. 在看是否该名字的文件夹
5. 如果是文件夹看里面是否有index.js
6. 如果没有index.js查看改文件中的package.json中的main选项确定入口文件
7. 否则找不到报错

## 9.服务器端基础概念

9.1URL

统一资源定位符，又叫RUL(Uniform Resource Locator),是专为标识Internet网上资源位置而设一种编址方式，

我们平台所说的网页地址指的即是URL

URL的组成

<span style="color:red">传输协议</span>：//服务器IP或者域名：端口/<span style="color:red">资源所在位置标识</span>>

<span style="color:red">http:</span>//www.itcast.cn<span style="color:red">/news/20181018/091522385.html</span>

http:超文本传输协议,提供一种发布和接收HTML页面的方法

<span style="color:red"></span>>

9.2 开发过程中客户端和服务端说明

在开发阶段，客户和服务器使用同一台电脑，即开发人员电脑

开发人员电脑

客户端 （浏览器）

服务器端（Node）

本机域名：localhost

本地IP：127.0.0.1

9.3 网站的组成

网站应用程序主要两大部分：客户端和服务器端。

客户端：在浏览器中运行的部分，就是用户看到并与之交互的界面程序。使用HTML，CSS，JavaScript构建

服务器端：在服务器中运行的部分，负责存储数据和处理应用逻辑。

9.4Node 网站服务器

能够停供网站访问服务器的机器就是网站服务器，它能接客户端的请求，能够对请求做出响应

9.5 IP地址

互联网中设备的唯一标识。

IP是Internet Protocol Address的简写，代表互联协议地址

9.6 域名

由于IP地址难于记忆,所以产生了域名的概念，所以域名就是平时上网所使用的网址

http://www.yunkong.com => http://124.165.219.100/

虽然在地址栏输入的是网站,但是最终还是会将域名转换为ip才能访问指定的网站服务器。

9.7 端口

端口是计算机与外界通讯交流的出口，用来区分服务器电脑中停供的不同的服务器

## 10.创建web服务器

创建web服务器示例代码

```javascript
//引用系统模块  这个模块用于创建网站服务器的模块
const http = require('http');
//创建web服务器 app对象就是网站服务器对象
const app = http.createServer();
//当客户端发送请求的时候, on()函数 参数一：请求对象， 参数二:事件处理函数
app.on('requset',(req,res)=>{
    //req ---》requset 代表是请求对象
    //res ---》response 代表是响应  返回给浏览器数据
    //响应
    res.end('<h1> hi user </h1>');
});
//监听3000端口
app.listen(3000);
console.log('服务器已启动，监听3000端口，请访问localhost:3000端口')
```

## 11.HTTP协议

11.1HTTP协议的概念

<span style="color:red">超文本传输协议（英文：HyperText Transfer Protocol）</span>缩写：<span style="color:red">HTTP</span>规定了如何从网站服务器传输超文本到本地浏览器，它基于客户端服务器机构工作,是客户端（用户）和服务器端（网站）请求答应的标准

客户端 请求 服务器

服务器 响应 客户端

使用HTTP协议

11.2 报文

在HTTP 请求和响应的过程中传递的数据块就是叫报文，包括要传送的数据和一写附加信息，并且要遵守规定好的格式

| 请求报文（客户端向服务器端） | 响应报文（服务器端向客户端） |
| ---------------------------- | ---------------------------- |
| 请求方式:post                | 内容类型：text.html          |
| 请求地址:www.yunkong.com     | 内容长度：20                 |
| Hello , 给我一个好消息       | Hi,我就是好消息              |

通过浏览器中Network面板中Header面板可以观看请求报文和响应报文

Header面板

- Response Headers 响应报文
- Request Headers 请求报文

11.3 请求报文

1. 请求方式（Requset Method）
   - GET方式 请求数据
     - 浏览器中输入发url是get请求
     - a标签是get请求
     - 表单默认是get请求
   - POST方式 发送数据
     - from 可以是post请求
2. 请求地址（RequestURL）

事件处理函数req中的方法

```js
app.on('requset',(req,res)=>{
 	//获取请求方式
    req.method;
    console.log(req.method);
    //获取请求URL
    req.url;
    console.log(req.url);
    //获取请求报文
    req.headers;
    console.log(req.headers);
});
```

请求报文代码示例

```js
//引用系统模块  这个模块用于创建网站服务器的模块
const http = require('http');
//创建web服务器 app对象就是网站服务器对象
const app = http.createServer();
//当客户端发送请求的时候, on()函数 参数一：请求对象， 参数二:事件处理函数
app.on('requset',(req,res)=>{
    
    //获取请求报文
    console.log(req.headers['accept'])
    
    //判断请求地址
    if(req.url == '/idnex' || req.url == '/'){
        res.end('welcome to homepage');
    }else if(req.url == '/list'){
        res.end('welcome to listpage');
    }else{
        res.end('not found');
    }
    
    //判断请求方式
    if(req.method == 'POST'){
        res.end('post')
    }else if(req.method == 'GET'){
        res.end('get')
    }
});
//监听3000端口
app.listen(3000);
console.log('服务器已启动，监听3000端口，请访问localhost:3000端口')
```

11.4 响应报文

1. HTTP状态码(Status)
   - 200 请求成功
   - 404 请求的资源没有找到
   - 500 服务器端错误
   - 400 客户端请求有语法错误

响应头设置

```js
res.writeHead(200,{
'content-type':'text/html;charset=utf8'
})
```

## 12.HTTP请求与响应处理

12.1 请求参数

客户端向服务端发送请求时，有时需要携带一些客户信，客户信息需要通过请求参数的形式传递到服务器端，比如登操作

12.2 GET请求参数

- 参数被放置在浏览器地址栏中，例如：http:localhost:3000/<span style="color:red;">?name=zhangshan&age=20</span>

```js
const url = require('url');
app.on('requset',(req,res)=>{
    console.log(req.url);//打印url地址
    //要解析url地址
    console.log(url.parse(req.url));
    //将查询参数解析成对象形式
    console.log(url.parse(req.url,,true));
    //解析url里的参数
    let params = url.parse(req.url,true).query;
    console.log(params.name); 
    console.log(params.age);
    //pathname是没有参数的的地址
    console.log(params.pathname);
    
     //判断请求地址
    if(params.pathname == '/idnex' || params.pathname == '/'){
        res.end('welcome to homepage');
    }else if(params.pathname == '/list'){
        res.end('welcome to listpage');
    }else{
        res.end('not found');
    }
    
})
```

12.3 POST请求参数

- 参数被放置在请求体中进行传输
- 获取POST参数需要使用data事件end事件
- 使用querystring系统模块将参数转换为对象格式

html文件（浏览器端）

```html
<!DOCTYPE html>
<html lang="en">
	<head>
        <meta charset="UTF-8">
        <title>Document</title>
    </head>
    <body>
       <!--
		method:指当前表单提交方式
		action:指定当前表单提交的地址
	   --> 
        <form method="post" action="http://loaclhost:3000">
            用户名：<input type="text" name="username"><br>
            密码：<input type="password" name="password"><br>
            <input type="submit">
        </form>
    </body>
</html>
```

node文件（服务器端）

```js
//导入系统模块querystring用于将HTTP参数换位对象格式
const querystring = require('querystring');
//post 参数是通过事件的方式接受的
//data 当请求参数传递的时候触发data事件
//end 当参数传递完成的时候触发end事件
app.on('request',(req,res)=>{
    let postData =  '';
    //监听参数传输事件
    req.on('data',(chunk)=> postData += chunk);
    //监听参数传输完毕事件
    req.on('end',()=>{
        console.log(postData);
        //把字符串转换成对象形式
        console.log(querystring.parse(postData));
    })
})
```

12.4 路由

- 首页：http://localhost:3000/index
- 登陆：http://localhost:3000/login
- 路由是指定客户端请求地址与服务端程序代码的对应的关系。简单的说，就是请求什么响应什么。

| url         | 路由 | 页面         |
| ----------- | ---- | ------------ |
| GET/index   |      | 响应首页     |
| GET/list    |      | 响应列表页   |
| GET/article |      | 响应文章页   |
| POST/login  |      | 登陆逻辑处理 |

路由示例代码

```js
const http = require('http');
const url = require('url');
//获取请求方式
const method = req.method.toLowerCase();
//获取请求地址
const pathname = url.parse(req.url).pathname;
if(method == 'get'){
    if(pathname == '/' || pathname == '/index'){
        res.end('欢迎来到首页');
    }else if(pathname == '/list'){
        res.end('欢迎来到列表页');
    }else {
        res.end('你访问的页面不存在')
    }
}else if(method == 'post'){
    
}

```

12.5 静态资源

服务器不需要处理，可以直接响应给客户端的资源就是静态资源，例如css，JavaScript，image文件，一般都会放在public文件夹中。

```js
const http = require('http'); //引入服务模块
const url = require('url'); //引入url路径模块
const path = require('path'); //引入路径拼接模块
const fs = require('fs'); //引入写入写出模块
//引入第三方模块 
const mime = require('mime')// npm install mime 获取请求文件类型
const app = http.createServer();
app.on('request',(req,res)=>{
   //获取用户请求的路径 会把get请求的参数抹去
   let pathname =  url.parse(req.url).pathname;
   pathname = pathname == '/'?'/default.html':pathaname; 
   //res.end() 是返回客户端的方法
   //将用户的请求路劲转换为实际的服务器硬盘路径
   let realPath = (path.join(__diranme,'public' + pathname));
    
   let type = mime.getType(realPath); 
   //读取文件 
   fs.readFile(realPath,(error,result)=>{
       //如果文件读取失败
       if(error != null){
          res.writeHead(404,{
              'content-type':'text/html;charset=utf8'
          }) 
      	  res.end('文件读取失败')      
       	  return;
       }
       res.writeHead(200,{
           'content-type':type
       })
       res.end(result); 
   }) 

})
app.listen(3000);
console.log('服务器启动成功')
```

 https://www.bilibili.com/video/av85548770?p=33 

12.6动态资源

相同的请求地址不同的响应资源，这种资源就是动态资源

图片的动态url

 http:www.yunkong.com/article?id=01

![img](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1581951514097&di=3bd80cbe151793cc614a6ef6d0b20e8b&imgtype=0&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fzhidao%2Fpic%2Fitem%2Fd1160924ab18972b48067763e4cd7b899e510a5e.jpg) 

 http:www.yunkong.com/article?id=02

![img](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1581951514097&di=0f8a3fb6e8ee7929c23571f466027c82&imgtype=0&src=http%3A%2F%2Fa.hiphotos.baidu.com%2Fzhidao%2Fpic%2Fitem%2Fa71ea8d3fd1f4134ff7d7513221f95cad1c85e10.jpg) 

## 13.Node.js异步编程

13.1同步API,异步API

同步API：只有当前API执行完后，才能继续执行下一个API

```js
//同步
console.log('before');
console.log('after');
```

异步API：当前API执行不会阻塞后续代码的执行

```js
//异步
console.log('before');
setTimeout(
	()=>{console.log('last')}
,2000);
console.log('after');
```

13.2同步API，异步API的区别(获取反回值)

同步API可以从返回值中拿到API执行的结果,但是异步API是不可以的

```js
//同步
function sum(n1,n2){
    return n1 + n2;
}
const result = sum(10,20);
```

```js
//异步
function getMsg(){
    setTimeout(function(){
        return{msg:'Hello Node.js'} 
    },200)
}
const msg = getMsg();
```

13.3回调函数

自定义函数让别人去调用

```js
//getData函数
function getData(callback){}
//getData函数用
getData(()=>{});
```

```js
function getMsg(callback){
	setTimeout(function(){
		cllback({
            msg:'hello node.js'
        })
	},,2000)
}
getMsg(function(data){
    console.log(data);
})
```

13.4 同步API,异步API的区别（代码执行顺序）

同步API从上到下依次执行，前面代码会阻塞后面代码的执行

```js
for(var i = 0; i<10000; i++){
	console.log(i);
}
//只用循环代码执行完，才会执行console.log()
console.log('for循环')
```

 异步API不会等待API执行完成后在向下执行代码

```js
console.log('代码开始执行');
setTimeout(()=>{console.log('2秒后执行代码')},2000);
setTimeout(()=>{console.log('0秒后执行行的代码')},0);
console.log('代码结束执行');
```

13.5Node.js中的异步API

```js
fs.readFile('./demo.txt',(err,result)=>{})
```

```js
var server = http.createServer();
server.on('requset',(req,res)=>{})
```

如果异步API后面代码的执行依赖当前异步API的执行结果，但实际上后续代码在执行的时候异步API还没有返回结果，这个问题要怎么解决呢？

```js
fs.readFile('./demo.txt',(err,result)=>{});
console.log('文件读取结果');
```

需求:依次读取A文件、B文件、C文件、（回调地狱）；

```js
fs.readFile('./1.txt','utf8',(err,result1)=>{
	fs.readFile('./2.txt','utf8',(err,result2)=>{
		fs.readFile('./3.txt','utf8',(err,result3)=>{

		})	
	})	
})
```

13.6 Promise
Promise出现的目的是解决Node.js异步编程中回调地狱问题

```js
let promise = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        if(true){
            resolve({name:'张三'}) 
        }else{
            reject('失败了')    
        }
    },2000)
})
promise.then(result => console.log(result);/*{name:'张三'}*/)
    .catch(error=> console.log(error);/*失败了*/)
```

```js
const fs = require('fs');
let promise = new Promise((resolve,reject)=>{
    fs.readFile('./1.txt','utf8',(err,result)=>{
        if(err != null){
            reject(err)
        }else{
            resolve(result);
        }
    })
})
promise.then((result)=>{
   console.log(result);
})
.catch((err)=>{
    console.log(err);
})
```

多个Promise读取文件

```js
function p1 (){
 	return new Promise((resolve,reject)=>{
        fs.readFile('./1.txt','utf8',(err,result)=>{
            resolve(result);
        })
	})    
}
function p2 (){
 	return new Promise((resolve,reject)=>{
        fs.readFile('./2.txt','utf8',(err,result)=>{
            resolve(result);
        })
	})    
}
function p3 (){
 	return new Promise((resolve,reject)=>{
        fs.readFile('./3.txt','utf8',(err,result)=>{
            resolve(result);
        })
	})    
}
p1().then((r1)=>{
    console.log(r1);
    return p2(); //当在then中return的一个Promise对象会在下一个then进行执行获取参数，从而达到链式调用
})
.then((r2)=>{
    console.log(r2);
    return p3();
})
.then((r3)=>{
    console.log(r3);
})
```

13.7 异步函数

异步函数是异步编程语法的终极解决方案，它可以让我们将异步代码写成同步的形式，让代码不在有函数嵌套，使代码变得清晰明了。

```js
const fn = async ()=>{};
```

```js
async function fn(){}
```

async关键字

1. 普通函数定义前加async关键字，普通函数变成异步函数
2. 异步函数默认返回Promise对象
3. 在异步函数内部使用return关键字进行结果返回 结果会被包裹的Promise 对象中 return关键字代替了resolve方法
4. 在异步函数内部使用throw关键字抛出程序异常
5. 调用异步函数再链式调用then方法获取异步函数执行结果
6. 调用异步函数再链式调用cath方法获取异步函数执行的错误信息

await 关键字

1. await 关键字只能出现在异步函数中
2. await promise await 后面只能写promise对象 ，写其他的API是不可以的
3. await 关键字可是暂停异步函数向下执行 直到promise 返回结果

代码示例

```js
//1.在普通函数定义的前面加上async关键字 普通函数就变成了异步函数
//2.异步函数默认的返回值是promise对象
//3.throw是JavaScript的关键字 意思是抛出错误，一但执行throw 后面的代码就不执行

//await 关键字
//1.它只能出现在异步函数中
//2.await promise 它可以暂停异步函数的执行 等待prominse对象返回结果后在向下执行函数
async function fn(){
    throw '发生了一些错误';
    return 123;
}
//console.log(fn())
fn().then(function(data){
    console.log(data);
}).catch(function(err){
    console.log(err);
})
```

多个异步函数

```js
async function p1(){
    return 'p2';
}
async function p1(){
    return 'p2';
}
async function p1(){
    return 'p2';
}
async function run(){
    let r1 = await p1();
    let r2 = await p1();
    let r3 = await p1();
    console.log(r1);
    console.log(r2);
    console.log(r3);
}
run()
```

promisify 函数

```js
const fs = require('fs');
//修改现有异步函数API 让其返回promise对象 从而支持异步函数语法
const promisify = require('util').promisity;
//调用promisify 方法改造现有异步API 让其返回promise对象
//通过promisify()方法修改fs.readFile的返回类型，修改成Promise类型
const readFile =  promisify(fs.readFile); 
async function run(){
    let r1  = await readFile('./1.txt','utf8')
    let r2  = await readFile('./2.txt','utf8')
    let r3  = await readFile('./3.txt','utf8')
    console.log(r1);
    console.log(r2);
    console.log(r3);
}

```

## 14.数据库概述及环境搭建

14.1为什么要使用数据库

- 动态网站中的数据库都是存储在数据库中的
- 数据库可以用来持久存储客户端通过表单收集的用户信息
- 数据库软件本身可以对数据进行高效的管理

14.2什么是数据库

数据库即存储数据库的仓库，可以将数据进行有序的分门别类的存储。它是独立于语言之外的软件，可以通过API去操作它。

常见的数据库软件有：mysql,mongoDB,oracle。

14.3 MongoDB数据库下载安装

下载地址：[点击步骤](https://www.mongodb.com/)

安装视频：[点击步骤](https://www.cnblogs.com/xiaozhaoboke/p/11479144.html)

14.4MongoDB可视化软件

是另一种可以操作数据的库的

14.5数据库相关概念

在一个数据库软件可以包含多个数据仓库，在每个数据库中可以包含多个数据集合，每个数据集合中可以包含多条文档（具体的数据）

| 术语       | 解释说明                                                     |
| ---------- | ------------------------------------------------------------ |
| database   | 数据库，mongoDB数据库软件中可以建立多个数据库                |
| collection | 集合，一组数据的集合，可以理解为JavaScript中的数组           |
| document   | 文档，一条具体的数据，可以理解为JavaScript中的对象（实际为json对象） |
| field      | 字段，文档中的属性名称，可以理解为JavaScript中的对象属性     |

 14.6Mongoose 第三方包

- 使用Node.js操作MongoDB数据库需要的依赖Node.js第三方包mongoose
- 使用<span style="color:red"> npm install mongoose</span> 命令下载（在项目文件中下载）

14.7 启动MongoDB

在命令工具运行<span style="color:red"> net start mongoDB</span>  即可启动MongoDB, 否则MongoDB将无法连接

在命令工具运行<span style="color:red"> net stop mongoDB</span>  即可关闭MongoDB

14.8 数据库连接

使用mongoose提供connect方法即可连接数据库

```js
//引入mongoose数据库的包
const mongoose = require('mongoose');
//connect方法返回是一个promise类型的对象,connect是连接的意思,
//mongodb://localhost/playground || mongodb是数据库的协议,localhost是端口,playground数据库的名称。
mongoose.connect('mongodb://localhost/playground',{
    useNewUrlParser:true
})
.then(()=>console.log('数据库连接成功'))
.catch(err=>console.log('数据库连接失败',err))
```

 14.9 创建数据库

在MongoDB中<span style="color:red">不需要显示</span>,如果正在使用的数据库不存在，<span style="color:red">MongoDB会自动创建</span>.

## 15.MongoDB增删改改查操作

15.1 创建集合

创建集合分为两步，一是对集合设定规则，二是创建集合，创建mongoose.Schema构造的实例即可创建集合。

```js
//设定集合规则
const courseSchema = new mongoose.Schema({
    name:String, //列名:字符串类型(String)
    author:String,
    isPublished:Boolean //列名:布尔值类型
});
//创建集合合并应用规则 mongoose.model('表名',集合规则)方法
//第一个参数 集合名称
//第一个参数 集合规则
const Course = mongoose.model('Course',courseSchema); //courses
```

15.2 创建文档

创建文档实例上就是<span style="color:red"> 向集合中插入数据</span>分成两步

1. 创建集合实例
2. 调用实例对象下的sava方法将数据保存到数据库中

创建文档方法一

```js
//创建文档实例
const course = new Course({
    name:'Node.js course',
    author:'云空',
    tags:['node','backend'],
    isPublished:true
});
//将文档插入到数据库中
course.save();
```

创建文档方法二

```js
//异步方法
Course.create({name:'JavaScript基础',author:'云空',isPublish:true},(err,doc)=>{
	//错误对象 err为null正确
    console.log(err)
    //当前插入的文档
    console.log(doc)
})
Course.create({name:'JavaScript基础',author:'云空',isPublish:true})
.then(doc=>console.log(doc))
.catch(err=>console.log(err))

```

15.3 mongoDB 数据库导入数据

mongoimport -d 数据库名称 -c 集合名称 --file 要导入的数据文件
找到mongodb数据库的安装目录，将安装目录下的bin目录放置环境变量中。

15.4 查询文档

```js
//根据条件查找文档 （条件为空侧所有文档）
Course.find().then(result =>console.log(result));
//返回的文档集合
[
   {
       __id:1f5s4fs5a4fa1,
       name:'node.js 基础',
       author:'云空'
   },
   {
       __id:1f5s4fs5a4fa1,
       name:'node.js 基础',
       author:'云飞'
   },   
]
```

查询多条数据

```js
mongoose.connect('mongodb//localhost/playground',{useNewUrlParser:true})
.then(()=>console.log('数据库连接成功'))
.then(()=>console.log('数据库连接失败',err));
//创建集合规则
const userSchema = new mongoose.Schema({
    name:String,
    age:Number,
    email:String,
    password:String,
    hobbies:[String]
});
//使用规则创建集合
const User = mongoose.model('User',UserSchema);

//查询用户集合中的所有文档
User.find().then(result => console.log(result) )

//通过下划线(_id) 字段查询文档 返回一定是数组 
User.find({_id:'jfaskljfkla42313'}).then(result => console.log(result) )

```

查询一条数据

```js
//findOne 方法返回一条文档
User.findOne({_id:'jfaskljfkla42313'}).then(result => console.log(result) )
```

查询大于

```js
//查询age 20 ~ 40的数据 $gt是大于 $lt是小于
User.find({age:{$gt:20,$lt:40}}).then(result=> console.log(result))
```

查询包含

```js
//
User.find({hobbies:{$in:['足球']}}).then(result=> console.log(result))
```

查询字段(列名)

```js
//-是不需要
User.find().select('name email -_id').then(result=> console.log(result))
```

数据排序

```js
//根据年龄字段进行升序排序
User.find().sort('age').then(result=> console.log(result))
//根据年龄字段进行降序排序
User.find().sort('-age').then(result=> console.log(result))
```

数据数量限制

```js
//skip(2)是从第几条开始 limit(3)是最多是3条数据
User.find().skip(2).limit(3).then(result=> console.log(result))
```

15.5 删除文档

删除单个

```js
//查找到一条文档并且删除
//返回删除的文档
//如何查询条件匹配了多个文档 那么将会删除第一个匹配的文档
Course.findOneAndDelete({_id:'456464564fsfa'}).then(result=> console.log(result))
```

 删除多个

```js
//
User.deleteMany({}).then(result=> console.log(result))
```

15.6 更新文档

更新单个

```js
User.updateOne({查询条件},{要修改的值}).then(result=> console.log(result))
User.updateOne({name:'李四'},{name:'云空'}).then(result=> console.log(result))
```

更新多个

```js
User.updateMany({查询条件},{要修改的值}).then(result=> console.log(result))
User.updateMany({},{age:56}).then(result=> console.log(result))
```

15. 7mongoose 验证

在创建集合时，可以设置当前字段的验证规则，验证失败就则输入插入失败

- required:true 必传字段

- minlength 最小长度

- maxlength 最大长度

- type 数据类型

- default 默认值

- enum 枚举

- trim:true 去除字符串两边的空格

- validate 自定义验证器

- default 默认值

  

```js
new mongoose.Schema({
	title:{
        type:String,
        required:true,
        /*
         required:[true,'请传入文章']
         第二个是报错信息
        */
        minlength:2, //最小长度
        maxlength:5 //最大长度
        trim:true, //去除字符串两边空格
    },
    age:{
    	type:Number,
    	min:18,
    	max:100
   },
   publishDate:{
       type:Date,
       //默认值
       default:Date.now
   }
   category:{
   		type:String,
         enum:['html','css','JavaScript','node']
   }
   author:{
        type:String,
        validate:{
            vaildator:v =>{
                //返回布尔值
                //true 验证成功
                //false 验证失败
                //v 要验证的值
                return v && v.length > 4
            },
            //自定义错误    
            message:'传入的值不符合规则'    
        }    
   }
})
const Post = mongoose.model('Post',postSchema);
Post.create({title:'aa',age:60,category:'java',author:'bd'}).then(result => console.log(result))
.cath(error =>{
    //获取错误信息对象
    const err = error.errors;
    //循环错误信息对象
    for(var attr in err){
        //将错误信息打印到控制台中
        console.log(err[attr]['message']);
    }
})
```

15.7集合关联

通常<span style="color:red">不同集合的数据之间是有关系的</span>，例如文章信息用户信息存储在不同集合中，但文章是某个用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联。

- 使用id对集合进行关联
- 使用populate 方法进行关联集合查询

```js
//用户集合
const User = mongoose.model('User',new mongoose.Schema({name:{type:String}}));
//文章集合
const Post = mongoose.model('Post',new mongoose.Schema({
    title:{type:String},
    //使用ID将文章集合和作者集合进行关联
    author:{
        type:mongoose.Schema.Types.ObjectId,
        ref:'User' //集合名称
    }
}))
//联合查询
Post.find().populate('author').then((err,result)=>console.log(result));
```

15.8 案例：用户案例信息增删改查

1. 搭建网站服务器，实现客户端与服务端的通信
2. 连接数据库，创建用户集合，向集合中插入文档
3. 当用户访问/list时，将所有用户信息查询出来
4. 将用户信息和表格HTML进行拼接并将结果响应客户端
5. 当用户访问/add时，呈现表单页面，并且实现添加用户信息功能
6. 当用户访问/modify时，呈现修改页面，并实现修改用户信息功能
7. 当用户访问/delete时，实现用户删除功能
8.  https://v2.bootcss.com/components.html#buttonGroups  网页组件大全

实现路由功能



https://www.bilibili.com/video/av85548770?p=51 

## 16.模板引擎的基础概念

16.1模板引擎

模板引擎是第三方模块。

让开发者以更加友好的方式拼接字符串，使项目代码更加清晰，更加易于维护

16.2 art-template 模板引擎

1. 在命令工具中使用 npm install art-template 命令进行下载
2. 使用const template = require('art-template ') 引入模板引擎
3. 告诉模板引擎要拼接的数据和模块在那 const html = template('模板路劲',数据)；

16.3 art-template 代码示例

node

```js
//导入系统模块
const path = require('path');
//const views = path.join(__dirname,'views','index.art')
// 导入模板引擎模块
const template =  require('art-template ');
//将待定模板与待定数据进拼接
//template 方法是用来拼接字符串的
//1.模板路径 绝对路径
//2.要在模板中显示的数据 对象类型
//返回拼接好的字符串
const html = template('./views/index.art',{
    data:{
        name:'张三',
        age:20
    }
})
console.log(html)
```

注意 虽然是html代码但是以及是art文件

```html
<!--标准语法-->
<p>{{name}}</p>
<p> {{1+1}}</p>
<!--原生语法 -->
<p><%=name%> </p>
<p><%= 1+1%> </p>

```

16.4原文输出

如果数据中携带HTML标签，默认模板不会解析标签，将会其转义后输出

- 标准语法 {{ @数据}}
- 原始语法 <%-数据%>

```html
<div>
	<span>{{@data.name}}</span>
    <span><%-data.age%></span>
</div>
```

16.5 条件判断

在模板中可以根据条件来决定是否那块HTML代码

```js
<!--标准语法 -->
{{if 条件}} {{/if}}
{{if vl}} {{else if v2}} {{/if}}
<!--原生语法 -->
<% if(value){%>  ......    <%} %>
<% if(value){%>  ......    <%} else if(value){ %> .....  <%}%>
```

 代码示例

```js

//标准语法
{{if age>18}}
    年龄大于18
 {{else if age < 15}}
 	年龄小于15
 {{else}}
     年龄不符合要求
{{/if}}
  
//原生语法
<% if(age>18) { %>
	年龄大于18
<% }else if(age < 15) { %>
     年龄小于15
<%}else {%>
     不符合年龄条件    
<%}%>    
  
```

16.6 循环

- 标准语法： {{each 数据}} {{/each}}
- 原生语法：<%for () {%> <%}%>

```js
<!--标准语法-->
{{each target}}
     索引
	{{$index}} {{$value}}
{{/each}}
<!--原始语法-->
<% for(var i = 0; i <target.length; i++) %>  
	<%= i %> <%=target[i] %>
<%}%>    
```

代码示例

```html
<!--标准语法-->
<ul>
    {{each users}}
    <li>
        {{$value.name}}
        {{$value.age}}
        {{$value.sex}}
    </li>
    {{/each}}
</ul>

<!--原始语法-->
<ul>
    <% for (var i = 0; i < user.length; i++){ %>
    	<li>
        	<%=user[i].name %>
             <%=user[i].age %>
             <%=user[i].sex %>
        </li>
    <%%>
</ul>
```

16.7 子模板

使用子模板可以将网站公共区块(头部，底部)抽离到单独的文件中

- 标准语法:{{include '模板'}}
- 原始语法：<%include('模板') %>

```html
<!--标准语法-->
{{include './header.art'}}
<!--原始语法-->
<% include('./header.art') %>
```

16.8 模板继承

使用模板继承可以网站HTML骨架抽离单独文件中，其他页面模板可以继承骨架文件

（ 首页页面模板 包含子模板 头部模板 ）继承 HTML骨架模板

简单说就把一个骨架挖几个坑，把向要的内容对坑添进去就可以了。

代码示例

```html
<!doctype html>
<html>
	<head>
		<meta charset = "utf-8">
		<title>HTML 骨架模板</title>
         {{block 'head'}}{{/block}}
	</head>
	<body>
        {{block 'content'}}{{/block}}
	</body>
</html>
```

```html
<!--index.art 首页模板 是继承--->
{{extend './layout.art'}}
{{block 'head'}} <link rel="stylesheet" href="custom.css">{{/block}}
{{block 'content'}} <p>This is just an awsome page.</p>{{block 'content'}}
```

16.9 模板配置

导入时间包 npm install deteformat

1. 向模板中导入变量 template.defaults.imports.变量名 = 变量值

2. 设置模板根目录 template.defaults.root = 模板目录

3. 设置模板默认后缀 template.defaults.extname = '.art'

   

代码示例

```js
//导入npm包
const template = require('art-template'); //模板包
const path = require('path'); //路径包
const dateFormat = require('dateformat');//配置模板包

//配置模板的根目录
template.defaults.root = path.join(__dirname,'views');
//配置模板的后缀
template.defaults.extname = '.art';
//导入模板变量
template.defaults.imports.dateFormat = dateFormat;

//const views = path.join(__driname,'views','06.art');
const html = template('06.art',{
    time:new Date() //创建一个时间
})
console.log(html);
```

```html
{{ dateFormat(time,'yyyy-mm-dd') }}
```

案例---学习

https://www.bilibili.com/video/av85548770?t=560&p=67

https://www.bilibili.com/video/av82257014?p=74

https://www.bilibili.com/video/av82257014?p=77

https://www.bilibili.com/video/BV187411C7C7?p=277

https://www.bilibili.com/video/BV187411C7C7?p=376 前后端分离

https://www.bilibili.com/video/BV187411C7C7?p=378 阿里百

[https://pan.baidu.com/s/1-nplTxYdujRjRNTCxqNWEQ#list/path=%2Fsharelink4197495409-993956270373319%2F2019%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%B0%B1%E4%B8%9A%E7%8F%AD&parentPath=%2Fsharelink4197495409-993956270373319](https://pan.baidu.com/s/1-nplTxYdujRjRNTCxqNWEQ#list/path=%2Fsharelink4197495409-993956270373319%2F2019黑马前端就业班&parentPath=%2Fsharelink4197495409-993956270373319)

黑马的前端资料

https://www.dalipan.com/detail/534e729aafa08d098d12812bef1e9ebd

黑马全部

[\w] 

 [\u4e00-\u9fa5]

[\u4e00-\u9fa5]

```html
<% for(var j = 0; j< allContent.length; j++){ %>
                        <li>
                            <div class="chatRoom-user">
                                <img src="<%=allContent[j].url%>">
                                <cite><%=allContent[j].user%><i><%=allContent[j].time%></i></cite>
                            </div>
                            <div class="chatRoom-user-text"><%=allContent[j].content%></div>
						</li>
						<% }%>
                            
                            <%=allContent[1].user %> 
```

https://www.bilibili.com/video/BV187411C7C7?p=529