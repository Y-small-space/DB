# NodeJS总结

## 1 说说你对 Node.js 的理解

### 1.1 是什么

Node.js 是一个开源与跨平台的 JavaScript 运行时环境

在浏览器外运行 V8 JavaScript 引擎（Google Chrome 的内核），利用事件驱动、非阻塞和异步输入输出模型等技术提高性能

可以理解为 Node.js 就是一个服务器端的、非阻塞式 I/O 的、事件驱动的 JavaScript 运行环境

#### 非阻塞异步

Nodejs 采用了非阻塞型 I/O 机制，在做 I/O 操作的时候不会造成任何的阻塞，当完成之后，以事件的形式通知执行操作

例如在执行了访问数据库的代码之后，将立即转而执行其后面的代码，把数据库返回结果的处理代码放在回调函数中，从而提高了程序的执行效率

#### 事件驱动

事件驱动就是当进来一个新的请求的时，请求将会被压入一个事件队列中，然后通过一个循环来检测队列中的事件状态变化，如果检测到有状态变化的事件，那么就执行该事件对应的处理代码，一般都是回调函数

比如读取一个文件，文件读取完毕后，就会触发对应的状态，然后通过对应的回调函数来进行处理

### 1.2 有缺点

- 优点：

  - 处理高并发场景性能更佳
  - 适合 I/O 密集型应用，值的是应用在运行极限时，CPU 占用率仍然比较低，大部分时间是在做 I/O 硬盘内存读写操作

- 因为 Nodejs 是单线程，带来的缺点有：

  - 不适合 CPU 密集型应用
  - 只支持单核 CPU，不能充分利用 CPU
  - 可靠性低，一旦代码某个环节崩溃，整个系统都崩溃

### 1.3 应用场景

- 借助 Nodejs 的特点和弊端，其应用场景分类如下：

  - 善于 I/O，不善于计算。因为 Nodejs 是一个单线程，如果计算（同步）太多，则会阻塞这个线程
  - 大量并发的 I/O，应用程序内部并不需要进行非常复杂的处理
  - 与 websocket 配合，开发长连接的实时交互应用程序

- 具体场景可以表现为如下：

  - 第一大类：用户表单收集系统、后台管理系统、实时交互系统、考试系统、联网软件、高并发量的 web 应用程序
  - 第二大类：基于 web、canvas 等多人联网游戏
  - 第三大类：基于 web 的多人实时聊天客户端、聊天室、图文直播
  - 第四大类：单页面浏览器应用程序
  - 第五大类：操作数据库、为前端和移动端提供基于 json 的 API

其实，Nodejs 能实现几乎一切的应用，只考虑适不适合使用它

## 2 Node. js 有哪些全局对象

### 2.1 是什么

在浏览器 JavaScript 中，通常 window 是全局对象， 而 Nodejs 中的全局对象是 global

在 NodeJS 里，是不可能在最外层定义一个变量，因为所有的用户代码都是当前模块的，只在当前模块里可用，但可以通过 exports 对象的使用将其传递给模块外部

所以，在 NodeJS 中，用 var 声明的变量并不属于全局的变量，只在当前模块生效

像上述的 global 全局对象则在全局作用域中，任何全局变量、函数、对象都是该对象的一个属性值

### 2.2 有哪些

将全局对象分成两类：

- 真正的全局对象
- 模块级别的全局变量

#### 真正的全局对象

下面给出一些常见的全局对象：

- Class:Buffer
- process
- console
- clearInterval、setInterval
- clearTimeout、setTimeout
- global

##### Class:Buffer

可以处理二进制以及非 Unicode 编码的数据

在 Buffer 类实例化中存储了原始数据。Buffer 类似于一个整数数组，在 V8 堆原始存储空间给它分配了内存

一旦创建了 Buffer 实例，则无法改变大小

##### process

进程对象，提供有关当前进程的信息和控制

包括在执行 node 程序进程时，如果需要传递参数，我们想要获取这个参数需要在 process 内置对象中

启动进程：

```js
node index.js 参数 1 参数 2 参数 3
```

index.js 文件如下：

```js
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
```

输出如下：

```js
/usr/local/bin/node
/Users/mjr/work/node/process-args.js
参数 1
参数 2
参数 3
```

除此之外，还包括一些其他信息如版本、操作系统等

##### console

用来打印 stdout 和 stderr

最常用的输入内容的方式：console.log

```js
console.log("hello");
```

清空控制台：console.clear

```js
console.clear;
```

打印函数的调用栈：console.trace

```js
function test() {
  demo();
}

function demo() {
  foo();
}

function foo() {
  console.trace();
}

test();
```

##### clearInterval、setInterval

设置定时器与清除定时器

```js
setInterval(callback, delay[, ...args])
```

callback 每 delay 毫秒重复执行一次

clearInterval 则为对应发取消定时器的方法

##### clearTimeout、setTimeout

设置延时器与清除延时器

```js
setTimeout(callback,delay[,...args])
```

callback 在 delay 毫秒后执行一次

clearTimeout 则为对应取消延时器的方法

##### global

全局命名空间对象，墙面讲到的 process、console、setTimeout 等都有放到 global 中

```js
console.log(process === global.process); // true
```

#### 模块级别的全局对象

这些全局对象是模块中的变量，只是每个模块都有，看起来就像全局变量，像在命令交互中是不可以使用，包括：

- \_\_dirname
- \_\_filename
- exports
- module
- require

##### \_\_dirname

获取当前文件所在的路径，不包括后面的文件名

从 /Users/mjr 运行 node example.js：

```js
console.log(__dirname);
// 打印: /Users/mjr
```

##### \_\_filename

获取当前文件所在的路径和文件名称，包括后面的文件名称

从 /Users/mjr 运行 node example.js：

```js
console.log(__filename);
// 打印: /Users/mjr/example.js
```

##### exports

module.exports 用于指定一个模块所导出的内容，即可以通过 require() 访问的内容

```js
exports.name = name;
exports.age = age;
exports.sayHello = sayHello;
```

##### module

对当前模块的引用，通过 module.exports 用于指定一个模块所导出的内容，即可以通过 require() 访问的内容

##### require

用于引入模块、 JSON、或本地文件。 可以从 node_modules 引入模块。

可以使用相对路径引入本地模块或 JSON 文件，路径会根据\_\_dirname 定义的目录名或当前工作目录进行处理

## 3 Node 中的 process 的理解

### 3.1 是什么

process 对象是一个全局变量，提供了有关当前 Node.js 进程的信息并对其进行控制，作为一个全局变量

我们都知道，进程计算机系统进行资源分配和调度的基本单位，是操作系统结构的基础，是线程的容器

当我们启动一个 js 文件，实际就是开启了一个服务进程，每个进程都拥有自己的独立空间地址、数据栈，像另一个进程无法访问当前进程的变量、数据结构，只有数据通信后，进程之间才可以数据共享

由于 JavaScript 是一个单线程语言，所以通过 node xxx 启动一个文件后，只有一条主线程

### 3.2 属性与方法

关于 process 常见的属性有如下：

- process.env：环境变量，例如通过 `process.env.NODE_ENV 获取不同环境项目配置信息
- process.nextTick：这个在谈及 EventLoop 时经常为会提到
- process.pid：获取当前进程 id
- process.ppid：当前进程对应的父进程
- process.cwd()：获取当前进程工作目录，
- process.platform：获取当前进程运行的操作系统平台
- process.uptime()：当前进程已运行时间，例如：pm2 守护进程的 uptime 值
- 进程事件： process.on(‘uncaughtException’,cb) 捕获异常信息、 process.on(‘exit’,cb)进程推出监听
- 三个标准流： process.stdout 标准输出、 process.stdin 标准输入、 process.stderr 标准错误输出
- process.title 指定进程名称，有的时候需要给进程指定一个名称

下面再稍微介绍下某些方法的使用：

#### process.cwd()

返回当前 Node 进程执行的目录

一个 Node 模块 A 通过 NPM 发布，项目 B 中使用了模块 A。在 A 中需要操作 B 项目下的文件时，就可以用 process.cwd() 来获取 B 项目的路径

#### process.argv

在终端通过 Node 执行命令的时候，通过 process.argv 可以获取传入的命令行参数，返回值是一个数组：

- 0: Node 路径（一般用不到，直接忽略）
- 1: 被执行的 JS 文件路径（一般用不到，直接忽略）
- 2~n: 真实传入命令的参数

所以，我们只要从 process.argv[2] 开始获取就好了

```js
const args = process.argv.slice(2);
```

#### process.env

返回一个对象，存储当前环境相关的所有信息，一般很少直接用到。

一般我们会在 process.env 上挂载一些变量标识当前的环境。比如最常见的用 process.env.NODE_ENV 区分 development 和 production

在 vue-cli 的源码中也经常会看到 process.env.VUE_CLI_DEBUG 标识当前是不是 DEBUG 模式

#### process.nextTick()

我们知道 NodeJs 是基于事件轮询，在这个过程中，同一时间只会处理一件事情

在这种处理模式下，process.nextTick()就是定义出一个动作，并且让这个动作在下一个事件轮询的时间点上执行

例如下面例子将一个 foo 函数在下一个时间点调用

```js
function foo() {
  console.error("foo");
}

process.nextTick(foo);
console.error("bar");
```

输出结果为 bar、foo

虽然下述方式也能实现同样效果：

```js
setTimeout(foo, 0);
console.log("bar");
```

两者区别在于：

- process.nextTick()会在这一次 event loop 的 call stack 清空后（下一次 event loop 开始前）再调用 callback
- setTimeout()是并不知道什么时候 call stack 清空的，所以何时调用 callback 函数是不确定的

## 4 Node 中的 fs 模块的理解

### 4.1 是什么

fs（filesystem），该模块提供本地文件的读写能力，基本上是 POSIX 文件操作命令的简单包装

可以说，所有与文件的操作都是通过 fs 核心模块实现

导入模块如下：

```js
const fs = require("fs");
```

这个模块对所有文件系统操作提供异步（不具有 sync 后缀）和同步（具有 sync 后缀）两种操作方式，而供开发者选择

### 4.2 文件知识

在计算机中有关于文件的知识：

权限位 mode
标识位 flag
文件描述为 fd

### 4.3 方法

下面针对 fs 模块常用的方法进行展开：

- 文件读取
- 文件写入
- 文件追加写入
- 文件拷贝
- 创建目录

#### 文件读取

##### fs.readFileSync

同步读取，参数如下：

- 第一个参数为读取文件的路径或文件描述符
- 第二个参数为 options，默认值为 null，其中有 encoding（编码，默认为 null）和 flag（标识位，默认为 r），也可直接传入 encoding

结果为返回文件的内容

```js
const fs = require("fs");

let buf = fs.readFileSync("1.txt");
let data = fs.readFileSync("1.txt", "utf8");

console.log(buf); // <Buffer 48 65 6c 6c 6f>
console.log(data); // Hello
```

##### fs.readFile

异步读取方法 readFile 与 readFileSync 的前两个参数相同，最后一个参数为回调函数，函数内有两个参数 err（错误）和 data（数据），该方法没有返回值，回调函数在读取文件成功后执行

```js
const fs = require("fs");

fs.readFile("1.txt", "utf8", (err, data) => {
  if (!err) {
    console.log(data); // Hello
  }
});
```

#### 文件写入

##### writeFileSync

同步写入，有三个参数：

第一个参数为写入文件的路径或文件描述符

第二个参数为写入的数据，类型为 String 或 Buffer

第三个参数为 options，默认值为 null，其中有 encoding（编码，默认为 utf8）、 flag（标识位，默认为 w）和 mode（权限位，默认为 0o666），也可直接传入 encoding

```js
const fs = require("fs");

fs.writeFileSync("2.txt", "Hello world");
let data = fs.readFileSync("2.txt", "utf8");

console.log(data); // Hello world
```

##### writeFile

异步写入，writeFile 与 writeFileSync 的前三个参数相同，最后一个参数为回调函数，函数内有一个参数 err（错误），回调函数在文件写入数据成功后执行

```js
const fs = require("fs");

fs.writeFile("2.txt", "Hello world", (err) => {
  if (!err) {
    fs.readFile("2.txt", "utf8", (err, data) => {
      console.log(data); // Hello world
    });
  }
});
```

#### 文件追加写入

##### appendFileSync

参数如下：

第一个参数为写入文件的路径或文件描述符
第二个参数为写入的数据，类型为 String 或 Buffer
第三个参数为 options，默认值为 null，其中有 encoding（编码，默认为 utf8）、 flag（标识位，默认为 a）和 mode（权限位，默认为 0o666），也可直接传入 encoding

```js
const fs = require("fs");

fs.appendFileSync("3.txt", " world");
let data = fs.readFileSync("3.txt", "utf8");
```

##### appendFile

异步追加写入方法 appendFile 与 appendFileSync 的前三个参数相同，最后一个参数为回调函数，函数内有一个参数 err（错误），回调函数在文件追加写入数据成功后执行

```js
const fs = require("fs");

fs.appendFile("3.txt", " world", (err) => {
  if (!err) {
    fs.readFile("3.txt", "utf8", (err, data) => {
      console.log(data); // Hello world
    });
  }
});
```

#### 文件拷贝

##### copyFileSync

同步拷贝

const fs = require("fs");

fs.copyFileSync("3.txt", "4.txt");
let data = fs.readFileSync("4.txt", "utf8");

console.log(data); // Hello world

##### copyFile

异步拷贝

```js
const fs = require("fs");

fs.copyFile("3.txt", "4.txt", () => {
  fs.readFile("4.txt", "utf8", (err, data) => {
    console.log(data); // Hello world
  });
});
```

#### 创建目录

##### mkdirSync

同步创建，参数为一个目录的路径，没有返回值，在创建目录的过程中，必须保证传入的路径前面的文件目录都存在，否则会抛出异常

```js
// 假设已经有了 a 文件夹和 a 下的 b 文件夹
fs.mkdirSync("a/b/c");
```

##### mkdir

异步创建，第二个参数为回调函数

```js
fs.mkdir("a/b/c", (err) => {
  if (!err) console.log("创建成功");
});
```

## 5 Node 中的 Buffer 的理解

### 5.1 是什么

在 Node 应用中，需要处理网络协议、操作数据库、处理图片、接收上传文件等，在网络流和文件的操作中，要处理大量二进制数据，而 Buffer 就是在内存中开辟一片区域（初次初始化为 8KB），用来存放二进制数据

在上述操作中都会存在数据流动，每个数据流动的过程中，都会有一个最小或最大数据量

如果数据到达的速度比进程消耗的速度快，那么少数早到达的数据会处于等待区等候被处理。反之，如果数据到达的速度比进程消耗的数据慢，那么早先到达的数据需要等待一定量的数据到达之后才能被处理

这里的等待区就指的缓冲区（Buffer），它是计算机中的一个小物理单位，通常位于计算机的 RAM 中

简单来讲，Nodejs 不能控制数据传输的速度和到达时间，只能决定何时发送数据，如果还没到发送时间，则将数据放在 Buffer 中，即在 RAM 中，直至将它们发送完毕

上面讲到了 Buffer 是用来存储二进制数据，其的形式可以理解成一个数组，数组中的每一项，都可以保存 8 位二进制：00000000，也就是一个字节

例如：

```js
const buffer = Buffer.from("why");
```

### 5.2 使用方法

Buffer 类在全局作用域中，无须 require 导入

创建 Buffer 的方法有很多种，我们讲讲下面的两种常见的形式：

- Buffer.from()

- Buffer.alloc()

#### Buffer.from()

```js
const b1 = Buffer.from("10");
const b2 = Buffer.from("10", "utf8");
const b3 = Buffer.from([10]);
const b4 = Buffer.from(b3);

console.log(b1, b2, b3, b4); // <Buffer 31 30> <Buffer 31 30> <Buffer 0a> <Buffer 0a>
```

#### Buffer.alloc()

```js
const bAlloc1 = Buffer.alloc(10); // 创建一个大小为 10 个字节的缓冲区
const bAlloc2 = Buffer.alloc(10, 1); // 建一个长度为 10 的 Buffer,其中全部填充了值为 `1` 的字节
console.log(bAlloc1); // <Buffer 00 00 00 00 00 00 00 00 00 00>
console.log(bAlloc2); // <Buffer 01 01 01 01 01 01 01 01 01 01>
```

在上面创建 buffer 后，则能够 toString 的形式进行交互，默认情况下采取 utf8 字符编码形式，如下

```js
const buffer = Buffer.from("你好");
console.log(buffer);
// <Buffer e4 bd a0 e5 a5 bd>
const str = buffer.toString();
console.log(str);
// 你好
```

如果编码与解码不是相同的格式则会出现乱码的情况，如下：

```js
const buffer = Buffer.from("你好", "utf-8 ");
console.log(buffer);
// <Buffer e4 bd a0 e5 a5 bd>
const str = buffer.toString("ascii");
console.log(str);
// d= e%=
```

当设定的范围导致字符串被截断的时候，也会存在乱码情况，如下：

```js
const buf = Buffer.from("Node.js 技术栈", "UTF-8");

console.log(buf); // <Buffer 4e 6f 64 65 2e 6a 73 20 e6 8a 80 e6 9c af e6 a0 88>
console.log(buf.length); // 17

console.log(buf.toString("UTF-8", 0, 9)); // Node.js �
console.log(buf.toString("UTF-8", 0, 11)); // Node.js 技
```

所支持的字符集有如下：

- ascii：仅支持 7 位 ASCII 数据，如果设置去掉高位的话，这种编码是非常快的
- utf8：多字节编码的 Unicode 字符，许多网页和其他文档格式都使用 UTF-8
- utf16le：2 或 4 个字节，小字节序编码的 Unicode 字符，支持代理对（U+10000 至 U+10FFFF）
- ucs2：utf16le 的别名
- base64：Base64 编码
- latin：一种把 Buffer 编码成一字节编码的字符串的方式
- binary：latin1 的别名，
- hex：将每个字节编码为两个十六进制字符

### 5.3 应用场景

Buffer 的应用场景常常与流的概念联系在一起，例如有如下：

- I/O 操作
- 加密解密
- zlib.js

#### I/O 操作

通过流的形式，将一个文件的内容读取到另外一个文件

```js
const fs = require("fs");

const inputStream = fs.createReadStream("input.txt"); // 创建可读流
const outputStream = fs.createWriteStream("output.txt"); // 创建可写流

inputStream.pipe(outputStream); // 管道读写
```

#### 加解密

在一些加解密算法中会遇到使用 Buffer，例如 crypto.createCipheriv 的第二个参数 key 为 string 或 Buffer 类型

#### zlib.js

zlib.js 为 Node.js 的核心库之一，其利用了缓冲区（Buffer）的功能来操作二进制数据流，提供了压缩或解压功能

## 6 Node 中的 Stream 的理解

### 6.1 是什么

流（Stream），是一个数据传输手段，是端到端信息交换的一种方式，而且是有顺序的,是逐块读取数据、处理内容，用于顺序读取输入或写入输出

Node.js 中很多对象都实现了流，总之它是会冒数据（以 Buffer 为单位）

它的独特之处在于，它不像传统的程序那样一次将一个文件读入内存，而是逐块读取数据、处理其内容，而不是将其全部保存在内存中

流可以分成三部分：source、dest、pipe

在 source 和 dest 之间有一个连接的管道 pipe,它的基本语法是 source.pipe(dest)，source 和 dest 就是通过 pipe 连接，让数据从 source 流向了 dest

### 6.2 种类

## 7 Node 中的 EventEmitter

### 7.1 概述

Node.js 采用了事件驱动机制，而 EventEmitter 是 Node.js 实现事件驱动的基础。在 EventEmitter 的基础上，Node.js 的许多模块都继承了这个类，赋予了这些模块处理事件的能力。这些模块可以绑定和触发事件监听器，从而实现异步操作。

例如，`fs.readStream`对象会在文件被打开时触发一个事件。这些产生事件的对象都是`events.EventEmitter`的实例，这些对象提供了`eventEmitter.on()`函数，用于将一个或多个函数绑定到命名事件上。

### 7.2 使用方法

Node.js 的`events`模块提供了`EventEmitter`类，该类实现了 Node.js 异步事件驱动架构的基本模式——观察者模式。在这种模式中，被观察者（主体）维护着一组注册的观察者，有新的对象对主体感兴趣就注册观察者，不感兴趣就取消订阅，当主体有更新时通知所有观察者。

**基本代码示例**：

```javascript
const EventEmitter = require("events");

class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();

function callback() {
  console.log("触发了event事件！");
}

myEmitter.on("event", callback);
myEmitter.emit("event");
myEmitter.removeListener("event", callback);
```

**常用方法**：

- `emitter.addListener/on(eventName, listener)`：添加类型为`eventName`的监听事件到事件数组尾部。
- `emitter.prependListener(eventName, listener)`：添加类型为`eventName`的监听事件到事件数组头部。
- `emitter.emit(eventName[, ...args])`：触发类型为`eventName`的监听事件。
- `emitter.removeListener/off(eventName, listener)`：移除类型为`eventName`的监听事件。
- `emitter.once(eventName, listener)`：添加类型为`eventName`的监听事件，仅执行一次并删除。
- `emitter.removeAllListeners([eventName])`：移除全部类型为`eventName`的监听事件。

### 7.3 实现过程

**EventEmitter 类的实现**：

`EventEmitter`是一个构造函数，内部包含一个存放所有事件的对象`events`。

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }
}
```

`events`对象的结构如下：

```javascript
{
  "event1": [f1, f2, f3],
  "event2": [f4, f5],
  ...
}
```

**实现 emit 方法**：

`emit`方法的第一个参数是事件的类型，后续参数是触发事件函数的参数。

```javascript
emit(type, ...args) {
    if (this.events[type]) {
        this.events[type].forEach((item) => {
            Reflect.apply(item, this, args);
        });
    }
}
```

**实现 on、addListener 和 prependListener 方法**：

这些方法用于添加事件监听触发函数。

```javascript
on(type, handler) {
    if (!this.events[type]) {
        this.events[type] = [];
    }
    this.events[type].push(handler);
}

addListener(type, handler) {
    this.on(type, handler);
}

prependListener(type, handler) {
    if (!this.events[type]) {
        this.events[type] = [];
    }
    this.events[type].unshift(handler);
}
```

**实现 removeListener 和 off 方法**：
用于移除事件监听触发函数。

```javascript
removeListener(type, handler) {
    if (!this.events[type]) {
        return;
    }
    this.events[type] = this.events[type].filter(item => item !== handler);
}

off(type, handler) {
    this.removeListener(type, handler);
}
```

**实现 once 方法**：
`once`方法在添加事件监听处理函数时进行封装，利用闭包特性维护当前状态，通过`fired`属性值判断事件函数是否执行过。

```javascript
once(type, handler) {
    this.on(type, this._onceWrap(type, handler, this));
}

_onceWrap(type, handler, target) {
    const state = { fired: false, handler, type, target };
    const wrapFn = this._onceWrapper.bind(state);
    state.wrapFn = wrapFn;
    return wrapFn;
}

_onceWrapper(...args) {
    if (!this.fired) {
        this.fired = true;
        Reflect.apply(this.handler, this.target, args);
        this.target.off(this.type, this.wrapFn);
    }
}
```

**完整代码示例**：

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }

  on(type, handler) {
    if (!this.events[type]) {
      this.events[type] = [];
    }
    this.events[type].push(handler);
  }

  addListener(type, handler) {
    this.on(type, handler);
  }

  prependListener(type, handler) {
    if (!this.events[type]) {
      this.events[type] = [];
    }
    this.events[type].unshift(handler);
  }

  removeListener(type, handler) {
    if (!this.events[type]) {
      return;
    }
    this.events[type] = this.events[type].filter((item) => item !== handler);
  }

  off(type, handler) {
    this.removeListener(type, handler);
  }

  emit(type, ...args) {
    if (this.events[type]) {
      this.events[type].forEach((item) => {
        Reflect.apply(item, this, args);
      });
    }
  }

  once(type, handler) {
    this.on(type, this._onceWrap(type, handler, this));
  }

  _onceWrap(type, handler, target) {
    const state = { fired: false, handler, type, target };
    const wrapFn = this._onceWrapper.bind(state);
    state.wrapFn = wrapFn;
    return wrapFn;
  }

  _onceWrapper(...args) {
    if (!this.fired) {
      this.fired = true;
      Reflect.apply(this.handler, this.target, args);
      this.target.off(this.type, this.wrapFn);
    }
  }
}
```

**测试代码示例**：

```javascript
const ee = new EventEmitter();

// 注册所有事件
ee.once("wakeUp", (name) => {
  console.log(`${name} 1`);
});
ee.on("eat", (name) => {
  console.log(`${name} 2`);
});
ee.on("eat", (name) => {
  console.log(`${name} 3`);
});
const meetingFn = (name) => {
  console.log(`${name} 4`);
};
ee.on("work", meetingFn);
ee.on("work", (name) => {
  console.log(`${name} 5`);
});

ee.emit("wakeUp", "xx");
ee.emit("wakeUp", "xx"); // 第二次没有触发
ee.emit("eat", "xx");
ee.emit("work", "xx");
ee.off("work", meetingFn); // 移除事件
ee.emit("work", "xx"); // 再次工作
```

## 8 Node.js 中的事件循环机制

### 8.1 是什么

Node.js 中的事件循环机制是基于 libuv 实现的，而 libuv 是一个多平台的专注于异步 I/O 的库。与浏览器中的事件循环机制不同，Node.js 的事件循环包含多个阶段，每个阶段有自己的回调队列。事件循环的核心是处理非阻塞的 I/O 操作，使 Node.js 可以高效地进行并发处理。

### 8.2 流程

Node.js 的事件循环分为六个阶段，每个阶段都有对应的一个先进先出的回调队列。事件循环的流程如下：

1. **定时器阶段 (timers)**：

   - 执行`setTimeout`和`setInterval`的回调。

2. **I/O 事件回调阶段 (I/O callbacks)**：

   - 执行延迟到下一个循环迭代的 I/O 回调，即上一轮循环中未被执行的一些 I/O 回调。

3. **闲置阶段 (idle, prepare)**：

   - 仅系统内部使用。

4. **轮询阶段 (poll)**：

   - 检索新的 I/O 事件，执行与 I/O 相关的回调（除了关闭的回调、计时器和`setImmediate()`调度的之外），在适当的时候会在此阶段阻塞。

5. **检查阶段 (check)**：

   - 执行`setImmediate()`的回调函数。

6. **关闭事件回调阶段 (close callbacks)**：
   - 执行一些关闭的回调函数，如`socket.on('close', ...)`。

每个阶段都有一个对应的回调队列。当事件循环进入某个阶段时，将会在该阶段内执行回调，直到队列耗尽或者达到回调的最大数量，然后进入下一个处理阶段。

node 中实现的微任务 , node 中 10 以上的版本执行和浏览器是一样的

一个宏任务执行完毕后会清空所有微任务.

我们调用的 nodeapi 都是交给我们 libuv 库来去实现的，通过阻塞 i/o 来实现异步

通知完成的方式就是事件驱动

```sh
   ┌───────────────────────────┐
┌─>│           timers          │ 放定时器
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │ 上一轮没执行完的在这来执行
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │ 内部使用
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │  文件读写回调再这里来执行
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │ 执行setImmiedate
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │ socket.close()
   └───────────────────────────┘
```

当主栈执行完后 会按照顺序依次执行 timers(setTimeout) -> poll(fs.方法的回调) -> check(setImmediate)

当代码执行完毕后 ，会从 timer-> poll 检测 poll 里面是否都执行完毕了。 检测一下有没有 setImmeidate 如果有则执行 setImmdiate 如果没有则在这里阻塞

node 中只是将宏任务进行了划分划分到了不同的宏任务队列中。微任务也是在每个宏任务执行完毕后 才清空的.

process.nextTick 并不是微任务 ，每个宏任务执行完后会执行 nextTick(比 nextTick 的优先级更高)

### 8.3 其他机制

除了上述 6 个阶段，还存在`process.nextTick`，它不属于事件循环的任何一个阶段，而是优先执行的微任务队列。`process.nextTick`在当前阶段结束后，进入下一个阶段之前执行，类似于插队。

**流程图**：

```plaintext
+------------------+
| Timers           | (setTimeout, setInterval)
+------------------+
| I/O Callbacks    | (I/O, e.g., reading files)
+------------------+
| Idle, Prepare    | (only for internal use)
+------------------+
| Poll             | (retrieve new I/O events)
+------------------+
| Check            | (setImmediate)
+------------------+
| Close Callbacks  | (e.g., socket.on('close'))
+------------------+
```

**宏任务和微任务**：
在 Node.js 中，同样存在宏任务和微任务，与浏览器中的事件循环相似。

**微任务**：

- `process.nextTick`：`next tick queue`
- `Promise`的`then`回调、`queueMicrotask`：`other queue`

**宏任务**：

- `setTimeout`、`setInterval`：`timer queue`
- I/O 事件：`poll queue`
- `setImmediate`：`check queue`
- `close`事件：`close queue`

**执行顺序**：

1. `next tick microtask queue`
2. `other microtask queue`
3. `timer queue`
4. `poll queue`
5. `check queue`
6. `close queue`

#### 示例代码

```javascript
const fs = require("fs");

console.log("Start");

setTimeout(() => {
  console.log("setTimeout");
}, 0);

setImmediate(() => {
  console.log("setImmediate");
});

fs.readFile(__filename, () => {
  console.log("I/O callback");

  setTimeout(() => {
    console.log("setTimeout inside I/O callback");
  }, 0);

  setImmediate(() => {
    console.log("setImmediate inside I/O callback");
  });

  process.nextTick(() => {
    console.log("nextTick inside I/O callback");
  });
});

process.nextTick(() => {
  console.log("nextTick");
});

console.log("End");
```

**执行顺序解释**：

1. `nextTick`和其他微任务（如 Promise 回调）优先于定时器和 I/O 操作。
2. `setTimeout`和`setInterval`在定时器阶段执行。
3. I/O 操作在轮询阶段执行。
4. `setImmediate`在检查阶段执行。
5. `close`事件在关闭回调阶段执行。

### 8.4 总结

Node.js 事件循环机制通过 libuv 实现，分为六个阶段，每个阶段都有一个回调队列。通过合理使用不同的阶段和`process.nextTick`，我们可以实现高效的异步操作和事件处理。理解事件循环的工作原理有助于优化 Node.js 应用的性能和响应能力。

## 9 Node.js 中的中间件概念及其封装

### 9.1 是什么

中间件（Middleware）是介于应用系统和系统软件之间的一类软件，用于处理网络上应用系统的各个部分或不同应用之间的衔接。在 Node.js 中，中间件主要指封装 HTTP 请求细节处理的方法。例如，在 Express 等 web 框架中，中间件本质上是一个回调函数，参数包含请求对象、响应对象和执行下一个中间件的函数。

通过中间件，我们可以执行业务逻辑代码，修改请求和响应对象，并返回响应数据等操作。

### 9.2 封装中间件

Express 是基于 Node.js 的流行 web 框架，通过中间件机制实现各种功能。Express 中间件采用线性模型，每次执行下一个中间件传入两个参数：

- `req`：请求对象
- `res`：响应对象
- `next`：进入下一个要执行的中间件的函数

下面是一些 Express 中间件的示例：

**异步函数的中间件：**

```javascript
app.use(async (req, res, next) => {
  const start = Date.now();
  await next();
  const ms = Date.now() - start;
  console.log(`${req.method} ${req.url} - ${ms}ms`);
});
```

**普通函数的中间件：**

```javascript
app.use((req, res, next) => {
  const start = Date.now();
  next();
  const ms = Date.now() - start;
  console.log(`${req.method} ${req.url} - ${ms}ms`);
});
```

下面是一些常见的中间件封装示例：

**Token 校验中间件：**

```javascript
module.exports = (options) => async (req, res, next) => {
  try {
    const token = req.header("Authorization");
    if (token) {
      try {
        // verify 函数验证 token，并获取用户相关信息
        await verify(token);
      } catch (err) {
        console.error(err);
      }
    }
    await next();
  } catch (err) {
    console.error(err);
  }
};
```

**日志模块中间件：**

```javascript
const fs = require("fs");
module.exports = (options) => async (req, res, next) => {
  const startTime = Date.now();
  const requestTime = new Date();
  await next();
  const ms = Date.now() - startTime;
  const logout = `${req.ip} -- ${requestTime} -- ${req.method} -- ${req.url} -- ${ms}ms`;
  fs.appendFileSync("./log.txt", logout + "\n");
};
```

Express 中有很多第三方的中间件，如`body-parser`、`express.static`等。下面是它们的简单实现示例：

**body-parser：**
`body-parser`中间件用于将 POST 请求和表单提交的查询字符串转换成对象，并挂在`req.body`上。

```javascript
const querystring = require("querystring");

module.exports = function bodyParser() {
  return (req, res, next) => {
    let dataArr = [];

    req.on("data", (data) => dataArr.push(data));

    req.on("end", () => {
      let contentType = req.get("Content-Type");
      let data = Buffer.concat(dataArr).toString();

      if (contentType === "application/x-www-form-urlencoded") {
        req.body = querystring.parse(data);
      } else if (contentType === "application/json") {
        req.body = JSON.parse(data);
      }

      next();
    });
  };
};
```

**express.static：**
`express.static`中间件用于处理静态文件。

```javascript
const fs = require("fs");
const path = require("path");
const mime = require("mime");
const { promisify } = require("util");

const stat = promisify(fs.stat);
const access = promisify(fs.access);

module.exports = function (dir) {
  return async (req, res, next) => {
    let realPath = path.join(dir, req.path);

    try {
      let statObj = await stat(realPath);

      if (statObj.isFile()) {
        res.set("Content-Type", `${mime.getType(realPath)};charset=utf8`);
        fs.createReadStream(realPath).pipe(res);
      } else {
        let filename = path.join(realPath, "index.html");
        await access(filename);
        res.set("Content-Type", "text/html;charset=utf8");
        fs.createReadStream(filename).pipe(res);
      }
    } catch (e) {
      next();
    }
  };
};
```

### 9.3 总结

在实现中间件时，单个中间件应该足够简单且职责单一。中间件的代码编写应该高效，并在必要时通过缓存来优化性能。Express 通过中间件机制实现各种功能，使得 web 应用具备良好的可拓展性和组合性。通过将公共逻辑处理编写在中间件中，可以避免在每个接口回调中重复编写相同的代码，从而减少冗杂代码，过程类似装饰者模式。

## 10 JWT 鉴权机制的实现（基于 Express）

### 10.1 什么是 JWT

JWT（JSON Web Token）是一种用于在用户和服务器之间传递安全信息的字符串格式，主要用于身份验证。它的结构分为三个部分：头部（Header）、载荷（Payload）和签名（Signature），通过点（`.`）连接起来。

1. **Header**: 描述签名的算法和类型，如下：

   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```

   编码后为：`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`

2. **Payload**: 包含实际传输的数据，如用户信息及其权限等。示例如下：

   ```json
   {
     "sub": "1234567890",
     "name": "John Doe",
     "iat": 1516239022
   }
   ```

   编码后为：`eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ`

3. **Signature**: 用于验证消息是否未被篡改。签名算法如下：

   ```plaintext
   HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
   ```

### 10.2 如何实现 JWT 鉴权

JWT 的使用分为两个部分：生成 Token 和验证 Token。

#### 生成 Token

在用户登录成功时，服务器生成一个 Token 并返回给客户端。客户端保存 Token（如在`localStorage`中），并在后续请求中将其放在 HTTP 请求头的`Authorization`字段中。

**用户登录并生成 Token 的代码示例**：

```javascript
const express = require("express");
const bodyParser = require("body-parser");
const crypto = require("crypto");
const jwt = require("jsonwebtoken");

const app = express();
app.use(bodyParser.json());

let userList = []; // 这里模拟用户数据，应使用数据库

app.post("/login", (req, res) => {
  const { name, password } = req.body;
  if (!name || !password) {
    return res.status(400).json({ code: "000002", message: "参数不合法" });
  }
  const user = userList.find(
    (user) =>
      user.name === name &&
      user.password === crypto.createHash("md5").update(password).digest("hex")
  );
  if (user) {
    const token = jwt.sign({ name: user.name }, "secret_key", {
      expiresIn: "1h",
    });
    return res.json({ code: "0", message: "登录成功", data: { token } });
  } else {
    return res
      .status(401)
      .json({ code: "000002", message: "用户名或密码错误" });
  }
});

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```

**前端保存 Token 并在请求中携带**：

```javascript
axios.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  config.headers.common["Authorization"] = "Bearer " + token;
  return config;
});
```

#### 验证 Token

使用`express-jwt`中间件验证 Token：

```javascript
const express = require("express");
const jwt = require("express-jwt");
const jsonwebtoken = require("jsonwebtoken");

const app = express();

app.use(bodyParser.json());

app.use(
  jwt({ secret: "secret_key", algorithms: ["HS256"] }).unless({
    path: ["/login", "/register"],
  })
);

app.get("/api/userInfo", (req, res) => {
  const token = req.headers.authorization.split(" ")[1];
  const user = jsonwebtoken.verify(token, "secret_key");
  res.json(user);
});

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```

在上述代码中：

1. `express-jwt`中间件用于验证 JWT。`unless`方法用于配置不需要验证的路径（如登录和注册）。
2. 在验证通过的请求中，解析 Token 并返回用户信息。

### 10.3 优缺点

#### 优点

1. **跨语言**：JSON 格式具有通用性，可以跨语言传输。
2. **轻量级**：结构简单，字节占用小，便于传输。
3. **无状态**：服务端无需保存会话信息，便于水平扩展。
4. **分布式**：适用于分布式系统中的单点登录（SSO）。
5. **安全性**：通过签名机制确保数据完整性，可防护 CSRF 攻击。

#### 缺点

1. **敏感信息**：Payload 部分只是 Base64 编码，不应存储敏感信息。
2. **密钥保护**：需要保护好签名密钥，一旦泄露，后果严重。
3. **HTTPS**：为避免 Token 被劫持，建议使用 HTTPS 协议。

通过上述步骤，可以实现一个简单的 JWT 鉴权机制，确保用户身份的安全验证。

## 11 CSMoudule

1. 调用的是 require 方法
2. 加载模块 Module.\_load
3. 通过 Module.\_resolveFilename 核心就是给我们的路径添加后缀 （会帮我们转成绝对路径）
4. 如果这个文件被加载过，走缓存，否则再去加载模块
5. 加载模块的核心就是创建一个模块的实例 new Module() -> {id:文件,exports:模块导出结果是什么}
6. 将模块缓存起来
7. 要加载文件要看加载的文件的扩展名是什么.js / .json
8. 根据扩展名找到对应的加载方案 （策略） 加载 js 的策略
9. js 的加载就是读取文件内容
10. 就是给内容包装一个函数，让这个函数执行 （代码里面肯定会给 module.exports 赋值）
