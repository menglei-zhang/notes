# nodejs

```
npm: NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题
cnpm: 
nrm: 
nvm:
```



```
js和node都运行在v8引擎

nvm：nodejs 版本管理工具。也就是说：一个 nvm 可以管理很多 node 版本和 npm 版本；
nodejs：在项目开发时的所需要的代码库；
npm：nodejs 包管理工具；
在安装的 nodejs 的时候，npm 也会跟着一起安装，它是包管理工具；
npm 管理 nodejs 中的第三方插件；

nvm 管理 nodejs 和 npm 的版本
npm 可以管理 nodejs 的第三方插件

对于文件读写，node 采用的是非阻塞IO；
非阻塞IO将读写操作交给CPU，而代码正常执行，减少等待浪费的性能；
```

## 包

​    多个模块可以形成包，满足特定的规则才能形成规范的包
​    NPM(node.js package management) 
​        全球最大的模块生态系统，里面所有的模块都是开源免费的，也是node.js的包管理工具
​        官方网站 http://www.npmjs.com
​    npm包安装方式
​        本地安装：用于本地开发
​        全局安装：
​        NPM 常用的命令
​        1、安装包
​            全局安装 npm install -g es-checker
​        2、包卸载
​            全局安装 
​        3、更新

## nrm 

```
是 npm 的镜像源管理工具 
全局安装：npm install -g nrm 
查看当前可选的镜像源 nrm ls
切换镜像源 nrm use taobao
nrm add mycompany http://www.baidu.com  添加nrm
```

npm init -y

npm i jquery -S

## http超文本传输协议

```
就是数据如何传输的
    客户端（浏览器） ->   服务器 BS
    原生应用（QQ）   ->   服务器 CS
    特点：
    一问一答（先有请求，后有响应）
    5大特点：
        轻便/简单快速
        无连接（不为每一个请求保持住链接）
        无状态（服务器不记得客户端是谁）-> cookie
    主体对象
        服务器对象 http.createServer();
        客户端对象 http.request({host:'www.baidu.com});
        请求报文对象（对于服务器来说，是可读）req
        响应报文对象（对于服务器来说，是可写）res

```

## node 对象

### 全局对象

```
process
	process.env 是一个对象，我们可以通过其属性名来获取具体的环境变量值。
	process.argv    获取命令行参数 从0开始
filename dirname
	__filename  文件   目录+文件名
	__dirname   目录
```

### 核心对象

#### path  

```
const path = require('path');
	拼接并修正路径
	path.join
	path.resolve
	path.parse();  // 路径转为对象
	path.format()  // 对象转成字符串
```

#### fs

```
fs	文件读写（文件的操作就是IO）
const fs = require('fs');

fs.readFile   Buffer(16进制)  Buffer.toString('utf8')

  fs.readFile('./06_a.txt','utf8',(err,data)=>{
      if(err) throw err;   // 抛到控制台
      console.log(data);
  });

fs.writeFile

  fs.writeFile('./06_a.txt','我今天赚了一块钱',{flag:'a'},(err)=>{
      if(err) throw err;   // 抛到控制台
      console.log('完成');
  });
```

#### http

```
http
const http = require('http');
http超传输协议  就是数据如何传输
协议至少双方->http双方   ( 客户端(浏览器)->服务器BS  原生应用(QQ)->服务器CS )
先有请求后又相应
最重要两大特点：无连接（不为没有个请求保持住链接） /  无状态（服务器不记得客户端是谁）
```

### 自定义对象

## 其他功能

## 扩展介绍

### nodejs 同步异步

```
js是单线程
node 异步 如果不处理，会导致嵌套层级过深
```

```
// 引入对象
const path = require('path');
const fs = require('fs');
// 接收命令行参数 并修正路径
let myPath = path.resolve(process.argv[2]);
function testReadFiles(dir){
    try{
        // 判断文件是否存在
        fs.accessSync(dir,fs.constants.F_OK);
        // 判断文件的状态
        let state = fs.statSync(dir);
        if(state.isFile()){
        }else if(state.isDirectory()){
            console.log(dir);
            // 读取文件夹中的内容
            let files = fs.readdirSync(dir);
            console.log(files);
            // 遍历文件夹
            files.forEach(file=>{
                testReadFiles(path.join(dir,file));
            })
        }
    }catch(e){
        console.log(e);
        console.log('该文件或者文件夹不存在');
    }
}
testReadFiles(myPath);
```

## 包（文件夹）

### npm

```
自己先有一个包描述文件（package.json）
创建一个包描述文件 npm init -y
    会根据当前的文件夹来自动生成包名（不允许中文，不允许大写英文字母）
下载一个包 npm instail 包名@版本 --save  （npm i 包名 -S）
    --save (记录依赖)
根据package.json 文件中的dependencies属性恢复依赖
    恢复包： npm instail  （npm i）
卸载包 npm uninstail jquery@1.5.1 --save （npm un jquery@1.5.1 --S）
查看包的信息   
    npm info 包名      
    npm info 包名 versions
安装(卸载)全局命令行工具
    npm uninstail(uninstall) -g http-server
查看全局包下载路径
    npm root -g
```

### nrm   

```
nrm是npm的镜像资源管理工具

安装npm install -g nrm    
查看当前可选的镜像源  nrm ls
切换镜像源  nrm use taobao
添加私有源  nrm add name url
```

### 包的加载机制

```
我们未来可能需要辨识一个包中，入口是够是我们想要的启动程序
逐级向上查找node_module,直到盘符根目录
1、查找node_modules下的包名文件夹中的main属性（常用）
2、比常用：查找node_modules下的包名.js
3、查找node_modules下的包名文件中的index.js(常用)
逐级向上 node_modules 要么main属性，要么index.js
```

## 主体对象

```
服务器对象 http.createServer();
客户端对象 http.request({host:'www.baidu.com'});
请求报文对象(对于服务器来说，是可读) req
响应报文对象(对于服务器来说，是可写) res
```

## 创建服务器对象

```
1、引入http核心对象；
2、利用http核心对象的createServer(callback);创建服务器对象；
3、使用服务器对象.listen(端口,ip地址) 开启服务器；
4、callback(req,res)根据请求处理响应；
```

## 请求报文对象（只读）

```
请求首行中的url  (req.url)
请求首行中的请求方式  (req.method)
请求头中的数据 req.headers 是一个对象
头信息中，也可以作为与服务器交互的一种途径
```

## 响应对象

```
响应首行  res.writeHead(状态码)
写响应头:一次性要在多次后面
    一次性写头信息： res.writeHead(状态码)
    多次设置头信息： res.setHeader(key,value);
    res.setHeader('c','c') // 头
    res.writeHead(200,{'content-type':'text/html;charset=utf-8'})   // 行
写响应体:一次性要在多次后面
    一次性写响应体：res.end();
    多次写响应体: res.write();
```

## 获取请求体数据

```
代码对比
浏览器  $('$xx').on('submit',function(e){ })
服务器  req.on('data',function(d){ d.toString();})
```

## querystring 核心对象

```
querystring.parse(formStr)
username=jack&password=123 转换成 {username:'jack',password:'123'}
```

## 写会页面

```
做一个简单地查询功能，查询后，页面跳转，显示查询结果
数据关系是英雄名称
请求方式为get请求
```

## 状态码分类
1开头   正在进行中
2开头   完成
3开头   重定向
4开头   客户端异常
5开头   服务器异常

## express 

```
初始化 npm init -y
安装 npm i express -S
引入express第三方对象
构建一个服务器对象  server.use
开启服务器监听端口  server.listen
处理响应
在express中，保留了原生http的相关属性和函数

const express = require('express');
let server = express();
// 获取路由中间件对象
let router = express.Router();
// 配置路由规则 router.请求方式(URL,fn)
router.get('/login',(req,res) => {
    res.end('login page');
})
router.get('/register',(req,res) => {
    res.end('register page');
})
// 将router加入到应用 server.use(router)
server.use(router);
server.listen(8888,() => {
    console.log('服务器启动端口8888...');
})
```

## res 扩展函数
```
res.download('./xxx.txt')  // 下载文件
res.json({})   // 响应json对象
res.jsonp(数据)  // 配合jsonp 要求客户端请求的时候因为是jsonp方式 并且callback=xxx
res.redirect()   // 重定向 301是永久重定向  302临时重定向
res.send()  // 发送字符串数据自动加content-type
res.sendFile()   // 显示一个文件
res.sendStatus()  // 响应状态码
```

```
const express = require('express');
let server = express();
let router = express.Router();
router.get('/json',(req,res) => {
   res.json([{name:'jack'}]); // res.end只能响应string  读文件中的data Buffer
}).get('/redirect',(req,res) => {
    res.redirect('https://www.baidu.com');
}).get('/download',(req,res) => {
    res.download('./app.js');
}).get('/jsonp',(req,res) => {
    res.jsonp('jack love rose');
})
server.use(router);
server.listen(8888,()=>{
    console.log('8888');
})
```

http  fs 同步请求，获取页面
http  相应的json对象 配套前端ajax 请求

CommonJS：规范JavaScript 语言作为后端语言运行的标准；
模块（Module）应该怎么写：
1、依赖一个模块 require('模块名(id)')；
2、需要被模块依赖 module.export = 给外部的数据；
3、一个文件一个模块；



```
1、引入对象
2、创建服务器对象
3、处理响应
4、监听端口
```

```
const express = require('express');
let server = express();
server.use('/jishu',(req,res,next)=>{
    console.log('1');
    next();
})
server.use('/oushu',(req,res,next)=>{
    console.log('2');
    next();
})
server.use('/jishu',(req,res,next)=>{
    console.log('3');
    next();
})
server.use('/oushu',(req,res,next)=>{
    console.log('4');
})
server.listen(8888,()=>{
    console.log('runing...');
});
```

```
const express = require('express');
const server = express();
const router = express.Router();
router.get('/login',(req,res)=>{
    res.end('login page');
}).get('/register',(req,res)=>{
    res.end('register page');
}).get('/redirect',(req,res)=>{
    res.redirect('http://www.baidu.com');
}).get('/download',(req,res)=>{
    res.download('./app.js');
})
server.use(router);
server.listen(8888,()=>{
    console.log('running...');
})
```

```
res.download('/xxx.txt');   下载文件
res.json({})   响应json对象
    响应数据，最常用，返回ajax数据
res.jsonp(数据)  配合 jsonp 要求客户端请求的时候也是jsonp的方式 并且callback = xxx
res.redirect()  重定向 301 是永久重定向 302是临时定向
res.sed() 发送字符串自动加content-type
res.sendFile()  显示一个文件
res.sendStatus() 响应状态码
```

渲染页面 
    使用 art-template 模板引擎
    下载 express-art-template art-template
    npm i express-art-template art-template -S

// 先下载两个包（express-art-template  art-template)
//  npm i express-art-template art-template -S
/**

 * 配置过程
 * 1、注册一个模板引擎  '.'表示渲染文件的后缀名
 *      app.engine('.html',express-art-template);
 * 2、设置默认渲染引擎
 *      app.set('view engine','.html');
 * 3、res.render(文件名，数据对象);
 *      expree 这套使用，默认在当前app.js同级的wiews目录查找
 */

const express = require('express');
let server = express();
// 1、注册一个模板引擎  '.'表示渲染文件的后缀名
server.engine('.html',require('express-art-template'));
// 区分开发和生产环节的不停配置
server.set('view options', {
    // debug：不压缩不混淆 实时保持最新的状态
    // 非debug：压缩合并，list.html 静态数据不会实时更新（服务器重启才更新）
    debug: process.env.NODE_ENV !== 'production',
    imports:{  // 数据的导入和过滤显示的操作
        num:1,
        reverse:function(str){
            return '^_^ + str + ^_^';
        }
    }
});
// 2、设置默认渲染引擎
server.set('view engine','.html');
let router = express.Router();
router.get('/hero-list',(req,res)=>{
    res.render('list.html',{
        heros:[{name:'貂蝉'},{name:'张飞'},{name:'关羽'},{name:'刘备'}]
    });
})
server.use(router);
server.listen(8888,()=>{
    console.log('running...');
})

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h3>英雄列表</h3>
    <hr>
    imports.num:{{num}}
    imports.reverse{{reverse('abcdef')}}
    <hr>
    <ul>
        {{each heros}}
        <li>{{$value.name}}</li>
        {{/each}}
    </ul>
</body>
</html>

npm init -y
npm i express -S
npm i express-art-template art-template -S
npm i nodemon -S

js服务器处理中，要么 Next 传球，要么 end , render , send 响应
静态处理中间件，错误处理，优化用户体验 404 处理

服务端处理错误 和 404页面找不到
    404页面响应 router.all('*,()=>{})
    触发错误：
        next(err);
        处理错误： app.use(4参数错误)

nodemo 
    修改代码自动重启
    安装全局命令行工具  npm i -g nodemon
    进入到指定目录命令行 nodemon ./xxx.js
    手动触发重启，在命令行输入 rs 回车

const express = require('express');
const fs = require('fs');
let server = express();
server.engine('.html',require('express-art-template'));
server.set('view option',{
    debug:process.env.NODE_ENV !== 'production',
})
server.set('view engine','.html');
let router = express.Router();
router.get('/',(req,res,next)=>{
    let errorPath = './abc/e.txt';
    try{
        fs.readFileSync(errorPath);
        res.render('index');
    }catch(err){
        throw err;   
        next(err);  // 触发一个具备4个参数的中间件的函数
    }
}).all('*',(req,res)=>{
    res.send('地址错误，去<a href="httpe://www.baidu.com">百度</a>看看')
})
// 要把js下的文件暴露出来
server.use(express.static('./js'));
server.use(router);
// 处理错误（参数位置错误优先）-> 优雅的用具体验
server.use((err,req,res,next)=>{
    res.send('<h1>页面丢失，去<a href="https://www.baidu.com">百度</a>看看</h1>');
})
server.listen(8888,()=>{
    console.log('running...');
})

数据库 = 服务器 + 客户端
一个DB服务器，可以有多个用户（实例）
一个实例下有多个DB（数据）
一个DB下面有多个表（集合）， 例如学校DB下有多个班级（集合）
一个集合中有多条数据（文档对象）多个学生

mysql数据库，有数据需要先创建数据库，加入数据（各表见关系强烈）
    MongoDB是非关系型数据库，其关系的操作比较弱，所有的DB/集合 
    无需提前创建，直接使用

中间件 和 路由 的区别 
    app.use 没有请求方式，对于程序功能的区分

db.users.find({name:/红/});
db.users.find({name:/红$/});
db.users.find({name:/^红/});

db.users.update({name:/狗/，{$set:contry:'狗国'}})

删除数据库  db.dropDatabase()
创建集合    db.createCollection()
显示集合  	show collections
删除集合  	db.c_name.drop()
插入文档  	db.c_name.insert({key1:”value1”,key2:”value2”,…})
删除文档  	db.n_name.remove({key:value}) 
更新文档  	db.c_name.update({key:value},{$set:{key:value1}})
查看文档  	db.c_name.find()
		   db.c_name.find().pretty()
条件查询  	db.c_name.find({key:value,key2:value2}).pretty()
		   db.c_name.find({$or:[{key:value},{key2:value2}]}).pretty()
   		   db.c_name.find({key:{$gt:40},$or:[{key:value},{key2:value2}]}).pretty()
limit,skip	    db. c_name.find().limit(1).skip(1)
排序1/-1	  	db.c_name.find().sort({key:1})

### Node.js REPL(交互式解释器)
Node.js REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。
Node 自带了交互式解释器，可以执行以下任务：
读取 - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
执行 - 执行输入的数据结构
打印 - 输出结果
循环 - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。
Node 的交互式解释器可以很好的调试 Javascript 代码。
### Node.js 回调函数
Node.js 异步编程的直接体现就是回调。
异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。
回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。
例如，我们可以一边读取文件，一边执行其他命令，在文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件 I/O 操作。这就大大提高了 Node.js 的性能，可以处理大量的并发请求。
回调函数一般作为函数的最后一个参数出现：
function foo1(name, age, callback) { }
function foo2(value, callback1, callback2) { }
### Node.js 事件循环
Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。
Node.js 几乎每一个 API 都是支持回调函数的。
Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。
Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.
### Node.js EventEmitter
Node.js 所有的异步 I/O 操作在完成时都会发送一个 事件 到 事件队列。
Node.js 里面的许多对象都会 分发事件 ：
    一个 net.Server 对象会在每次有新连接时触发一个 事件， 
    一个 fs.readStream 对象会在文件被打开的时候触发一个 事件。 
    所有这些产生事件的对象都是 events.EventEmitter 的实例。
events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。
### EventEmitter 类
可以通过require("events")来访问该模块。
    // 引入 events 模块
    var events = require('events');
    // 创建 eventEmitter 对象
    var eventEmitter = new events.EventEmitter();
### Node.js Buffer(缓冲区)
JavaScript 语言自身 只有 字符串 数据类型，没有 二进制 数据类型。
但在处理像TCP流或文件流时，必须使用到二进制数据。
因此在 Node.js中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。
在 Node.js 中，Buffer 类是随 Node 内核一起发布的核心库。
Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据，每当需要在 Node.js 中处理I/O操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。

在v6.0之前创建Buffer对象直接使用new Buffer()构造函数来创建对象实例，但是Buffer对内存的权限操作相比很大，可以直接捕获一些敏感信息，所以在v6.0以后，官方文档里面建议使用 Buffer.from() 接口去创建Buffer对象。
### Node.js Stream(流)
Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。
例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）。
Node.js，Stream 有四种流类型：
    Readable - 可读操作。
    Writable - 可写操作。
    Duplex - 可读可写操作.
    Transform - 操作被写入数据，然后读出结果。
所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：
    data - 当有数据可读时触发。
    end - 没有更多的数据可读时触发。
    error - 在接收和写入过程中发生错误时触发。
    finish - 所有数据已被写入到底层系统时触发。
### Node.js模块系统  文件模块，原生模块
为了让Node.js的文件可以相互调用，Node.js提供了一个简单的模块系统。
模块是Node.js 应用程序的基本组成部分，文件和模块是一一对应的。
一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。
Node.js 提供了 exports 和 require 两个对象，
其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象
1、hello.js 通过 exports 对象把 world 作为模块的访问接口，在 main.js 中通过 require('./hello') 加载这个模块，然后就可以直接访 问 hello.js 中 exports 对象的成员函数了。
// main.js 文件，代码如下:

    var hello = require('./hello');
    hello.world();

// hello.js 文件，代码如下：

    exports.world = function() {
        console.log('Hello World');
    }

2、把一个对象封装到模块中
// hello.js 
function Hello() { 
    var name; 
    this.setName = function(thyName) { 
        name = thyName; 
    }; 
    this.sayHello = function() { 
        console.log('Hello ' + name); 
    }; 
}; 
module.exports = Hello;

// main.js 
var Hello = require('./hello'); 
hello = new Hello(); 
hello.setName('BYVoid'); 
hello.sayHello(); 

模块接口的唯一变化是使用 module.exports = Hello 代替了exports.world = function(){}。 在外部引用该模块时，其接口对象就是要输出的 Hello 对象本身，而不是原先的 exports。

Node.js 的 require 方法进行模块加载     原生模块的优先级仅次于文件模块缓存的优先级

### Node.js 函数
在JavaScript中，一个函数可以作为另一个函数的参数。我们可以先定义一个函数，然后传递，也可以在传递参数的地方直接定义函数。
Node.js中函数的使用与Javascript类似
function say(world){
    console.log(world);
}
function execute(someFunction,value){
    someFunction(value);
}
execute(say,hello);

function execute(someFunction,value){
    someFunction(value);
}
execute(function say(world){
    console.log(world);
},'你好');


const http = require('http');
http.createServer(function(req,res){
    res.writeHead(200,{
        "Content-type":"text/plain;charset=utf8"   // 不需要空格
    })
    res.write("世界晚安");
    res.end();
}).listen(8888,()=>{
    console.log('running...');
})

### Node.js 路由
要为路由提供请求的 URL 和其他需要的 GET 及 POST 参数，随后路由需要根据这些数据来执行相应的代码。
因此，需要查看 HTTP 请求，从中提取出请求的 URL 以及 GET/POST 参数。
这一功能应当属于路由还是服务器（甚至作为一个模块自身的功能）确实值得探讨，但这里暂定其为HTTP服务器的功能。
需要的所有数据都会包含在 request 对象中，该对象作为 onRequest() 回调函数的第一个参数传递。
但是为了解析这些数据，需要额外的 Node.JS 模块，它们分别是 url 和 querystring 模块。

### Node.js 全局对象
JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。
在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 global，
所有全局变量（除了 global 本身以外）都是 global 对象的属性。
在 Node.js 我们可以直接访问到 global 的属性，而不需要在应用中包含它。

最好不要使用 var 定义变量以避免引入全局变量，因为全局变量会污染命名空间，提高代码的耦合风险。

__filename   表示当前正在执行的脚本的文件名。
它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。 如果在模块中，返回的值是模块文件的路径。
__dirname    表示当前执行脚本所在的目录。
setTimeout(cb, ms)  全局函数在指定的毫秒(ms)数后执行指定函数(cb)。：setTimeout() 只执行一次指定函数。
clearTimeout(t) 全局函数用于停止一个之前通过 setTimeout() 创建的定时器。 参数 t 是通过 setTimeout() 函数创建的定时器。
setInterval(cb, ms)
setInterval(cb, ms)  setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。

### 常用工具
util 是一个Node.js 核心模块，提供常用函数的集合，用于弥补核心 JavaScript 的功能 过于精简的不足。
    const util = require('util');
util.callbackify(original) 将 async 异步函数（或者一个返回值为 Promise 的函数）转换成遵循异常优先的回调风格的函数，
例如将 (err, value) => ... 回调作为最后一个参数。 
在回调函数中，第一个参数为拒绝的原因（如果 Promise 解决，则为 null），第二个参数则是解决的值。
const util = require('util');
async function fn(){
    return '你好';
}
const callbackFunction = util.callbackify(fn);
callbackFunction((err,ret)=>{
    if(err) throw err;
    console.log(ret);
})

util.inherits
util.inherits(constructor, superConstructor) 是一个 实现 对象间 原型继承 的函数。
JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。
JavaScript 没有提供对象继承的语言级别特性，而是通过原型复制来实现的。
util.inspect
util.inspect(object,[showHidden],[depth],[colors]) 是一个将任意对象转换 为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。
util.isArray(object)
如果给定的参数 "object" 是一个数组返回 true，否则返回 false。
util.isRegExp(object)
如果给定的参数 "object" 是一个正则表达式返回true，否则返回false。
util.isDate(object)
如果给定的参数 "object" 是一个日期返回true，否则返回false。

### Node.js 文件系统
Node.js 提供一组类似 UNIX（POSIX）标准的文件操作API。 Node 导入文件系统模块(fs)语法如下所示：
var fs = require("fs")
异步和同步
Node.js 文件系统（fs 模块）模块中的方法均有异步和同步版本，
例如读取文件内容的函数有异步的 fs.readFile() 和同步的 fs.readFileSync()。
异步的方法函数最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。
建议大家使用异步方法，比起同步，异步方法性能更高，速度更快，而且没有阻塞。

// 文件读取
    // 异步
    fs.readFile(path,function(err,data){
        if(err) return console.error(err);
        console.log(data.toString());
    })
    // 同步
    var data = fs.readFileSync(path);
    console.log(data.toString());

打开文件  fs.open(path, flags[, mode], callback)
获取文件信息  fs.stat(path, callback)
写入文件  fs.writeFile(file, data[, options], callback)
读取文件  fs.read(fd, buffer, offset, length, position, callback)
关闭文件  fs.close(fd, callback)
截取文件  fs.ftruncate(fd, len, callback)
删除文件  fs.unlink(path, callback)
创建目录  fs.mkdir(path[, options], callback)
读取目录  fs.readdir(path, callback)
删除目录  fs.rmdir(path, callback)

### GET/POST请求
在很多场景中，我们的服务器都需要跟用户的浏览器打交道，如表单提交。
表单提交到服务器一般都使用 GET/POST 请求。

获取GET请求内容
由于GET请求直接被嵌入在路径中，URL是完整的请求路径，包括了 "?" 后面的部分，因此可以手动解析后面的内容作为GET请求的参数。
node.js 中 url 模块中的 parse 函数提供了这个功能。
获取 URL 的参数   使用 url.parse 方法来解析 URL 中的参数
获取 POST 请求内容
POST 请求的内容全部的都在请求体中，http.ServerRequest 并没有一个属性内容为请求体，原因是等待请求体传输可能是一件耗时的工作。
比如上传文件，而很多时候我们可能并不需要理会请求体的内容，恶意的POST请求会大大消耗服务器的资源，
所以 node.js 默认是不会解析请求体的，当你需要的时候，需要手动来做。

const http = require('http');
const querystring = require('querystring');
var postHTML = 
    '<html><head><meta charset="utf-8"><title>菜鸟教程 Node.js 实例</title></head>' +
    '<body>' +
    '<form method="post">' +
    '网站名： <input name="name"><br>' +
    '网站 URL： <input name="url"><br>' +
    '<input type="submit">' +
    '</form>' +
    '</body></html>';
http.createServer(function(req,res){
    var body = "";
    req.on('data',function(chunk){
        body += chunk;
    });
    req.on('end',function(){
        body = querystring.parse(body);
        res.writeHead(200,{
            'Content-type':'text/html;charset=utf8'
        })
        if(body.name && body.url){
            res.write('网站名：' + body.name);
            res.write('<br/>');
            res.write('网站url：' + body.url);
        }else{
            res.write(postHTML);
        }
        res.end();
    })
}).listen(8888,()=>{
    console.log('running...');
})

### Node.js 工具模块
在 Node.js 模块库中有很多好用的模块
Node.js os 模块提供了一些基本的系统操作函数。 var os = require("os")
Node.js path 模块提供了一些用于处理文件路径的小工具， var path = require("path")
Node.js Net 模块提供了一些用于底层的网络通信的小工具，包含了创建服务器/客户端的方法，  var net = require("net")
Node.js Domain(域) 简化异步代码的异常处理，可以捕捉处理try catch无法捕捉的异常。  ar domain = require("domain")

使用 Node 创建 Web 服务器
Node.js 提供了 http 模块，http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块

使用 Node 创建 Web 客户端
Node 创建 Web 客户端需要引入 http 模块，创建 client.js 文件

Node.js Express 框架
Express 简介
Express 是一个简洁而灵活的 node.js Web应用框架, 提供了一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。

使用 Express 可以快速地搭建一个完整功能的网站。

### Express 框架核心特性：
可以设置 中间件 来响应 HTTP 请求。
定义了路由表用于执行不同的 HTTP 请求动作。
可以通过向模板传递参数来动态渲染 HTML 页面。

安装 Express
安装 Express 并将其保存到依赖列表中：
npm install express -S

以上命令会将 Express 框架安装在当前目录的 node_modules 目录中， node_modules 目录下会自动创建 express 目录。以下几个重要的模块是需要与 express 框架一起安装的：

body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。
cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
multer - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

请求和响应
Express 应用使用回调函数的参数： request 和 response 对象来处理请求和响应的数据。

app.get('/', function (req, res) {
   // --
})
Request 对象 - request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性
Response 对象 - response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据

路由
我们已经了解了 HTTP 请求的基本应用，而路由决定了由谁(指定脚本)去响应客户端请求。
在HTTP请求中，我们可以通过路由提取出请求的URL以及GET/POST参数。

静态文件
Express 提供了内置的中间件 express.static 来设置静态文件如：图片， CSS, JavaScript 等。
可以使用 express.static 中间件来设置静态文件路径。
例如，如果你将图片， CSS, JavaScript 文件放在 public 目录下，可以这么写：
app.use('/public', express.static('public'));








const http = require('http');
const fs = require('fs');
const url = require('url');
// querystring 模块提供用于解析和格式化 URL 查询字符串的实用工具
const querystring = require('querystring');
http.createServer(function(req,res){
    res.writeHead(200,{
        "Content-type":"text/plain;charset=utf8"   // 不需要空格
    })
    res.write("世界晚安");
    res.end();
}).listen(8888,()=>{
    console.log('running...');
})
fs.readFile('input.txt',function(err,data){
    if(err) return console.error(err);
    console.log(data.toString());
})

<!-- db.test.insert({name:"A",sp:{type:"Point",coordinates:[105.754,41.689]}})
db.test.insert({name:"B",sp:{type:"Point",coordinates:[105.304,41.783]}})
db.test.insert({name:"C",sp:{type:"Point",coordinates:[105.084,41.389]}})
db.test.insert({name:"D",sp:{type:"Point",coordinates:[105.128,41.285]}})
db.test.insert({name:"E",sp:{type:"Point",coordinates:[106.128,42.086]}})
db.test.insert({name:"F",sp:{type:"Point",coordinates:[105.431,42.009]}})
db.test.insert({name:"G",sp:{type:"Point",coordinates:[104.705,41.921]}}) -->


#### Express 框架的核心是 对HTTP模块的再包装 Express框架等于在http模块之上，加了一个中间层。

### 原生HTTP模块生成服务器
const http = require('http');
http.createServer(function(req,res){
    res.writeHead(200,{
        "Content-type":"text/plain;charset=utf8"   // 不需要空格
    })
    res.write("Hello World");
    res.end();
}).listen(8888,()=>{
    console.log('running...');
})

### Express框架生成服务器
const express = require('express');
const app = express();
app.get('/',function(req,res){
    res.send('Hello World');
}).get('/list',function(req,res){
    res.send('list page');
})
app.listen(8888,function(){
    console.log('running...');
})

### 中间件
中间件（middleware）就是处理HTTP请求的函数。
它最大的特点就是，一个中间件处理完，再传递给下一个中间件。
App实例在运行过程中，会调用一系列的中间件。

每个中间件可以从App实例，接收三个参数，
依次为request对象（代表HTTP请求）、response对象（代表HTTP回应），next回调函数（代表下一个中间件）。
每个中间件都可以对HTTP请求（request对象）进行加工，并且决定是否调用next方法，将request对象再传给下一个中间件。

一个不进行任何操作、只传递request对象的中间件
function uselessMiddleware(req, res, next) {
    next();
}

### use方法
use是express注册中间件的方法，它返回一个函数。

var express = require("express");
var app = express();
app.use("/home", function(request, response, next) {
    response.writeHead(200, { "Content-Type": "text/plain" });
    response.end("Welcome to the homepage!\n");
});
app.use("/about", function(request, response, next) {
    response.writeHead(200, { "Content-Type": "text/plain" });
    response.end("Welcome to the about page!\n");
});
app.use(function(request, response) {
    response.writeHead(404, { "Content-Type": "text/plain" });
    response.end("404 error!\n");
});
app.listen(8888);

### all方法和HTTP动词方法
即HTTP动词都是Express的方法。Express提供post、put、delete、get方法
针对不同的请求，Express提供了use方法的一些别名。

var express = require("express");
var app = express();
app.all("*", function(request, response, next) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  next();
});
app.get("/", function(request, response) {
  response.end("Welcome to the homepage!");
});
app.get("/about", function(request, response) {
  response.end("Welcome to the about page!");
});
app.get("*", function(request, response) {
  response.end("404!");
});
app.listen(8888);

第一个参数都是请求的路径。除了绝对匹配以外，Express允许模式匹配。

### set方法  用于指定变量的值。

app.set("views", __dirname + "/views");

app.set("view engine", "jade");

为系统变量“views”和“view engine”指定值

### response对象

## response.redirect方法  允许网址的重定向。
response.redirect("/hello/anime");
response.redirect("http://www.example.com");
response.redirect(301, "http://www.example.com");

## response.sendFile方法  用于发送文件。
response.sendFile("/path/to/anime.mp4");

## response.render方法  用于渲染网页模板。
app.get("/", function(request, response) {
    response.render("index", { message: "Hello World" });  // render方法，将message变量传入index模板，渲染成HTML网页
});

### requst对象

## request.ip  用于获得HTTP请求的IP地址。

## request.files  用于获取上传的文件。

### 使用Express搭建HTTPs加密服务器

var fs = require('fs');
var options = {
  key: fs.readFileSync('E:/ssl/myserver.key'),
  cert: fs.readFileSync('E:/ssl/myserver.crt'),
  passphrase: '1234'
};
var https = require('https');
var express = require('express');
var app = express();
app.get('/', function(req, res){
  res.send('Hello World Expressjs');
});
var server = https.createServer(options, app);
server.listen(8084);
console.log('Server is running on port 8084');













### Express.Router用法
从Express 4.0开始，路由器功能成了一个单独的组件Express.Router。
它像小型的express应用程序一样，有自己的use、get、param和route方法。

Express.Router是一个构造函数，调用后返回一个路由器实例。
然后，使用该实例的HTTP动词方法，为不同的访问路径，指定回调函数；最后，挂载到某个路径。

var router = express.Router();
router.get('/', function(req, res) {
  res.send('首页');
});
router.get('/about', function(req, res) {
  res.send('关于');
});
app.use('/', router);
上面代码先定义了两个访问路径，然后将它们挂载到根目录。
如果最后一行改为app.use(‘/app’, router)，则相当于为/app和/app/about这两个路径，指定了回调函数。

### router.route方法
router实例对象的route方法，可以接受访问路径作为参数。
var router = express.Router();

router.route('/api')
	.post(function(req, res) {
		// ...
	})
	.get(function(req, res) {
		Bear.find(function(err, bears) {
			if (err) res.send(err);
			res.json(bears);
		});
	});
app.use('/', router);

### router中间件
use方法为router对象指定中间件，即在数据正式发给用户之前，对数据进行处理。

router.use(function(req, res, next) {
	console.log(req.method, req.url);
	next();
});
上面代码中，回调函数的next参数，表示接受其他中间件的调用。函数体中的next()，表示将数据传递给下一个中间件。

注意，中间件的放置顺序很重要，等同于执行顺序。而且，中间件必须放在HTTP动词方法之前，否则不会执行。






app.use(express.static(__dirname + '/public'));

app.get('/', function (req, res) {
  res.send('Hello world!');
});
中间层  中间件
Express允许模式匹配 和 绝对匹配
使用Express搭建HTTPs加密服务器
HTTP动词方法





```
http.createServer(() => {		}).listen(8888);

(req, res) => {
	res.writeHead(200, {'Content-Type': 'text/plain'});
	res.end('Hello World!!!')
}

function(req, res) {
	res.writeHead(200, {'Content-Type': 'text/plain'});
	res.end('Hello World!!!')
}

(req, res) => {	}
function(req, res) {	}
```

```
setTimeOut(function() {
	console.log('123')
}, 1000)

setTimeOut(() => {
	console.log('123')
},1000)
```



## 模块

### 本地安装

```
将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。

可以通过 require() 来引入本地安装的包。
```



### 全局安装

```
将安装包放在 /usr/local 下或者你 node 的安装目录。
可以直接在命令行里使用。
```



```
npm install <Module Name>

npm install express				// 本地安装
npm install express -g		// 全局安装
var express = require('express');
```

## REPL(交互式解释器)

```
Node.js REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。
```

```
Node 自带了交互式解释器，可以执行以下任务：

读取 - 读取用户输入，解析输入的 Javascript 数据结构并存储在内存中。
执行 - 执行输入的数据结构
打印 - 输出结果
循环 - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。

Node 的交互式解释器可以很好的调试 Javascript 代码。
```

## 回调函数

```
Node.js 异步编程的直接体现就是回调。
异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。
回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

例如，我们可以一边读取文件，一边执行其他命令，在文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件 I/O 操作。这就大大提高了 Node.js 的性能，可以处理大量的并发请求。

回调函数一般作为函数的最后一个参数出现：

function foo1(name, age, callback) { }
function foo2(value, callback1, callback2) { }

var data = fs.readFileSync('input.txt');
console.log(data.toString());
console.log('执行完毕');

fs.readFile('input.txt', function(err, data) {
	if(err) return console.log(err);
	console.log(data.toString());
})
console.log('执行完毕');
```

## 事件循环

```
Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。
Node.js 几乎每一个 API 都是支持回调函数的。
Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。
Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.
```

## EventEmitter类

```
events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。
你可以通过require("events");来访问该模块。

// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

// 绑定事件及事件的处理程序
eventEmitter.on('eventName', eventHandler);

// 触发事件
eventEmitter.emit('eventName');
```

## Buffer(缓冲区)

```
JavaScript 语言自身只有字符串数据类型，没有二进制数据类型。

但在处理像TCP流或文件流时，必须使用到二进制数据。因此在 Node.js中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。

在 Node.js 中，Buffer 类是随 Node 内核一起发布的核心库。Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据，每当需要在 Node.js 中处理I/O操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。

在v6.0之前创建Buffer对象直接使用new Buffer()构造函数来创建对象实例，但是Buffer对内存的权限操作相比很大，可以直接捕获一些敏感信息，所以在v6.0以后，官方文档里面建议使用 **Buffer.from()** 接口去创建Buffer对象。
```

```
const buf = Buffer.from('runoob', 'ascii');

// 输出 72756e6f6f62
console.log(buf.toString('hex'));

// 输出 cnVub29i
console.log(buf.toString('base64'));

Node.js 目前支持的字符编码包括：
ascii - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。
utf8 - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。
utf16le - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。
ucs2 - utf16le 的别名。
base64 - Base64 编码。
latin1 - 一种把 Buffer 编码成一字节编码的字符串的方式。
binary - latin1 的别名。
hex - 将每个字节编码为两个十六进制字符。
```

### 创建 Buffer 类

```
Buffer.alloc(size[, fill[, encoding]])： 返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0

Buffer.allocUnsafe(size)： 返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据

Buffer.allocUnsafeSlow(size)

Buffer.from(array)： 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖）

Buffer.from(arrayBuffer[, byteOffset[, length]])： 返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。Buffer.from(buffer)： 复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例

Buffer.from(string[, encoding])： 返回一个被 string 的值初始化的新的 Buffer 实例
```

### 写入缓冲区

```
buf.write(string[, offset[, length]][, encoding])

参数描述如下：

- **string** - 写入缓冲区的字符串。
- **offset** - 缓冲区开始写入的索引值，默认为 0 。
- **length** - 写入的字节数，默认为 buffer.length
- **encoding** - 使用的编码。默认为 'utf8' 。
```

### 从缓冲区读取数据

```
buf.toString([encoding[, start[, end]]])

参数描述如下：

- **encoding** - 使用的编码。默认为 'utf8' 。
- **start** - 指定开始读取的索引位置，默认为 0。
- **end** - 结束位置，默认为缓冲区的末尾。
```

### 将 Buffer 转换为 JSON 对象

```
buf.toJSON()

const json = JSON.stringify(buf);

const copy = JSON.parse(json, (key, value) => {
  return value && value.type === 'Buffer' ?
    Buffer.from(value.data) :
    value;
});
```

### 缓冲区合并

```
Buffer.concat(list[, totalLength])

参数描述如下：
list - 用于合并的 Buffer 对象数组列表。
totalLength - 指定合并后Buffer对象的总长度。

var buffer1 = Buffer.from(('菜鸟教程'));
var buffer2 = Buffer.from(('www.runoob.com'));
var buffer3 = Buffer.concat([buffer1,buffer2]);
console.log("buffer3 内容: " + buffer3.toString());

buffer3 内容: 菜鸟教程www.runoob.com
```

### 缓冲区比较

```
buf.compare(otherBuffer);
```

### 拷贝缓冲区

```
buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])

参数描述如下：
targetBuffer - 要拷贝的 Buffer 对象。
targetStart - 数字, 可选, 默认: 0
sourceStart - 数字, 可选, 默认: 0
sourceEnd - 数字, 可选, 默认: buffer.length

var buf1 = Buffer.from('abcdefghijkl');
var buf2 = Buffer.from('RUNOOB');
//将 buf2 插入到 buf1 指定位置上
buf2.copy(buf1, 2);
console.log(buf1.toString());
```

### 缓冲区裁剪

```
buf.slice([start[, end]])

var buffer1 = Buffer.from('runoob');
// 剪切缓冲区
var buffer2 = buffer1.slice(0,2);
console.log("buffer2 content: " + buffer2.toString());
```

### 缓冲区长度

```
buf.length;

var buffer = Buffer.from('www.runoob.com');
//  缓冲区长度
console.log("buffer length: " + buffer.length);

执行以上代码，输出结果为：
buffer length: 14
```

## Stream(流)

```
Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）。
```

### Stream 有四种流类型

```
- **Readable** - 可读操作。
- **Writable** - 可写操作。
- **Duplex** - 可读可写操作.
- **Transform** - 操作被写入数据，然后读出结果。
```

### 所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：

```
- **data** - 当有数据可读时触发。
- **end** - 没有更多的数据可读时触发。
- **error** - 在接收和写入过程中发生错误时触发。
- **finish** - 所有数据已被写入到底层系统时触发。
```

### 从流中读取数据

```
var fs = require("fs");
var data = '';

// 创建可读流
var readerStream = fs.createReadStream('input.txt');

// 设置编码为 utf8。
readerStream.setEncoding('UTF8');

// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});

readerStream.on('end',function(){
   console.log(data);
});

readerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

### 写入流

```
var fs = require("fs");
var data = '菜鸟教程官网地址：www.runoob.com';

// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');

// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');

// 标记文件末尾
writerStream.end();

// 处理流事件 --> finish、error
writerStream.on('finish', function() {
    console.log("写入完成。");
});

writerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

### 管道流

管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。

```
var fs = require("fs");

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);

console.log("程序执行完毕");
```

### 链式流

```
链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。
```

```
var fs = require("fs");
var zlib = require('zlib');

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
  
console.log("文件压缩完成。");
```

```
var fs = require("fs");
var zlib = require('zlib');

// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input.txt'));
  
console.log("文件解压完成。");
```

## 模块系统

### 引入模块

```
// hello.js
exports.world = function() {
  console.log('Hello World');
}

// index.js
var hello = require('./hello');
hello.world();
```

```
//hello.js 
function Hello() { 
    var name; 
    this.setName = function(thyName) { 
        name = thyName; 
    }; 
    this.sayHello = function() { 
        console.log('Hello ' + name); 
    }; 
}; 
module.exports = Hello;


//main.js 
var Hello = require('./hello'); 
hello = new Hello(); 
hello.setName('BYVoid'); 
hello.sayHello(); 

module.exports = Hello 代替了exports.world = function(){	}
其接口对象就是要输出的 Hello 对象本身，而不是原先的 exports。
```

### 服务端的模块

```
Node.js 中自带了一个叫做 **http** 的模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。
这把我们的本地变量变成了一个拥有所有 http 模块所提供的公共方法的对象。
```

```
var http = require("http");
...
http.createServer(...);
```

```
由于 Node.js 中存在 4 类模块（原生模块和3种文件模块），尽管 require 方法极其简单，但是内部的加载却是十分复杂的，其加载优先级也各自不同。如下图所示：
```

![image-20210205104602319](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210205104602319.png)

```
### 从文件模块缓存中加载
尽管原生模块与文件模块的优先级不同，但是都会优先从文件模块的缓存中加载已经存在的模块。

### 从原生模块加载
原生模块的优先级仅次于文件模块缓存的优先级。require 方法在解析文件名之后，优先检查模块是否在原生模块列表中。以http模块为例，尽管在目录下存在一个 http/http.js/http.node/http.json 文件，require("http") 都不会从这些文件中加载，而是从原生模块中加载。
原生模块也有一个缓存区，同样也是优先从缓存区加载。如果缓存区没有被加载过，则调用原生模块的加载方式进行加载和执行。

### 从文件加载
当文件模块缓存中不存在，而且不是原生模块的时候，Node.js 会解析 require 方法传入的参数，并从文件系统中加载实际的文件，加载过程中的包装和编译细节在前一节中已经介绍过，这里我们将详细描述查找文件模块的过程，其中，也有一些细节值得知晓。

require方法接受以下几种参数的传递：
- http、fs、path等，原生模块。
- ./mod或../mod，相对路径的文件模块。
- /pathtomodule/mod，绝对路径的文件模块。
- mod，非原生模块的文件模块。
```

## 函数

## 路由

## 全局对象

```
它及其所有属性都可以在程序的任何地方访问，即全局变量。
在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性。
```

### 全局对象与全局变量

```
global 最根本的作用是作为全局变量的宿主。
按照 ECMAScript 的定义，满足以下条 件的变量是全局变量：

1、在最外层定义的变量；
2、全局对象的属性；
3、隐式定义的变量（未定义直接赋值的变量）。

当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。
需要注意的是，在 Node.js 中你不可能在最外层定义变量，因为所有用户代码都是属于当前模块的， 而模块本身不是最外层上下文。

注意： 最好不要使用 var 定义变量以避免引入全局变量，因为全局变量会污染命名空间，提高代码的耦合风险。
```

#### __filename

```
__filename 表示当前正在执行的脚本的文件名

console.log(__filename);
```

#### __dirname

```
__dirname 表示当前执行脚本所在的目录。

console.log(__dirname);
```

#### setTimeout(cb, ms)

```
setTimeout(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。：setTimeout() 只执行一次指定函数。
返回一个代表定时器的句柄值。

function printHello(){
   console.log( "Hello, World!");
}
// 两秒后执行以上函数
setTimeout(printHello, 2000);
```

#### clearTimeout(t)

```
clearTimeout( t ) 全局函数用于停止一个之前通过 setTimeout() 创建的定时器。 
参数 t 是通过 setTimeout() 函数创建的定时器。

function printHello(){
   console.log( "Hello, World!");
}
// 两秒后执行以上函数
var t = setTimeout(printHello, 2000);

// 清除定时器
clearTimeout(t);
```

#### setInterval(cb, ms)

```
setInterval(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
返回一个代表定时器的句柄值。可以使用 clearInterval(t) 函数来清除定时器。
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。
```

```
function printHello(){
   console.log( "Hello, World!");
}
// 两秒后执行以上函数
setInterval(printHello, 2000);
```

#### process

```
process 是一个全局变量，即 global 对象的属性。

它用于描述当前Node.js 进程状态的对象，提供了一个与操作系统的简单接口。通常在你写本地命令行程序的时候，少不了要 和它打交道。
```

## 常用工具

```
util 是一个Node.js 核心模块，提供常用函数的集合，用于弥补核心 JavaScript 的功能 过于精简的不足。

const util = require('util');
```

### util.callbackify

```
util.callbackify(original) 将 async 异步函数（或者一个返回值为 Promise 的函数）转换成遵循异常优先的回调风格的函数，
例如将 (err, value) => ... 回调作为最后一个参数。 在回调函数中，第一个参数为拒绝的原因（如果 Promise 解决，则为 null），第二个参数则是解决的值。
```

### util.inherits

```
util.inherits(constructor, superConstructor) 是一个实现对象间原型继承的函数。
JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。JavaScript 没有提供对象继承的语言级别特性，而是通过原型复制来实现的。
```





### util.inspect

```
util.inspect(object,[showHidden],[depth],[colors]) 
是一个将任意对象转换 为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。

showHidden 是一个可选参数，如果值为 true，将会输出更多隐藏信息。
depth 表示最大递归的层数，如果对象很复杂，你可以指定层数以控制输出信息的多少。如果不指定depth，默认会递归 2 层，指定为 null 表示将不限递归层数完整遍历对象。 
如果 colors 值为 true，输出格式将会以 ANSI 颜色编码，通常用于在终端显示更漂亮 的效果。
特别要指出的是，util.inspect 并不会简单地直接把对象转换为字符串，即使该对 象定义了 toString 方法也不会调用。
```

### util.isArray(object)

```
如果给定的参数 "object" 是一个数组返回 true，否则返回 false。
```

### util.isRegExp(object)

```
如果给定的参数 "object" 是一个正则表达式返回true，否则返回false。
```

### util.isDate(object)

```
如果给定的参数 "object" 是一个日期返回true，否则返回false。
```

## 文件系统

```
Node.js 提供一组类似 UNIX（POSIX）标准的文件操作API。 Node 导入文件系统模块(fs)语法如下所示：
var fs = require("fs")
```

### 异步和同步

```
Node.js 文件系统（fs 模块）模块中的方法均有异步和同步版本，例如读取文件内容的函数有异步的 fs.readFile() 和同步的 fs.readFileSync()。
异步的方法函数最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。
建议大家使用异步方法，比起同步，异步方法性能更高，速度更快，而且没有阻塞。
```

### 打开文件

```
fs.open(path, flags[, mode], callback)

参数使用说明如下：

path - 文件的路径。
flags - 文件打开的行为。具体值详见下文。
mode - 设置文件模式(权限)，文件创建默认权限为 0666(可读，可写)。
callback - 回调函数，带有两个参数如：callback(err, fd)。
```

### 获取文件信息

```
fs.stat(path, callback)

参数使用说明如下：

path - 文件路径。
callback - 回调函数，带有两个参数如：(err, stats), stats 是 fs.Stats 对象。

fs.stat(path)执行后，会将stats类的实例返回给其回调函数。可以通过stats类中的提供方法判断文件的相关属性。
```

```
stats.isFile()						如果是文件返回 true，否则返回 false。
stats.isDirectory()				如果是目录返回 true，否则返回 false。
stats.isBlockDevice()			如果是块设备返回 true，否则返回 false。
stats.isCharacterDevice()	如果是字符设备返回 true，否则返回 false。
stats.isSymbolicLink()		如果是软链接返回 true，否则返回 false。
stats.isFIFO()						如果是FIFO，返回true，否则返回 false。FIFO是UNIX中的一种特殊类型的命令管道。
stats.isSocket()					如果是 Socket 返回 true，否则返回 false。
```

### 写入文件

```
fs.writeFile(file, data[, options], callback)

参数使用说明如下：

file - 文件名或文件描述符。
data - 要写入文件的数据，可以是 String(字符串) 或 Buffer(缓冲) 对象。
options - 该参数是一个对象，包含 {encoding, mode, flag}。默认编码为 utf8, 模式为 0666 ， flag 为 'w'
callback - 回调函数，回调函数只包含错误信息参数(err)，在写入失败时返回。
```

### 读取文件

```
fs.read(fd, buffer, offset, length, position, callback)

参数使用说明如下：

fd - 通过 fs.open() 方法返回的文件描述符。
buffer - 数据写入的缓冲区。
offset - 缓冲区写入的写入偏移量。
length - 要从文件中读取的字节数。
position - 文件读取的起始位置，如果 position 的值为 null，则会从当前文件指针的位置读取。
callback - 回调函数，有三个参数err, bytesRead, buffer，err 为错误信息， bytesRead 表示读取的字节数，buffer为缓冲区对象。
```

### 关闭文件

```
fs.close(fd, callback)

参数使用说明如下：

fd - 通过 fs.open() 方法返回的文件描述符。
callback - 回调函数，没有参数。
```

### 截取文件

```
fs.ftruncate(fd, len, callback)

参数使用说明如下：

fd - 通过 fs.open() 方法返回的文件描述符。
len - 文件内容截取的长度。
callback - 回调函数，没有参数。
```

### 删除文件

```
fs.unlink(path, callback)

参数使用说明如下：

path - 文件路径。
callback - 回调函数，没有参数。
```

### 创建目录

```
fs.mkdir(path[, options], callback)

参数使用说明如下：

path - 文件路径。
options 参数可以是：
	recursive - 是否以递归的方式创建目录，默认为 false。
	mode - 设置目录权限，默认为 0777。
callback - 回调函数，没有参数。
```

### 读取目录

```
fs.readdir(path, callback)

参数使用说明如下：

path - 文件路径。
callback - 回调函数，回调函数带有两个参数err, files，err 为错误信息，files 为 目录下的文件数组列表。
```

### 删除目录

```
fs.rmdir(path, callback)

参数使用说明如下：

path - 文件路径。
callback - 回调函数，没有参数。
```

## GET/POST请求

### 获取GET请求内容

```
由于GET请求直接被嵌入在路径中，URL是完整的请求路径，包括了?后面的部分，因此你可以手动解析后面的内容作为GET请求的参数。
node.js 中 url 模块中的 parse 函数提供了这个功能。
```

```
var http = require('http');
var url = require('url');
var util = require('util');
 
http.createServer(function(req, res){
    res.writeHead(200, {'Content-Type': 'text/plain; charset=utf-8'});
    res.end(util.inspect(url.parse(req.url, true)));
}).listen(3000);
```

```
可以使用 url.parse 方法来解析 URL 中的参数

var http = require('http');
var url = require('url');
var util = require('util');
 
http.createServer(function(req, res){
    res.writeHead(200, {'Content-Type': 'text/plain'});
 
    // 解析 url 参数
    var params = url.parse(req.url, true).query;
    res.write("网站名：" + params.name);
    res.write("\n");
    res.write("网站 URL：" + params.url);
    res.end();
 
}).listen(3000);
```

### 获取 POST 请求内容

```
POST 请求的内容全部的都在请求体中，http.ServerRequest 并没有一个属性内容为请求体，原因是等待请求体传输可能是一件耗时的工作。

比如上传文件，而很多时候我们可能并不需要理会请求体的内容，恶意的POST请求会大大消耗服务器的资源，所以 node.js 默认是不会解析请求体的，当你需要的时候，需要手动来做。
```

## 工具模块

### OS模块

### Path模块

### Net模块

### DNS模块

### Domain模块

## Web 模块

### Web服务器

```
Web服务器一般指网站服务器，是指驻留于因特网上某种类型计算机的程序，Web服务器的基本功能就是提供Web信息浏览服务。
它只需支持HTTP协议、HTML文档格式及URL，与客户端的网络浏览器配合。

大多数 web 服务器都支持服务端的脚本语言（php、python、ruby）等，并通过脚本语言从数据库获取数据，将结果返回给客户端浏览器。

目前最主流的三个Web服务器是Apache、Nginx、IIS。
```

### 应用架构

![image-20210206140317772](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210206140317772.png)

```
Client - 客户端，一般指浏览器，浏览器可以通过 HTTP 协议向服务器请求数据。

Server - 服务端，一般指 Web 服务器，可以接收客户端请求，并向客户端发送响应数据。

Business - 业务层， 通过 Web 服务器处理应用程序，如与数据库交互，逻辑运算，调用外部程序等。

Data - 数据层，一般由数据库组成。
```

### Node 创建 Web 服务器

```
Node.js 提供了 http 模块，http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块

var http = require('http');
```

## Express 框架

```
Express 是一个简洁而灵活的 node.js Web应用框架, 提供了一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。
使用 Express 可以快速地搭建一个完整功能的网站。

Express 框架核心特性：

可以设置中间件来响应 HTTP 请求。
定义了路由表用于执行不同的 HTTP 请求动作。
可以通过向模板传递参数来动态渲染 HTML 页面。
```

```
cnpm install express --save
cnpm install express -S
```

```
var express = require('express')
var app = express()
app.get('/', (req, res) => {
    res.send('Hello World!!!')
})
var server = app.listen(8888, () => {
    var host = server.address().address
    var port = server.address().port
    console.log("应用实例，访问地址为 http://%s:%s", host, port)
})
```

### 请求和响应

```
Express 应用使用回调函数的参数： request 和 response 对象来处理请求和响应的数据。

app.get('/', function (req, res) {
   // --
})
```

#### Request 对象

```
Request 对象 - request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。常见属性有：

req.app：当callback为外部文件时，用req.app访问express的实例
req.baseUrl：获取路由当前安装的URL路径
req.body / req.cookies：获得「请求主体」/ Cookies
req.fresh / req.stale：判断请求是否还「新鲜」
req.hostname / req.ip：获取主机名和IP地址
req.originalUrl：获取原始请求URL
req.params：获取路由的parameters
req.path：获取请求路径
req.protocol：获取协议类型
req.query：获取URL的查询参数串
req.route：获取当前匹配的路由
req.subdomains：获取子域名
req.accepts()：检查可接受的请求的文档类型
req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
req.get()：获取指定的HTTP请求头
req.is()：判断请求头Content-Type的MIME类型
```

#### Response 对象

```
response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。常见属性有：

res.app：同req.app一样
res.append()：追加指定HTTP头
res.set()在res.append()后将重置之前设置的头
res.cookie(name，value [，option])：设置Cookie
opition: domain / expires / httpOnly / maxAge / path / secure / signed
res.clearCookie()：清除Cookie
res.download()：传送指定路径的文件
res.get()：返回指定的HTTP头
res.json()：传送JSON响应
res.jsonp()：传送JSONP响应
res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
res.redirect()：设置响应的Location HTTP头，并且设置状态码302
res.render(view,[locals],callback)：渲染一个view，同时向callback传递渲染后的字符串，如果在渲染过程中有错误发生next(err)将会被自动调用。callback将会被传入一个可能发生的错误以及渲染后的页面，这样就不会自动输出了。
res.send()：传送HTTP响应
res.sendFile(path [，options] [，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
res.set()：设置HTTP头，传入object可以一次设置多个头
res.status()：设置HTTP状态码
res.type()：设置Content-Type的MIME类型
```

### 路由

```
我们已经了解了 HTTP 请求的基本应用，而路由决定了由谁(指定脚本)去响应客户端请求。

在HTTP请求中，我们可以通过路由提取出请求的URL以及GET/POST参数。
```

### 静态文件

```
Express 提供了内置的中间件 express.static 来设置静态文件如：图片， CSS, JavaScript 等。

可以使用 express.static 中间件来设置静态文件路径。
例如，如果你将图片， CSS, JavaScript 文件放在 public 目录下，你可以这么写：
app.use('/public', express.static('public'));
```

## RESTful API













## 多进程

```
Node.js 是以单线程的模式运行的，但它使用的是事件驱动来处理并发，这样有助于我们在多核 cpu 的系统上创建多个子进程，从而提高性能。

每个子进程总是带有三个流对象：child.stdin, child.stdout 和child.stderr。
他们可能会共享父进程的 stdio 流，或者也可以是独立的被导流的流对象。

Node 提供了 child_process 模块来创建子进程，方法有：

exec - child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。
spawn - child_process.spawn 使用指定的命令行参数创建新进程。
fork - child_process.fork 是 spawn()的特殊形式，用于在子进程中运行的模块，如 fork('./son.js') 相当于 spawn('node', ['./son.js']) 。与spawn方法不同的是，fork会在父进程与子进程之间，建立一个通信管道，用于进程之间的通信。
```

### exec() 方法

```
child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。

exec() 方法返回最大的缓冲区，并等待进程结束，一次性返回缓冲区的内容。

child_process.exec(command[, options], callback)

参数说明如下：

command： 字符串， 将要运行的命令，参数使用空格隔开
options ：对象，可以是：
  cwd ，字符串，子进程的当前工作目录
  env，对象 环境变量键值对
  encoding ，字符串，字符编码（默认： 'utf8'）
  shell ，字符串，将要执行命令的 Shell（默认: 在 UNIX 中为/bin/sh， 在 Windows 中为cmd.exe， Shell 应当能识别 -c开关在 UNIX 中，或 /s /c 在 Windows 中。 在Windows 中，命令行解析应当能兼容cmd.exe）
  timeout，数字，超时时间（默认： 0）
  maxBuffer，数字， 在 stdout 或 stderr 中允许存在的最大缓冲（二进制），如果超出那么子进程将会被杀死 （默认: 200*1024）
  killSignal ，字符串，结束信号（默认：'SIGTERM'）
  uid，数字，设置用户进程的 ID
  gid，数字，设置进程组的 ID
callback ：回调函数，包含三个参数error, stdout 和 stderr。

```

































## JXcore 打包

```
Node.js 是一个开放源代码、跨平台的、用于 服务器端 和 网络应用的运行环境。

JXcore 是一个支持多线程的 Node.js 发行版本，基本不需要对你现有的代码做任何改动就可以直接线程安全地以多线程运行。
```

