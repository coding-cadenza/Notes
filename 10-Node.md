# node面试题



### 说说你对node的理解，优缺点和应用场景

* **是什么**

  1. `Node.js` 是一个开源与跨平台的 `JavaScript` 运行时环境

  2. 在浏览器外运行`V8`引擎（Google Chrome 的内核），利用`事件驱动`、`非阻塞`和`异步输入输出模型`等技术提高性能

  3. 可以理解为 `Node.js` 就是一个服务器端的、非阻塞式I/O的、事件驱动的`JavaScript`运行环境

  4. **非阻塞异步**

     * `Nodejs`采用了非阻塞型`I/O`机制，在做`I/O`操作的时候不会造成任何的阻塞，当完成之后，以事件的形式通知执行操作

       > 例如在执行了访问数据库的代码之后，将立即转而执行其后面的代码，把数据库返回结果的处理代码放在回调函数中，从而提高了程序的执行效率

  5. **事件驱动**

     事件驱动就是当进来一个新的请求的时，请求将会被压入一个事件队列中，然后通过一个循环来检测队列中的事件状态变化，如果检测到有状态变化的事件，那么就执行该事件对应的处理代码，一般都是回调函数

     > 比如读取一个文件，文件读取完毕后，就会触发对应的状态，然后通过对应的回调函数来进行处理

* **优点**

  1. 处理高并发场景性能更佳
  2. 适合I/O密集型应用，应用在运行极限时，CPU占用率仍然比较低，大部分时间是在做 I/O硬盘内存读写操作

* **缺点**

  - 不适合CPU密集型应用
  - 只支持单核CPU，不能充分利用CPU
  - 可靠性低，一旦代码某个环节崩溃，整个系统都崩溃

* **应用场景**

  * 善于`I/O`，不善于计算。因为Nodejs是一个单线程，如果计算（同步）太多，则会阻塞这个线程
  * 大量并发的I/O，应用程序内部并不需要进行非常复杂的处理
  * 与 websocket 配合，开发长连接的实时交互应用程序

  > - 第一大类：用户表单收集系统、后台管理系统、实时交互系统、考试系统、联网软件、高并发量的web应用程序
  > - 第二大类：基于web、canvas等多人联网游戏
  > - 第三大类：基于web的多人实时聊天客户端、聊天室、图文直播
  > - 第四大类：单页面浏览器应用程序
  > - 第五大类：操作数据库、为前端和移动端提供基于`json`的API





### 说说 Node. js 有哪些全局对象？

* **是什么**

  * 在浏览器 `JavaScript` 中，通常`window` 是全局对象， 而 `Nodejs`中的全局对象是 `global`
  * 在`NodeJS`里，是不可能在最外层定义一个变量，因为所有的用户代码都是当前模块的，只在当前模块里可用，但可以通过`exports`对象的使用将其传递给模块外部
  * 所以，在`NodeJS`中，用`var`声明的变量并不属于全局的变量，只在当前模块生效
  * 像上述的`global`全局对象则在全局作用域中，任何全局变量、函数、对象都是该对象的一个属性值

* **有哪些**

  * **真正的全局对象**

    1. **Class:Buffer**

       可以处理二进制以及非`Unicode`编码的数据

    2. **process**

       进程对象，提供有关当前进程的信息和控制

       可以通过该对象获取当前进程的参数

    3. **console**

       用来打印`stdout`和`stderr`

    4. **clearInterval、setInterval**

    5. **clearTimeout、setTimeout**

    6. **global**

       全局命名空间对象，墙面讲到的`process`、`console`、`setTimeout`等都有放到`global`中

       ```js
       console.log(process === global.process) // true
       ```

  * **模块级别的全局变量**

    * **__dirname**

      获取当前文件所在的路径，不包括后面的文件名

    * **__filename**

      获取当前文件所在的路径和文件名称，包括后面的文件名称

    * **exports**

      `module.exports` 用于指定一个模块所导出的内容，即可以通过 `require()` 访问的内容

    * **module**

      对当前模块的引用，通过`module.exports` 用于指定一个模块所导出的内容，即可以通过 `require()` 访问的内容

    * **require**

      用于引入模块、 `JSON`、或本地文件。 可以从 `node_modules` 引入模块。

      可以使用相对路径引入本地模块或`JSON`文件，路径会根据`__dirname`定义的目录名或当前工作目录进行处理



### 说说对 Node 中的 process 的理解？有哪些常用方法

* **是什么**
  * `process` 对象是一个全局变量，提供了有关当前 `Node.js`进程的信息并对其进行控制，作为一个全局变量
  * 我们都知道，进程计算机系统进行资源分配和调度的基本单位，是操作系统结构的基础，是线程的容器
  * 当我们启动一个`js`文件，实际就是开启了一个服务进程，每个进程都拥有自己的独立空间地址、数据栈，像另一个进程无法访问当前进程的变量、数据结构，只有数据通信后，进程之间才可以数据共享
  * 由于`JavaScript`是一个单线程语言，所以通过`node xxx`启动一个文件后，只有一条主线程

* **属性和方法**

  * **process.env：环境变量**

    一般我们会在 `process.env` 上挂载一些变量标识当前的环境。比如最常见的用 `process.env.NODE_ENV` 区分 `development` 和 `production`

  * **process.argv：进程参数**

    - 0: Node 路径（一般用不到，直接忽略）
    - 1: 被执行的 JS 文件路径（一般用不到，直接忽略）
    - 2~n: 真实传入命令的参数

  * **process.nextTick**

    优先级最高哪个微任务

  * process.pid：获取当前进程id

  * process.ppid：当前进程对应的父进程

  * process.cwd`()`：获取当前进程工作目录

  * process.platform：获取当前进程运行的操作系统平台

  * process.uptime()：当前进程已运行时间，例如：pm2 守护进程的 uptime 值

  * 进程事件： process.on(‘uncaughtException’,cb) 捕获异常信息、 process.on(‘exit’,cb）进程退出监听

  * 三个标准流： process.stdout 标准输出、 process.stdin 标准输入、 process.stderr 标准错误输出

  * process.title 指定进程名称，有的时候需要给进程指定一个名称



### 说说对 Node 中的 fs模块的理解? 有哪些常用方法

* **是什么**

  * `fs（filesystem`），该模块提供本地文件的读写能力，基本上是`POSIX`文件操作命令的简单包装。可以说，所有与文件的操作都是通过`fs`核心模块实现

  * 这个模块对所有文件系统操作提供异步（不具有`sync` 后缀）和同步（具有 `sync` 后缀）两种操作方式，而供开发者选择

* **方法**

  1. **fs.readFileSync**

     > 同步读取

     * 第一个参数为读取文件的路径或文件描述符
     * 第二个参数为 options，默认值为 null，其中有 encoding（编码，默认为 null）和 flag（标识位，默认为 r），也可直接传入 encoding
     * 结果为返回文件的内容

  2. **fs.readFile**

     > 异步读取方法

     前两个参数相同与上相同，最后一个参数为回调函数，函数内有两个参数 `err`（错误）和 `data`（数据），该方法没有返回值，回调函数在读取文件成功后执行

  3. **writeFileSync**

     > 同步写入

     * 第一个参数为写入文件的路径或文件描述符
     * 第二个参数为写入的数据，类型为 String 或 Buffer
     * 第三个参数为 options，默认值为 null，其中有 encoding（编码，默认为 utf8）、 flag（标识位，默认为 w）和 mode（权限位，默认为 0o666），也可直接传入 encoding

  4. **writeFile**

     > 异步写入

     前三个参数与上相同，最后一个参数为回调函数，函数内有一个参数 `err`（错误），回调函数在文件写入数据成功后执行，可以通过判断`err`的值来判断写入过程有无错误

  5. appendFileSync

     > 追加写入

  6. appendFile

     > 异步追加写入方法

  7. copyFileSync

     > 文件拷贝

  8. copyFile

     > 异步拷贝

  9. mkdirSync

     > 创建目录

  10. mkdir

      > 异步创建目录



### 说说对 Node 中的 Buffer 的理解？应用场景？

* **是什么**

  * 在`Node`应用中，需要处理网络协议、操作数据库、处理图片、接收上传文件等，在网络流和文件的操作中，要处理大量二进制数据，而`Buffer`就是在内存中开辟一片区域（初次初始化为8KB），用来存放二进制数据
  * 在上述操作中都会存在数据流动，每个数据流动的过程中，都会有一个最小或最大数据量
  * 如果数据到达的速度比进程消耗的速度快，那么少数早到达的数据会处于等待区等候被处理。反之，如果数据到达的速度比进程消耗的数据慢，那么早先到达的数据需要等待一定量的数据到达之后才能被处理
  * 这里的等待区就指的缓冲区（Buffer），它是计算机中的一个小物理单位，通常位于计算机的 `RAM` 中
  * 简单来讲，`Nodejs`不能控制数据传输的速度和到达时间，只能决定何时发送数据，如果还没到发送时间，则将数据放在`Buffer`中，即在`RAM`中，直至将它们发送完毕
  * `Buffer`是用来存储二进制数据，其的形式可以理解成一个数组，数组中的每一项，都可以保存8位二进制：`00000000`，也就是一个字节

  

* **方法**

  `Buffer` 类在全局作用域中，无须`require`导入

  1. **Buffer.from()**

     用于创建Buffer

     ```js
     const b1 = Buffer.from('10','utf8')
     console.log(b1)
     // <Buffer 31 30>   //1的ascall是9
     ```

  2. **Buffer.alloc()**

     ```js
     const b2 = Buffer.alloc(10, 1) // 建立一个长度为10的缓冲区，填充-1
     console.log(b2)
     // <Buffer 01 01 01 01 01 01 01 01 01 01>
     ```

     > 上述`Buffer`使用`toString()`方法后可以变回原来的
     >
     > * 但是解码和编码格式不同会出现乱码
     > * 当toString设定了范围导致字符串被截断的时候，也会出现乱码

* **应用场景**

  1. **I/O操作**

     > 通过流的方式读取和写入文件的时候就是

     ```js
     const fs = require('fs');
     
     const inputStream = fs.createReadStream('input.txt'); // 创建可读流
     const outputStream = fs.createWriteStream('output.txt'); // 创建可写流
     
     inputStream.pipe(outputStream); // 管道读写
     ```

  2. **加密解密**

     一些加密算法中会用到

  3. **zlib.js**

     `zlib.js` 为 `Node.js` 的核心库之一，其利用了缓冲区（`Buffer`）的功能来操作二进制数据流，提供了压缩或解压功能



### 说说对 Node 中的 Stream 的理解？应用场景？

* **是什么**

  * 流(Stream)，是一种数据传输手段，是端到端信息交换的一种方式，是有顺序的，是逐块读取数据、处理内容，用于顺序读取输入或写入输出，以`Buffer`为单位

  * 流的独特之处在于，它`不`像传统的程序那样一次`将一个文件读入内存`，而是逐块读取数据、处理其内容，`而不是将其全部保存在内存中`

  * 流可以分成三部分：source、dest、pipe

    > 在source和dest之间有一个连接的管道pipe,它的基本语法是source.pipe(dest)
    >
    > 就是将资源从source读出，再利用管道放到dest中

* **种类**

  

  在NodeJS，几乎所有的地方都使用到了流的概念，分成四个种类

  1. 可写流：可写入数据的流。

     > 例如 fs.createWriteStream() 可以使用流将数据写入文件

  2. 可读流：可读取数据的流

     > 例如fs.createReadStream() 可以从文件读取内容

  3. 双工流：既可读又可写的流

     > 例如 net.Socket

  4. 转换流：可以在数据写入和读取时修改或转换数据的流

     > 在文件压缩操作中，可以向文件写入压缩数据，并从文件中读取解压数据
     >
     > 如一个 babel，把es6转换为es5

  5. 在NodeJS中HTTP服务器模块中，request 是可读流，response 是可写流。还有fs 模块，能同时处理可读和可写文件流。可读流和可写流都是单向的，比较容易理解，而另外两个是双向的

* **应用场景**

  `stream`的应用场景主要就是处理`IO`操作，而`http`请求和文件操作都属于`IO`操作

  1. **get请求返回文件给客户端**

     使用`stream`流返回文件，`res`也是一个`stream`对象，通过`pipe`管道将文件数据返回

  2. **文件操作**

  ```js
  const server = http.createServer(function (req, res) { 
      const method = req.method; // 获取请求方法 
      if (method === 'GET') { // get 请求 
          const fileName = path.resolve(__dirname, 'data.txt'); 
          let stream = fs.createReadStream(fileName); 
          stream.pipe(res); // 将 res 作为 stream 的 dest 
      } 
  }); 
  server.listen(8000); 
  ```

  


### 说说Node中的EventEmitter? 如何实现一个EventEmitter?

* **是什么**
  * `Node`采用了事件驱动机制，而`EventEmitter`就是`Node`实现事件驱动的基础
  * 在`EventEmitter`的基础上，`Node`几乎所有的模块都继承了这个类，这些模块拥有了自己的事件，可以绑定／触发监听器，实现了异步操作
  * `Node.js` 里面的许多对象都会分发事件，比如 `fs.readStream` 对象会在文件被打开的时候触发一个事件
  * 产生事件的对象都是 `events.EventEmitter` 的实例，这些对象有一个 `eventEmitter.on()` 函数，用于将一个或多个函数绑定到命名事件上

* **怎么用**

  * `Node`的`events`模块只提供了一个`EventEmitter`类，这个类实现了`Node`异步事件驱动架构的基本模式——`观察者模式`

  * 在这种模式中，被观察者(主体)维护着一组其他对象派来(注册)的观察者，有新的对象对主体感兴趣就注册观察者，不感兴趣就取消订阅，主体有更新的话就依次通知观察者们

  * 基本代码

    ```js
    const EventEmitter = require('events')
    
    class MyEmitter extends EventEmitter{}
    const myEmitter = new MyEmitter()
    
    function callback(){
        console.log('触发了event事件')
    }
    
    myEmitter.on('event',callback)
    myEmitter.emit('event')
    myEmitter.removeListener('event',callback)
    myEmitter.emit('event')
    ```

  * 其他常见的方法
    * emitter.addListener/on(eventName, listener) ：添加类型为 eventName 的监听事件到事件数组`尾部`
    * emitter.prependListener(eventName, listener)：添加类型为 eventName 的监听事件到事件数组`头部`
    * emitter.emit(eventName[, ...args])：触发类型为 eventName 的监听事件
    * emitter.removeListener/off(eventName, listener)：移除类型为 eventName 的监听事件
    * emitter.once(eventName, listener)：添加类型为 eventName 的监听事件，以后只能执行一次并删除
    * emitter.removeAllListeners([eventName])： 移除全部类型为 eventName 的监听事件

* **实现**

  ```js
  class EventEmitter{
      constructor(){
          this.events = {} //每个键的值时一个数组 
      }
  
      
      emit(type,...args){
          this.events[type].forEach(item => {
              // 这个apply和那个apply不大一样
              Reflect.apply(item,this,args)
          });
      }
  
      on(type,handler){
          if(!this.events[type]){
              this.events[type] = []
          }
          this.events[type].push(handler)
      }
  
      addListener(type,handler){
          this.on(type,handler)
      }
  
      prependListener(type,handler){
          if(!this.events[type]){
              this.events[type] = []
          }
          this.events[type].unshift(handler)
      }
  
      removeListener(type,handler){
          if(!this.events[type]){
              return 
          }
          this.events[type] = this.events[type].filter(item => item!==handler)
      }
  
      off(type,handler){
          this.removeListener(type,handler)
      }
      
      // 对handler进行包装
      once(type,handler){
          this.on(type,this._onceWrap(type,handler,this))
      }
  
      _onceWrap(type,handler,target){
          const state = {fired:false,handler,type,target} // handler是标志有没有执行过,封装这个是为了传入下面
          // 真正对函数进行包装,返回包装后的函数
          const wrapFn = this._onceWrapper.bind(state)
          state.wrapFn = wrapFn
          return wrapFn  // 返回包装的fn
      }
  
      _onceWrapper(...args){
          if(!this.fired){ // 没执行过的才执行
              this.fired = true
              Reflect.apply(this.handler,this.target,args)
              this.target.off(this.type,this.wrapFn)
          }
      }
  
  }
  ```

  

### 说说对中间件概念的理解

* 中间件（Middleware）是介于应用系统和系统软件之间的一类软件，它使用系统软件所提供的基础服务（功能），衔接网络上应用系统的各个部分或不同的应用，能够达到`资源共享`、`功能共享`的目的
* 在`NodeJS`中，中间件主要是指封装`http`请求细节处理的方法
* 例如在`express`、`koa`等`web`框架中，中间件的本质为一个回调函数，参数包含请求对象、响应对象和执行下一个中间件的函数
* 在这些中间件函数中，我们可以执行业务逻辑代码，修改请求和响应对象、返回响应数据等操



[![q20ftH.png](https://s1.ax1x.com/2022/03/30/q20ftH.png)](https://imgtu.com/i/q20ftH)

* 中间件是从Http请求发起到响应结束过程中的处理方法，通常需要对请求和响应进行处理

  ```js
  const middleware = (req, res, next) => {
    // TODO
    next()
    // TODO
  }
  ```



### 中间是怎么实现的  

* **方式一**

  通过递归的形式，将后续中间件的执行方法传递给当前中间件，在当前中间件执行结束，通过调用next()方法执行后续中间件

  ```js
  // 中间件数组
  const middlewares = [middleware1, middleware2, middleware3]
  
  // 中间件实现
  function run (req, res) {
    const next = () => {
      // 获取中间件数组中第一个中间件
      const middleware = middlewares.shift()
      if (middleware) {
        // next是自己
        middleware(req, res, next)
      }
    }
    next()
  }
  run() // 模拟一次请求发起
  ```

  如果中间件中有异步操作，需要在异步操作的流程结束后再调用next()方法，否则中间件不能按顺序执行

  ```js
  const middleware2 = (req, res, next) => {
    console.log('middleware2 start')
    new Promise(resolve => {
      // 异步操作 
      setTimeout(() => resolve(), 1000)
    }).then(() => {  
      next()
    })
  }
  ```

  

* **方法二** **--著名的洋葱切片模型**

  有些中间件不止需要在业务处理前执行，还需要在业务处理后执行，比如统计时间的日志中间件。在方式一情况下，无法在next()为异步操作时再将当前中间件的其他代码作为回调执行。

  > 也就是说，我们要在next执行完之后再回来执行现在这个中间件的逻辑
  >
  > 比如说我们想知道执行的时间，那么在进入中间件的时候记录时间，在回来的时候还记录时间

  > 虽然express的中间件使用后也可以回来，但是没有数据返回
  
  因此可以将next()方法的后续操作封装成一个Promise对象，中间件内部就可以使用next.then()形式完成业务处理结束后的回调
  
  ```js
  function run (req, res) {
    const next = () => {
      const middleware = middlewares.shift()
      if (middleware) {
        // 将middleware(req, res, next)包装为Promise对象
        return Promise.resolve(middleware(req, res, next))
      }
    }
    next()
  }
  ```
  
  中间件的调用方法改写
  
  ```js
  const middleware1 = (req, res, next) => {
    console.log('middleware1 start')
    // 所有的中间件都应返回一个Promise对象
    // Promise.resolve()方法接收中间件返回的Promise对象，供下层中间件异步控制
    // 将当前逻辑放到后面的中间件结束之后,再去执行现在这个中间件
    return next().then(() => {
      console.log('middleware1 end')
    })
  }
  ```
  
  使用async和await
  
  ```js
  // async函数自动返回Promise对象
  const middleware2 = async (req, res, next) => {
    console.log('middleware2 start')
    await new Promise(resolve => {
      setTimeout(() => resolve(), 1000)
    })
    await next()
    console.log('middleware2 end')
  }
  
  const middleware3 = async (req, res, next) => {
    console.log('middleware3 start')
    await next()
    console.log('middleware3 end')
  }
  ```
  
  

### 介绍一下node的模块是什么

* Node中每个文件模块都是一个对象
* 所有的模块都是 Module 的实例。可以看到，当前模块（module.js）也是 Module 的一个实例。

```js
function Module(id, parent) {
  this.id = id;
  this.exports = {};
  this.parent = parent;
  this.filename = null;
  this.loaded = false;
  this.children = [];
}
module.exports = Module;

var module = new Module(filename, parent);
```



### 介绍一下require的模块加载机制

1. 先计算模块绝对路径
2. 如果模块在缓存里面，则从缓存中取出该模块
3. 按优先级依次寻找并编译执行模块，若找到则将模块推入缓存`Module._caches`中；
4. 输出模块的exports属性即可

```js
// require 其实内部调用 Module._load 方法
Module._load = function(request, parent, isMain) {
  //  计算绝对路径
  var filename = Module._resolveFilename(request, parent);

  //  第一步：如果有缓存，取出缓存
  var cachedModule = Module._cache[filename];
  if (cachedModule) {
    return cachedModule.exports;

  // 第二步：是否为内置模块
  if (NativeModule.exists(filename)) {
    return NativeModule.require(filename);
  }
  
  // 第三步：生成模块实例，存入缓存
  // 这里的Module就是我们上面的1.1定义的Module
  var module = new Module(filename, parent);
  Module._cache[filename] = module;

  // 第四步：加载模块
  // 下面的module.load实际上是Module原型上有一个方法叫Module.prototype.load
  try {
    module.load(filename);
    hadException = false;
  } finally {
    if (hadException) {
      delete Module._cache[filename];
    }
  }

  // 第五步：输出模块的exports属性
  return module.exports;
};

```

### exports.xxx=xxx和Module.exports={}两种模块导出方式有什么区别吗

* 模块最后返回出来出来的是`Module.exports`
* `exports`是node为我们提供的`Module.exports`的一个引用
* 如果模块要返回一个键值对象{}，可以利用`exports`这个已存在的空对象{}，并继续在上面添加新的键值
* 如果返回要返回一个函数或数组，必须直接对`module.exports`对象赋值
* 总的来说就是最后以`Module.exports`值为准



### 怎么看 nodejs 可支持高并发

* **nodejs 的单线程架构模型**

  nodejs 其实并不是真正的单线程架构，因为 nodejs 还有I/O线程存在（网络I/O、磁盘I/O），这些I/O线程是由更底层的 `libuv` 处理，这部分线程对于开发者来说是透明的(看不到的)。 JavaScript 代码永远运行在V8上，是单线程的。所以从开发者的角度上来看 nodejs 是单线程的。

  * **优势**
    1. 只有一个线程，省去了线程间切换的开销
    2. 线程同步的问题，线程冲突的问题的也不需要担心
  * **劣势**
    1. 现在起步都是 4 核，单线程没法充分利用 cpu 的资源
    2. 单线程，一旦崩溃，应用就挂掉了
    3. 因为只能利用一个 cpu ，一旦 cpu 被某个计算一直占用， cpu 得不到释放，后续的请求就会一直被挂起，直接无响应了

* **单线程怎么支持高并发呢？**

  核心就要在于js引擎的事件循环机制

  简单说一下事件循环的核心

  然后给出个结论nodejs是异步非阻塞的，所以能抗住高并发

* **来个栗子吧**

  比如有个客户端请求A进来，需要读取文件，读取文件后将内容整合，最后数据返回给客户端。但在读取文件的时候另一个请求进来了，那处理的流程是怎么样的？

  1. 请求A进入服务器，线程开始处理该请求
  2. A请求需要读取文件，ok，交给文件IO处理，但是处理得比较慢，需要花3秒，这时候 A 请求就挂起（这个词可能不太恰当），等待通知，而等待的实现就是由事件循环机制实现的
  3. 在A请求等待的时候，cpu 是已经被释放的，这时候B请求进来了， cpu 就去处理B请求
  4. 两个请求间，并不存在互相竞争的状态

* **可以给面试官扩展 同步、异步、阻塞、非阻塞 这个几个概念**

  1. **同步**

     在发起一个调用后，在没有得到结果前，该调用不返回，知道调用返回，才往下执行，也就是说调用者等待被调用方返回结果。

  2. **异步**

     在发起一个调用后，调用就直接返回，不等待结果，继续往下执行，而执行的结果是由被调用方通过状态、通知等方式告知调用方，典型的异步编程模型比如 Node.js

  3. **阻塞**

     在等待调用结果时，线程挂起了，不往下执行

  4. **非阻塞**

     与上面相反，当前线程继续往下执行



### 说一下事件循环

* nodejs中提供阻塞和非阻塞的调用方式，比如fs模块中读取文件，可以根据需要使用 readFile（异步） 或者 readFileSync（同步）

* 异步的编程方式，后续代码的执行无需等待此次的执行结束，不会“阻塞”程序的运行，但它同样也会存在一个问题，那就是非阻塞式调用需要**不断的轮询**获取异步调用的执行结果。

* 如果不断轮询获取结果这个过程对系统有一定的性能影响，为了将这个影响降低，libuv中将不断轮询的这个过程放到`线程池`当中，当轮询到结果时，将对应的回调和获取的结果放置到 event loop（事件循环）的某一个队列中，事件循环再来进行下一步的操作

* **事件循环机制的做事情就是用于管理异步API的回调函数什么时候回到主线程中执行**

* nodejs中的事件循环要比 [javascript的事件循环](https://blog.csdn.net/bingbing1128/article/details/118685716)更为复杂一些，一次循环分为以下几个阶段，每个阶段都有一个**事件队列**

  > 1. 定时器(timer): 在这个阶段执行 setTimeout、setInterval的回调函数
  >
  > 2. I/O事件回调阶段(I/O callbacks)：执行上一轮循环中未被执行的一些I/O回调
  >
  > 3. 闲置阶段(idle, prepare)：仅系统内部使用
  >
  > 4. IO轮询(IO poll)：检索新的 I/O 事件; 执行与 I/O 相关的回调比如文件操作，数据库操作
  >    * **如果这个事件队列中没有回调函数，那么事件循环就会在此阶段停留一段事件等待新的IO操作**
  >         * 如果这个队列为空但是`timer`或者`check`阶段有任务，就不会等待
  >    
  >    5. 检测阶段(check)：setImmediate() 回调函数在这里执行。
  > 
  >6. 关闭的回调函数阶段(close callbacks)：一些与关闭事件相关的回调函数，如：socket.on('close', ...)
  > 
  >7. 回到timer
  
* nodejs中也和javascript中一样存在着微任务（micro-task）、宏任务（macro-task），两个任务中执行的内容也有一部分的相似性。执行顺序也和javascript中一致。

  > 微任务：promise的then函数的回调、queueMicrotask、process.nextTick
  > 宏任务: setTimeout、setInterval、io事件、setImmediate、close事件

  > 微任务队列(有优先级概念)
  > next tick queue：`process.nextTick`
  > other tick queue：`promise的then函数、queueMicrotask`
  >
  > 宏任务队列(无优先级概念，按事件循环执行)
  > timer queue: setTimeout、setInterval
  > poll queue: io事件
  > check queue: setImmediate
  > close queue: close事件 

  当微任务队列中存在回调函数的时候，事件循环在执行完当前阶段的回调函数后会暂停进入事件循环的下一个阶段，事件循环会立即进入微任务的事件队列中开始执行回调函数，完成后进入事件循环的下一个阶段

* 当主线程代码已经完成后再开始事件循环，否则只是将任务放到队列中

* **题目**

  > 这题有两种情况，因为`setTimeout`会被强行变为一秒
  >
  > 所以，如果同步代码的运行时间超过一秒，那么结果就是不同的

  ```js
  setTimeout(() => {
    console.log("setTimeout");
  }, 0);
  
  setImmediate(() => {
    console.log("setImmediate");
  });
  ```

  

  

### nodejs为什么要引入process.nexttick

* 提供高优先级任务的插队方式，在nodejs事件循环的每一个阶段结束后，都能立即执行process.nextTick所注册的回调



### 说说npm模块安装机制

1. 发出`npm install`命令
2. npm向`registy（就是那个地址，配置镜像那个）`查询模块压缩包的网址
3. 下载压缩包，放在跟根目录的.npm目录里
4. 解压压缩包到当前项目的node_moudules
5. 如果当前项目有这个包，就会更新



### Nodejs种多进程如何创建子进程

child_process 模块赋予了node可以随意创建子进程的能力 ，它提供了4个方法用于创建子进程：

* **spawn(): 启动一个子进程来执行`命令`**

  要通过监听事件来获取返回结果。所以结果其实最后还是异步得到的

  > `process.argv`第一个值为执行程序的路径，第二个值是被执行文件的路径，第三个值是参数
  >
  > [
  >   'D:\\nodejs\\node.exe',
  >   'C:\\Users\\accjf\\Desktop\\test\\worker.js',
  >   '1'
  > ]

  ```js
  // worker.js
  console.log('子进程‘+process.argv[2]+’结束' )
  
  // main.js
  const cp = require('child_process')
  let ls = cp.spawn('node',['worker.js',1]) // 创建子进程以及传参
  ls.stdout.on('data',function(data){
      console.log(data.toString())
  })
  
  console.log('主进程结束')
  
  // 输出
  // 主进程结束
  // 子进程1结束
  ```

* **exec: 启动一个子进程来执行`命令`**

  与`spawn`不同，它有一个回调函数来获得子进程情况，并且stdout返回来的就是子进程输出内容

  并且`exec`会生成一个新的子`shell`,在这个shell中执行命令

  ```js
  // worker.js
  console.log('子进程‘+process.argv[2]+’结束' )
  
  // main.js
  const cp = require('child_process')
  cp.exec('node worker.js 1', (err, stdout, stderr) => {
      console.log(stdout)
  })
  
  console.log('主进程结束')
  
  // 输出
  // 主进程结束
  // 子进程1结束
  ```

* **execFile():启动一个子进程来执行可执行`文件`**

  与`exec`相比，它是有参数的，而`exec`是直接把参数作为命令一部分

  ```js
  cp.execFile("node",["worker.js",1], function (err, stdout, stderr) {
      console.log(stdout)
  });
  ```

* **fork():与spawn()类似**

  不同点在于它创建Node的子进程只需指定要执行的JavaScript文件模块即可

  ```js
  let ls = cp.fork('worker.js',[1]) // 创建子进程以及传参
  ls.on('data',function(data){ // 这里不用stdout,on
      console.log(data.toString())
  })
  ```

* 区别

  [![LFTIi9.png](https://s1.ax1x.com/2022/04/10/LFTIi9.png)](https://imgtu.com/i/LFTIi9)

* 最后说一下

  > 尽管4种创建子进程的方式有些差别，但事实上后面3种方法都是spawn()的延伸应用

### 请介绍一下 Node 中的内存泄露问题和解决方案

* **原因**

  1. 全局变量：全局变量挂在root对象上，不会被清除掉；

  2. 闭包：如果闭包未释放，就会导致内存泄露；

  3. 事件监听：对同一个事件重复监听，忘记移除（removeListener），将造成内存泄露

     > 通常EventEmitter监听的事件是不自动释放的，所以

* **解决方法**

  如果出现了内存泄露问题，需要检测内存使用情况，对内存泄露的位置进行定位，然后对对应的内存泄露代码进行修复



### 什么是守护进程？Node 如何实现守护进程？

* 守护进程是不依赖终端的进程，不会因为用户退出终端而停止运行的进程

* 创建思路

  1. 创建一个进程A

  2. 在进程A中创建进程B，可以使用`child_process.fork`或者其他方法

  3. 启动子进程式，设置`derached`属性为`true`

     > 这个子进程将会变成进程组的领导,保证子进程在父进程退出后继续运行

  4. 进程`A`退出，进程`B`由`init`进程接管。此时进程`B`为守护进程







### 说说 Node 文件查找的优先级以及 Require 方法的文件查找策略?

* **模块规范**

  `NodeJS`对`CommonJS`进行了支持和实现，让我们在开发`node`的过程中可以方便的进行模块化开发

  * 在Node中每一个js文件都是一个单独的模块
  * 模块中包括CommonJS规范的核心变量：exports、module.exports、require
  * 通过上述变量进行模块化开发

  模块化的核心是导出与导入，在`Node`中通过`exports`与`module.exports`负责对模块中的内容进行导出，通过`require`函数导入其他模块（自定义模块、系统模块、第三方库模块）中的内容

* **查找策略**

  `require`方法接收一下几种参数的传递：

  - 原生模块：http、fs、path等
  - 相对路径的文件模块：./mod或../mod
  - 绝对路径的文件模块：/pathtomodule/mod
  - 目录作为模块：./dirname
  - 非原生模块的文件模块：mod

  其查找如下

  [![OMZxG8.png](https://s1.ax1x.com/2022/05/07/OMZxG8.png)](https://imgtu.com/i/OMZxG8)

* **原生模块**

  而像原生模块这些，通过`require`方法在解析文件名之后，优先检查模块是否在原生模块列表中，如果在则从原生模块中加载

* **绝对路径、相对路径**

  * 如果`require`绝对路径的文件，则直接查找对应的路径，速度最快
  * 相对路径的模块则相对于当前调用`require`的文件去查找
  * 如果按确切的文件名没有找到模块，则 `NodeJs` 会尝试带上 `.js`、`.json`或 `.node`拓展名再加载

* **目录作为模块**

  默认情况是根据根目录中`package.json`文件的`main`来指定目录模块，如：

  ```js
  { "name" : "some-library",
    "main" : "main.js" }
  ```

  `require('./some-library')` 会试图加载 `./some-library/main.js`

  如果目录里没有 `package.json`文件，或者 `main`入口不存在或无法解析，则会试图加载目录下的 `index.js` 或 `index.node` 文件

* **非原生模块**

  在每个文件中都存在`module.paths`，表示模块的搜索路径，`require`就是根据其来寻找文件

  在`window`下输出如下：

  ![image-20220507085420319](C:\Users\accjf\AppData\Roaming\Typora\typora-user-images\image-20220507085420319.png)

  可以看出`module path`的生成规则为：从当前文件目录开始查找`node_modules`目录；然后依次进入父目录，查找父目录下的`node_modules`目录，依次迭代，直到根目录下的`node_modules`目录

  当都找不到的时候，则会从系统`NODE_PATH`环境变量查找

* **总结**

  文件查找的优先级如下

  - 缓存的模块优先级最高
  - 如果是内置模块，则直接返回，优先级仅次缓存的模块
  - 如果是绝对路径 / 开头，则从根目录找
  - 如果是相对路径 ./开头，则从当前require文件相对位置找
  - 如果文件没有携带后缀，先从js、json、node按顺序查找
  - 如果是目录，则根据 package.json的main属性值决定目录下入口文件，默认情况为 index.js
  - 如果文件为第三方模块，则会引入 node_modules 文件，如果不在当前仓库文件中，则自动从上级递归查找，直到根目录





### 如何实现jwt鉴权机制？说说思路

* **是什么**

  JWT（JSON Web Token），本质就是一个字符串书写规范

  在目前前后端分离的开发过程中，使用`token`鉴权机制用于身份验证是最常见的方案，流程如下：

  - 服务器当验证用户账号和密码正确的时候，给用户颁发一个令牌，这个令牌作为后续用户访问一些接口的凭证
  - 后续访问会根据这个令牌判断用户时候有权限进行访问

  `Token`，分成了三部分，头部（Header）、载荷（Payload）、签名（Signature），并以`.`进行拼接。其中头部和载荷都是以`JSON`格式存放数据，只是进行了编码

  * **header**

    每个JWT都会带有头部信息，这里主要声明使用的算法。声明算法的字段名为`alg`，同时还有一个`typ`的字段，默认`JWT`即可。以下示例中算法为HS256

    ```tsx
    {  "alg": "HS256",  "typ": "JWT" } 
    ```

    因为JWT是字符串，所以我们还需要对以上内容进行Base64编码，编码后字符串如下：

    ```tsx
    eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9  
    ```

  * **payload**

    载荷即消息体，这里会存放实际的内容，也就是`Token`的数据声明，例如用户的`id`和`name`

    默认情况下也会携带令牌的签发时间`iat`，通过还可以设置过期时间，如下

    ```js
    {
      "sub": "1234567890",
      "name": "John Doe",
      "iat": 1516239022
    }
    ```

    同样需要编码

    ```js
    eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ
    ```

  * **Signature**

    签名是对头部和载荷内容进行签名，一般情况，设置一个`secretKey`，对前两个的结果进行`HMACSHA25`算法

    ```js
    Signature = HMACSHA256(base64Url(header)+.+base64Url(payload),secretKey)
    ```

    一旦前面两部分数据被篡改，只要服务器加密用的密钥没有泄露，得到的签名肯定和之前的签名不一致

* **实现**

  token实现分为两部分

  **生成token：登录成功的时候，颁发token**

  借助第三方库`jsonwebtoken`，通过`jsonwebtoken` 的 `sign` 方法生成一个 `token`

  - 第一个参数指的是 Payload
  - 第二个是秘钥，服务端特有
  - 第三个参数是 option，可以定义 token 过期时间

  ```js
  const crypto = require("crypto"),
    jwt = require("jsonwebtoken");
  // TODO:使用数据库
  // 这里应该是用数据库存储，这里只是演示用
  let userList = [];
  
  class UserController {
    // 用户登录
    static async login(ctx) {
      const data = ctx.request.body;
      if (!data.name || !data.password) {
        return ctx.body = {
          code: "000002", 
          message: "参数不合法"
        }
      }
      const result = userList.find(item => item.name === data.name && item.password === crypto.createHash('md5').update(data.password).digest('hex'))
      if (result) {
        // 生成token
        const token = jwt.sign(  
          {
            name: result.name
          },
          "test_token", // secret
          { expiresIn: 60 * 60 } // 过期时间：60 * 60 s
        );
        return ctx.body = {
          code: "0",
          message: "登录成功",
          data: {
            token
          }
        };
      } else {
        return ctx.body = {
          code: "000002",
          message: "用户名或密码错误"
        };
      }
    }
  }
  
  module.exports = UserController;
  ```

  

  **验证token：访问某些资源或者接口时，验证token**

  使用 `koa-jwt` 中间件进行验证，方式比较简单

  ```js
  / 注意：放在路由前面
  app.use(koajwt({
    secret: 'test_token'
  }).unless({ // 配置白名单
    path: [/\/api\/register/, /\/api\/login/]
  }))
  ```

  获取信息

  ```js
  router.get('/api/userInfo',async (ctx,next) =>{
      const authorization =  ctx.header.authorization // 获取jwt
      const token = authorization.replace('Beraer ','')
      const result = jwt.verify(token,'test_token')
      ctx.body = result
  ```

  

* **优缺**
  - json具有通用性，所以可以跨语言
  - 组成简单，字节占用小，便于传输
  - 服务端无需保存会话信息，很容易进行水平扩展
  - 一处生成，多处使用，可以在分布式系统中，解决单点登录问题
  - 可防护CSRF攻击

* **缺点**

  - payload部分仅仅是进行简单编码，所以只能用于存储逻辑必需的非敏感信息

    > base64是很容易破解的

  - 需要保护好加密密钥，一旦泄露后果不堪设想

  - 为避免token被劫持，最好使用https协议



### 如何实现文件上传？说说你的思路

对于文件上传，我们需要设置请求头为`content-type:multipart/form-data`

如下

> 1. 每个表单项由`———XXX`开始，以`———XXX`结尾
> 2. 而`xxx`是即时生成的字符串，用以确保整个分隔符不会在文件或表单项的内容中出现
> 3. 每个表单项必须包含一个 `Content-Disposition` 头，其他的头信息则为可选项， 比如 `Content-Type`
> 4. `Content-Disposition` 包含了 `type`和 一个名字为`name`的 `parameter`，`type` 是 `form-data`，`name`参数的值则为表单控件（也即 field）的名字，如果是文件，那么还有一个 `filename`参数，值就是文件名
> 5. 至于使用`multipart/form-data`，是因为文件是以二进制的形式存在，其作用是专门用于传输大型二进制数据，效率高

```http
POST /t2/upload.do HTTP/1.1
User-Agent: SOHUWapRebot
Accept-Language: zh-cn,zh;q=0.5
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.7
Connection: keep-alive
Content-Length: 60408
Content-Type:multipart/form-data; boundary=ZnGpDtePMx0KrHh_G0X99Yef9r8JZsRJSXC
Host: w.sohu.com

--ZnGpDtePMx0KrHh_G0X99Yef9r8JZsRJSXC
Content-Disposition: form-data; name="city"

Santa colo
--ZnGpDtePMx0KrHh_G0X99Yef9r8JZsRJSXC
Content-Disposition: form-data;name="desc"
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit
 
...
--ZnGpDtePMx0KrHh_G0X99Yef9r8JZsRJSXC
Content-Disposition: form-data;name="pic"; filename="photo.jpg"
Content-Type: application/octet-stream
Content-Transfer-Encoding: binary
 
... binary data of the jpg ...
--ZnGpDtePMx0KrHh_G0X99Yef9r8JZsRJSXC--
```

* 实现

  关于文件的上传的上传，我们可以分成两步骤：

  **文件的上传**

  > 这个就是前端做的事了，把数据设置程formdata就行

  **文件的解析**

  在服务器中，这里采用`koa2`中间件的形式解析上传的文件数据，分别有下面两种形式：

  - **koa-body**

    1. 引入中间件

       ```js
       const koaBody = require('koa-body');
       app.use(koaBody({
           multipart: true,
           formidable: {
               maxFileSize: 200*1024*1024    // 设置上传文件大小最大限制，默认2M
           }
       }));
       ```

    2. 获取上传的文件

       ```js
       const file = ctx.request.files.file; // 获取上传文件
       ```

    3. 写入目录

       ```js
       router.post('/uploadfile', async (ctx, next) => {
         // 上传单个文件
         const file = ctx.request.files.file; // 获取上传文件
         // 创建可读流
         const reader = fs.createReadStream(file.path);
         let filePath = path.join(__dirname, 'public/upload/') + `/${file.name}`;
         // 创建可写流
         const upStream = fs.createWriteStream(filePath);
         // 可读流通过管道写入可写流
         reader.pipe(upStream);
         return ctx.body = "上传成功！";
       });
       ```

  - **koa-multer**

    ```js
    const storage = multer.diskStorage({
      destination: (req, file, cb) => {
        cb(null, "./upload/")
      },
      filename: (req, file, cb) => {
        cb(null, Date.now() + path.extname(file.originalname))
      }
    })
    ss
    const upload = multer({
      storage
    });
    
    const fileRouter = new Router();
    
    fileRouter.post("/upload", upload.single('file'), (ctx, next) => {
      console.log(ctx.req.file); // 获取文件
    })
    
    app.use(fileRouter.routes());
    ```

    

