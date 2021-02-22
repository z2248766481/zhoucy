# 1.node概述

## 1.1 介绍

https://nodejs.org/zh-cn/

http://nodejs.cn/

Node.js 是一个开源与跨平台的JavaScript 运行时环境。

它是在浏览器外运行，它是一个事件驱动异步I/O单进程的服务端JS环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

它使用新的 ECMAScript 标准，不必等待所有用户更新其浏览器，可以通过更改其版本来决定要使用新的标准特性。

**注意**

* 浏览器是JS的前端运行环境
* Node.js是JS的后端运行环境，在后端中运行无法调用 DOM 和 BOM 等浏览器内置 API
* nodejs调用服务查看服务器相关api  gulp基础 ->node环境



## 1.2 node应用场景

* 创建应用服务

* web开发

* 接口开发

* 客户端应用工具  gulp webpack vue脚手架 react脚手架 小程序等

## 1.3 安装

nodejs环境安装非常便捷，直接可通过官网地址，下载对应的安装软件包即可安装使用。

<img src="img/1 install.png" style="zoom:50%;" />

如果在开发的过程中，需要安装多个node的版本以支持 多个项目的使用，建议使用 [nvm node环境管理工具](https://www.runoob.com/w3cnote/nvm-manager-node-versions.html)，可以根据自己的电脑系统选择安装。

## 1.4 模块化

NodeJs基于 Commonjs模块化开发的规范，它定义一个JS文件就称之为一个模块

node的模块类型

* 核心模块 - 安装nodejs自带的模块
* 第三方模块 - 需要手动通过（npm/cnpm/yarn）安装的模块
* 自定义模块 - 开发者自己编写的模块

```js
// 模块导出
module.exports
exports

// 模块导入
require
```

Demo1:

```js
// app.js
var app = {
    name: '千锋教育HTML5大前端',
    sayName: function(name){
        console.log(this.name);
    }
}
module.exports = app;

// index.js
var app = require('./app.js');
app.sayName('hello');//hello
```

Demo2:

```js
// functions.js
var func1 = function() {
   console.log("func1");
};
 
var func2 = function() {
   console.log("func2");
};
 
exports.function1 = func1;
exports.function2 = func2;

// index.js
var functions = require("./functions");
functions.function1();
functions.function2();
```

# 2.node快速开始

## 2.1 运行js文件

检测nodejs是否安装成功,命令行输入如下语句

```bash
$ node -v
```

如果需要查看node的相关语法以及使用命令

```bash
$ node
```

## 2.2 核心模块

### 2.2.1 [os操作系统](http://nodejs.cn/api/os.html)

```js
const os = require('os')
console.log(os) // 查看所有的api
// 常用api
os.EOL // 操作系统特定的行末标志。根据操作系统生成对应的换行符. window 为 \r\n，linux为 \n
os.cpus() // 返回一个对象数组，其中包含有关每个逻辑 CPU 内核的信息。
os.totalmem() // 以整数的形式返回系统的内存总量（以字节为单位）。
os.freemem() // 以整数的形式返回空闲的系统内存量（以字节为单位）。
```

### 2.2.2 [path模块](http://nodejs.cn/api/path.html)

path模块用于处理文件和目录(文件夹)的路径

```js
const path = require('path')

# 获取路径最后一部内容  一般用它来获取文件名称
path.basename('c:/a/b/c/d.html')  // d.html

# 获取目录名，路径最后分隔符部分被忽略
path.dirname('c:/a/b/c/d.html') // c:/a/b/c

# 获取路径中文件扩展名
path.extname('c:/a/b/c/d.html') // .html

# 给定的路径连接在一起
path.join('/a', 'b', 'c') // /a/b/c
```

### 2.2.3 [url模块](http://nodejs.cn/api/url.html)

URL字符串是结构化的字符串，包含多个含义不同的组成部分。 解析字符串后返回的 URL 对象，每个属性对应字符串的各个组成部分。

```text
┌────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                              href                                              │
├──────────┬──┬─────────────────────┬────────────────────────┬───────────────────────────┬───────┤
│ protocol │  │        auth         │          host          │           path            │ hash  │
│          │  │                     ├─────────────────┬──────┼──────────┬────────────────┤       │
│          │  │                     │    hostname     │ port │ pathname │     search     │       │
│          │  │                     │                 │      │          ├─┬──────────────┤       │
│          │  │                     │                 │      │          │ │    query     │       │
"  https:   //    user   :   pass   @ sub.example.com : 8080   /p/a/t/h  ?  query=string   #hash "
│          │  │          │          │    hostname     │ port │          │                │       │
│          │  │          │          ├─────────────────┴──────┤          │                │       │
│ protocol │  │ username │ password │          host          │          │                │       │
├──────────┴──┼──────────┴──────────┼────────────────────────┤          │                │       │
│   origin    │                     │         origin         │ pathname │     search     │ hash  │
├─────────────┴─────────────────────┴────────────────────────┴──────────┴────────────────┴───────┤
│                                              href                                              │
└────────────────────────────────────────────────────────────────────────────────────────────────┘
```

```js
const url = require('url');

const href = 'http://www.xxx.com:3000/pathname?id=100#bbb'
// 解析网址，返回Url对象
// 参2 如果为true 则 query获取得到的为对象形式
url.parse(href,true)
```



### 2.2.4 [querystring模块](http://nodejs.cn/api/querystring.html)



### 2.2.5 [fs模块](http://nodejs.cn/api/fs.html)



### 2.2.6 [global全局变量](http://nodejs.cn/api/globals.html)



# 三.web服务器

## 3.1 介绍

Web服务器一般指的是网站服务器，是指驻留因特网上某一台或N台计算机的程序，可以处理浏览器等Web客户端的请求并返回相应响应，目前最主流的三个Web服务器是Apache、 Nginx 、IIS。

![](img/2 webservice.png)

## 3.2 传统开发和前后端分离开发

* 传统的开发也叫做前后端耦合开发

  前端写完页面，交给后端，后端把html页面后缀名改为自己需要的页面模版，然后渲染数据，示意图如下

![](img/3 together.png)

* 前后端分离开发

  前端开发者编写html页面通过Ajax调用后端的RestFul API接口进行数据进行交互，后面负责接口开发无需关心页面结构，示意图如下

  ![](img/4 leave.png)

  

## 3.3 服务器相关概念

### 3.3.1 IP地址

IP地址就是互联网上每台计算机的唯一地址，因此IP地址具有唯一性。在开发期间，自己的电脑既是一台服务器，也是一个客户端，可以在本机浏览器中输入127.0.0.1进行访问

### 3.3.2 域名

尽管 IP地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，叫域名地址。IP地址和域名是一一对应的关系，这份对应关系存放在一种叫做域名服务器(DNS)的电脑中。在开发测试期间， 127.0.0.1 对应的域名是 localhost。

本地如果localhost无法使用，则是因为本机中的hosts文件中没有匹配上ip地址

### 3.3.3 网络协议

网络上的计算机之间交换信息,就像我们说话用某种语言一样，在网络上的各台计算机之间也有一种语言，这就是网络协议，不同的计算机之间必须使用相同的网络协议才能进行通信。如：TCP、UDP、HTTP、FTP等等。

### 3.3.4 端口

服务器的端口号就像是现实生活中的门牌号一样。通过门牌号，外卖员就可以准确把外卖

送到你的手中。同样的道理，在一台电脑中，可以运行N多个web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理

**注意**

* http 默认端口为 80
* https 默认端口为443



## 3.4 创建web服务器

NodeJs是通过官方提供的http模块来创建 web服务器的模块。

通过几行简单的代码，就能轻松的手写一个web服务，从而对外提供 web 服务。

```js
// ①、导入http模块    
	const http = require('http')
// ②、创建web服务对象实例
	const server = http.createServer()
// ③、绑定监听客户端请求事件request
	server.on('request', (request, response) => {})

	/* request: 接受客户端请求对象，它包含了与客户端相关的数据和属性
			   request.url      客户端请求的uri地址
			   request.method  客户端请求的方式 get或post
			   req.headers	  客户端请求头信息
	response:服务器对客户端的响应对象
			  # 设置响应头信息 ，用于响应时有中文时乱码解决处理
			  response.setHeader('content-type', 'text/html;charset=utf-8')
			  # 设置状态码
  			  res.statusCode = 200
			  # 向客户端发送响应数据,并结束本次请求的处理过程
		
			  res.end('hello world')
	*/
// ④、启动服务
	server.listen(8080, () => {
  		console.log('服务已启动')
	})
```

## 3.5 静态资源服务器

客户端请求的每个资源uri地址，作为在本机服务器指定目录中的文件。

通过相关模块进行读取文件中数据进行响应给客户端，从而实现静态服务器。

![](img/05 web.png)



假设目录结构如下：

app.js

www

- read.txt
- photo.jpeg
- index.html

```js
// app.js
var http = require('http');
var fs = require('fs');
var server = http.createServer();
var wwwDir = __dirname;			// 所有读取文件所在的根目录
server.on('request', (req, res) => {
	/*
		req.url 拿到的路径是 端口号后面的
		例如： localhost：3000/index 对应的 path 就是 /index
	*/
    var url = req.url;  				
    var filePath = 'index.html';		// 路径为 '/' 时 文件路径指向index.html
    console.log(`${wwwDir}${filePath}`);
    
    if(url !== '/'){
    	filePath = url;
    }
    
    fs.readFile(`${wwwDir}${filePath}`, (err, data)=>{
    	if(err){
			return res.end('404');
		}
		res.end(data); 					//结束响应 并发送响应数据 
    })
})
server.listen('3000', '127.0.0.1', () => {
    console.log('http://localhost:3000/')
})
```

地址栏输入如下测试

```url
http://localhost:3000/  			# 显示 index.html
http://localhost:3000/index.html	# 显示 index.html
http://localhost:3000/read.txt		# 显示 read.txt
http://localhost:3000/photo.jpeg	# 显示 photo.jpeg
```

## 3.6 获取数据-get

get数据通过地址栏使用query方式进行传递的数据 

例如请求地址 http://localhost:3000?course=node&class=就业班

```js
const http = require('http');
const url = require('url');
http.createServer((req, res) => {
	// 获取地址栏中 query数据
	let { query } = url.parse(req.url, true);
	console.log(query); // { course: 'node', class: '就业班'}
}).listen(3000)
```

## 3.7 获取数据-post

表单数据多数为post进行提交到服务器端,可以通过[postman](https://www.postman.com/)测试

```js
const http = require('http');
const queryString = require('querystring');
http.createServer((req, res) => {
  let arr = [];
  // 数据接受中
  req.on('data', buffer => {
    arr.push(buffer);
  });
  // 数据传输结束了
  req.on('end', () => {
	// 拼接接受到的所有数据
    console.log(arr);
  });

}).listen(3000)
```



