### 什么是前端工程化

**前端工程化**是使用**软件工程的技术**和方法来进行前端的开发流程、技术、工具、经验等规范化、标准化其主要目的**为了提高效率和降低成本**，（即提高开发过程中的开发效率，减少不必要的重复工作时间），而前端工程本质上是软件工程的一种，因此我们应该从软件工程的角度来研究前端工程。



### 如何做"前端工程化"？

前端工程化就是为了让前端开发能够“自成体系”，个人认为主要应该从

* **模块化**

* **组件化**

  从UI拆分下来的**每个包含模板(HTML)+样式(CSS)+逻辑(JS)功能完备的结构单元**，我们称之为**组件**。

* **规范化**

* **自动化**

  前端工程化的很多脏活累活都应该交给自动化工具来完成

### webpack解决了什么问题

* `Webpack` 最初的目标是实现前端项目的模块化，旨在更高效地管理和维护项目中的每一个资源
* 现代前端开发已经变得十分的复杂，所以我们开发过程中会遇到如下的问题，而webpack就能解决下面的问题
  - 需要通过模块化的方式来开发
  - 使用一些高级的特性来加快我们的开发效率或者安全性，比如通过ES6+、TypeScript开发脚本逻辑，通过sass、less等方式来编写css样式代码
  - 监听文件的变化来并且反映到浏览器上，提高开发的效率
  - JavaScript 代码需要模块化，HTML 和 CSS 这些资源文件也会面临需要被模块化的问题
  - 开发完成后我们还需要将代码进行压缩、合并以及其他相关的优化

### webpack是什么

* `webpack` 是一个用于现代`JavaScript`应用程序的静态模块打包工具
* 当 `webpack`处理应用程序时，它会在内部构建一个依赖图，此依赖图对应映射到项目所需的每个模块（不再局限`js`文件），并生成一个或多个 `bundle`



### 说说webpack的构建流程

* `webpack` 的运行流程是一个串行的过程，它的工作流程就是将各个插件串联起来

* 在运行过程中会广播事件，插件只需要监听它所关心的事件，就能加入到这条`webpack`机制中，去改变`webpack`的运作，使得整个系统扩展性良好
* 从启动到结束会依次执行以下三大步骤
  - 初始化流程：从配置文件和 `Shell` 语句中读取与合并参数，并初始化需要使用的插件和配置插件等执行环境所需要的参数
  - 编译构建流程：从 Entry 发出，针对每个 Module 串行调用对应的 Loader 去翻译文件内容，再找到该 Module 依赖的 Module，递归地进行编译处理
  - 输出流程：对编译后的 Module 组合成 Chunk，把 Chunk 转换成文件，输出到文件系统

[![Ll8Wi6.png](https://s1.ax1x.com/2022/04/14/Ll8Wi6.png)](https://imgtu.com/i/Ll8Wi6)





### 什么是loader，解决了什么问题

* `loader` 用于对模块的"源代码"进行转换，在 `import` 或"加载"模块时预处理文件
* `webpack`做的事情，仅仅是分析出各种模块的依赖关系，然后形成资源列表，最终打包生成到指定的文件中 
* 在`webpack`内部中，任何文件都是模块，不仅仅只是`js`文件
* 默认情况下，在遇到`import`或者`require`加载模块的时候，`webpack`只支持对`js` 和 `json` 文件打包
* 像`css`、`sass`、`png`等这些类型的文件的时候，`webpack`则无能为力，这时候就需要配置对应的`loader`进行文件内容的解析
* 当 `webpack` 碰到不识别的模块的时候，`webpack` 会在配置的中查找该文件解析规则
* `loader`支持链式调用，链中的每个`loader`会处理之前已处理过的资源，最终变为`js`代码。顺序为相反的顺序执行

* 常见的loader

  >- style-loader: 将css添加到DOM的内联样式标签style里
  >- css-loader :允许将css文件通过require的方式引入，并返回css代码
  >- less-loader: 处理less
  >- sass-loader: 处理sass
  >- file-loader: 分发文件到output目录并返回相对路径
  >- url-loader：可以处理理 `file-loader` 所有的事情，但是遇到图片格式的模块，可以选择性的把图片转成 `base64` 格式的字符串，并打包到 `js` 中，对小体积的图片比较合适，大图片不合适。
  >- html-minify-loader: 压缩HTML
  >- babel-loader :用babel来转换ES6文件到ES
  >
  >



### 什么是plugin，解决了什么问题

* `plugin`赋予其各种灵活的功能，例如打包优化、资源管理、环境变量注入等，它们会运行在 `webpack` 的不同阶段（钩子 / 生命周期），贯穿了`webpack`整个编译周期

* 目的在于解决`loader` 无法实现的其他事

* 其本质是一个具有`apply`方法`javascript`对象

  > `apply` 方法会被 `webpack compiler`调用，并且在整个编译生命周期都可以访问 `compiler`对象

  ```js
  const pluginName = 'ConsoleLogOnBuildWebpackPlugin';
  
  class ConsoleLogOnBuildWebpackPlugin {
    apply(compiler) {
      // 下面的run就是一个钩子
      compiler.hooks.run.tap(pluginName, (compilation) => {
        console.log('webpack 构建过程开始！');
      });
    }
  }
  
  module.exports = ConsoleLogOnBuildWebpackPlugin;
  ```

* 生命周期钩子有如下
  - entry-option ：初始化 option
  - run
  - compile： 真正开始的编译，在创建 compilation 对象之前
  - compilation ：生成好了 compilation 对象
  - make：从 entry 开始递归分析依赖，准备对每个模块进行 build
  - after-compile： 编译 build 过程结束
  - emit ：在将内存中 assets 内容写到磁盘文件夹之前
  - after-emit ：在将内存中 assets 内容写到磁盘文件夹之后
  - done： 完成所有的编译过程
  - failed： 编译失败的时候

* 常见的plugin

  >* HtmlWebpackPlugin:在打包结束后，自动生成⼀个 `html`文件，并把打包生成的`js` 模块引入到该`html`中
  >
  >  > 可在该插件构造函数配置模板
  >
  >* clean-webpack-plugin：删除（清理）构建目录



### 说说Loader和Plugin的区别

* `loader` 是文件加载器，能够加载资源文件，并对这些文件进行一些处理，诸如编译、压缩等，最终一起打包到指定的文件中

* `plugin` 赋予了 webpack 各种灵活的功能，例如打包优化、资源管理、环境变量注入等，目的是解决 loader 无法实现的其他事

* 在`Webpack` 运行的生命周期中会广播出许多事件，`Plugin` 可以监听这些事件，在合适的时机通过`Webpack`提供的 `API`改变输出结果

* `loader` 运行在打包文件之前

* `plugins`在整个编译周期都起作用

  

## 写一个loader

> 用于回答写过loader吗

> 美团

* 其本质为函数，函数中的 `this` 作为上下文会被 `webpack` 填充，因此我们不能将 `loader`设为一个箭头函数

* 函数接受一个参数，为 `webpack` 传递给 `loader` 的文件源内容，函数中 `this` 是由 `webpack` 提供的对象，能够获取当前 `loader` 所需要的各种信息

* **Loader 工具库**

  先了解两个loader的工具

  * **`loader-utils`** 

    用于获取 loader 的 `options`

  * **`schema-utils`** 

    用于校验 loader 的 `options` 与 `JSON Schema` 结构定义的是否一致

* **`loader`开发准则**

  * **简单易用**。

  * 使用**链式**传递。（由于 loader 是可以被链式调用的，所以请保证每一个 loader 的单一职责）

  * **模块化**的输出。

  * 确保**无状态**。（不要让 loader 的转化中保留之前的状态，每次运行都应该独立于其他编译模块以及相同模块之前的编译结果）

  * 充分使用官方提供的 loader utilities

  * 记录 loader 的依赖。

  * 解析模块依赖关系。
  * 提取通用代码。
  * 避免绝对路径。
  * 使用`peer dependencies`。如果你的`loader`简单包裹另外一个包，你应该把这个包作为一个`peerDependency`引入。



* **同步`loader`和异步`loader`**

  loader之所以有同步和异步之分，是因为有些资源的处理比较耗时，需要异步处理，等待处理完成后再继续执行

  * 异步模式下，用`this.callback()` 返回处理结果，如下：

    ```js
    this.callback(
      err: Error | null,
      content: string | Buffer,
      sourceMap?: SourceMap,
      meta?: any
    );
    ```

    > 第一个参数必须是 Error 或者 null
    >
    > 第二个参数是一个 string 或者 Buffer。
    >
    > 可选的：第三个参数必须是一个可以被这个模块解析的 source map。
    >
    > 可选的：第四个选项，会被 webpack 忽略，可以是任何东西（例如一些元数据）。

  
  * 同步之际返回结果即可





### 需求

* 有类似如下一个`.tpl`文件，里面是一个模板

  ```js
  <div>
      <h1>{{name}}</h1>
      <p>{{age}}</p>
      <p>{{hobby}}</p>
  </div>
  ```

* 在`app.js`中,向模板传递参数，要求返回一个`html`字符串，并可以插入到页面

  ```js
  import tpl from './info.tpl'
  
  // tpl是函数
  const info = {
      name:'cjf',
      age:34,
      hobby:'笛子'
  }
  console.log(tpl(info))
  
  document.querySelector('#app').innerHTML = tpl(info)
  ```

### 需求分析

* 需求就是将模板解析成`html`字符串
* 从`app.js`中可以看出，`info.tpl`里面的内容最终要转换成一个函数返回给`app.js`调用，`app.js`向函数传入参数替换模板中的插值，并返回html字符串
* 我们可以在自己创建的`tpl-loader`中将代码进行转化

### 具体思路

将`info.tpl`文件转换成`ES6`代码字符串,然后使用将该字符串使用`babel-loader`转化并返回对应的函数

> 好像自己不配置也行

​                           [![L3xYF0.png](https://s1.ax1x.com/2022/04/15/L3xYF0.png)](https://imgtu.c      om/i/L3xYF0)

### 配置webpack

```js
/**
 * mode development production
 * entry 入口文件
 * output path filename  打包输出路径
 * devtool source-map
 * module rules loader
 * plugins 插件
 * devServer 开发服务器 
 */
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    mode: 'development',
    entry: resolve(__dirname, 'src/app.js'),
    output: {
        path: resolve(__dirname, 'build'),
        filename: 'app.js'
    },
    devtool: 'source-map',

    // 配置loader的查找路径
    resolveLoader:{
        modules:[
            'node_modules',
            resolve(__dirname,'loaders')
        ],
    },
    
    module: {
        rules: [
            {
                test: /\.tpl$/,
                use: [
                    'babel-loader',   // 用babel-loader处理下面转化的
                    // 配置自己的loader
                     'tpl-loader', // 使用tpl-loader转化
                ]
            }
        ]
    },
    
    // 插件是数组
    plugins:[
        //HtmlWebpackPlugin可以把打包好的文件当成脚本，然后index.html是默认的模板
        new HtmlWebpackPlugin({
            template:resolve(__dirname,'index.html')
        })
    ],
    devServer:{
        port:'3333'
    }
}
```



### 编写loader

* 先把传入的源文件空格删除
* 返回一个`代码字符串`,将这个字符串交给`babel-loader`转换，其实这个字符串就是我们平时写的ES6代码，只不过是以字符串形式传递
* 该代码导出一个函数，函数接收一个参数`options`,则在`app.js`中可以导入该函数，并传递一个`options`
* 在字符串中，要将`tplReplace`变成转化后的函数内部的代码，其实也可以直接调用，但是写入后看起来我们就是真转化了代码罢了

```js
const { tplReplace } = require('../utils/tplReplace')

// 这是一个loader
function tplLoader(source) {
    source = source.replace(/\s+/g, '')  //取出源码中的空格，防止后面用babel错 
    // return后面不要换行
    return `export default (options) => {
     	${tplReplace.toSting()}
        return ('${source}',options)
    }`
}

module.exports = tplLoader
```

* 上述`tplReplace`因为很多地方可能会用到，所以抽离出来了，其本质就是完成替换功能

  ```js
  // 用来转化模板的函数
  function tplReplace(template, replacebject) {
      // replace函数第一个参数是匹配到的字符串
      // 往后n个参数是每个分组对应的子字符串
      // 倒数第二个参数是匹配到的字符串在原字符串中的位置
      // 最后一个是原始字符串
      // 利用了/g之后replace会执行多次
      return template.replace(/\{\{(.*?)\}\}/g, (str, key) => {
          return replacebject[key]
      })
  }
  
  module.exports = {
      tplReplace
  }
  ```

* 经过上述的转化之后，我们在`app.js`中就能从`.sql`文件返回一个函数了
* 我们只用了一个`loader`，就可以写很多简单的模板，这就是`laoder`的魅力

> 其实`.vue`文件就是这样的转化的，只不过更复杂一点



### 新需求

* 在loader的配置中，有一个叫做`log`的配置项，如果为`true`，则需要打印一些东西

  ```js
   module: {
          rules: [
              {
                  test: /\.tpl$/,
                  use: [
                      'babel-loader',   // 用babel-loader处理下面转化的
                      // 配置自己的loader
                      {
                          loader: 'tpl-loader', // 使用tpl-loader转化
                          options: {
                              log: true
                          }
                      }
                  ]
              }
          ]
      },
  ```

* 我们可以利用`getOptions`获取配置项，然后判断即可,再加入字符串中即可

  ```js
  const { tplReplace } = require('../utils/tplReplace')
  const {getOptions} = require('loader-utils')
  // 这是一个loader
  function tplLoader(source) {
      source = source.replace(/\s+/g, '')  //取出源码中的空格，防止后面用babel错 
      
      // 把上下文传到getOptions可以得到laoder的配置
      const {log} = getOptions(this) 
  
      const _log = log ? `console.log('compiled the fie which is from ${this.resourcePath}')`:''
      // return后面不要换行
      return `export default (options) => {
          ${tplReplace.toString()}
          ${_log.toString()}
          return tplReplace('${source}',options)
      }`
  }
  module.exports = tplLoader
  ```




### 编写plugin

* 由于`webpack`基于发布订阅模式，在运行的生命周期中会广播出许多事件，插件通过监听这些事件，就可以在特定的阶段执行自己的插件任务

* `webpack`编译会创建两个核心对象：

  * `compiler`：包含了 webpack 环境的所有的配置信息，包括 options，loader 和 plugin，和 webpack 整个生命周期相关的钩子
  * `compilation`：作为 plugin 内置事件回调函数的参数，包含了当前的`模块资源`、`编译生成资源`、`变化的文件`以及`被跟踪依赖的状态信息`。当检测到一个文件变化，一次新Compilation 将被创建

* 如果自己要实现`plugin`，也需要遵循一定的规范：

  * 插件必须是一个函数或者是一个包含 `apply` 方法的对象，这样才能访问`compiler`实例
  * 传给每个插件的 `compiler` 和 `compilation` 对象都是同一个引用，因此不建议修改
  * 异步的事件需要在插件处理完任务时调用回调函数通知 `Webpack` 进入下一个流程，不然会卡住

* **让我们来写一个简单的示例插件，生成一个叫做 `filelist.md` 的新文件；文件内容是所有构建生成的文件的列表**

  * 插件编写

    ```js
    class FileListPlugin{
    
        // 插件可以传递配置
        constructor(options){}
    
        apply(compiler){
            // emit是生成资源到putput目录之前的插件api
            compiler.hooks.emit.tap('FileListPlugin',(compilation)=>{
                // 在生成文件中，创建一个头部字符串
                let filelist = "In this build:\n\n"
    
                // 遍历所有编译过的资源文件
                // 每个文件的名称都新加一行
                for(let filename in compilation.assets){
                    filelist += `- ${filename} + \n`
                }
    
                // 将这个列表作为一个新的文件资源，插入到webpack的构建中
                compilation.assets['filelist.md']={
                    source:function(){
                        return filelist
                    },
                    size:function(){
                        return filelist.length
                    }
                }
    
            })
    
        }
    }
    
    module.exports = FileListPlugin
    ```

  * 配置

    ```js
    const FileListPlugin = require('./plugins/FileListPlugin')
    //.....
    // 插件是数组
    plugins:[
        //....
        new FileListPlugin()
    ],
    ```



### 说说webpack的热更新是如何做到的？原理是什么？

* **是什么**

  * 模块热替换，指在应用程序运行过程中，替换、添加、删除模块，而无需重新刷新整个应用

  * 我们在应用运行过程中修改了某个模块，通过自动刷新会导致整个应用的整体刷新，那页面中的状态信息都会丢失

  * 如果使用的是 `HMR(Hot Module Replacement)`，就可以实现只将修改的模块实时替换至应用中，不必完全刷新整个应用

  * 在`webpack`中配置开启热模块也非常的简单，如下代码

    ```js
    const webpack = require('webpack')
    module.exports = {
      // ...
      devServer: {
        // 开启 HMR 特性
        hot: true
        // hotOnly: true
      }
    }
    ```

  * 通过上述这种配置，如果我们修改并保存`css`文件，确实能够以不刷新的形式更新到页面中

  * 但是，当我们修改并保存`js`文件之后，页面依旧自动刷新了，这里并没有触发热模块

  * 所以，`HMR`并不像 `Webpack` 的其他特性一样可以开箱即用，需要有一些额外的操作

    

* **原理**

  [![LzRIL4.png](https://s1.ax1x.com/2022/04/30/LzRIL4.png)](https://imgtu.com/i/LzRIL4)

  * Webpack Compile：将 JS 源代码编译成 bundle.js

  * HMR Server：用来将热更新的文件输出给 HMR Runtime

  * Bundle Server：静态资源文件服务器，提供文件访问路径

  * HMR Runtime：socket服务器，会被注入到浏览器，更新文件的变化

  * bundle.js：构建输出的文件

  * 在HMR Runtime 和 HMR Server之间建立 websocket，即图上4号线，用于实时更新文件变化

    * 启动阶段为上图 1 - 2 - A - B

      > 在编写未经过`webpack`打包的源代码后，`Webpack Compile` 将源代码和 `HMR Runtime` 一起编译成 `bundle`文件，传输给`Bundle Server` 静态资源服务器

    * 更新阶段为上图 1 - 2 - 3 - 4

      > 当某一个文件或者模块发生变化时，`webpack`监听到文件变化对文件重新编译打包，编译生成唯一的`hash`值，这个`hash`值用来作为下一次热更新的标识

      > 根据变化的内容生成两个补丁文件：`manifest`（包含了 `hash` 和 `chundId`，用来说明变化的内容）和`chunk.js` 模块

      > 由于`socket`服务器在`HMR Runtime` 和 `HMR Server`之间建立 `websocket`链接，当文件发生改动的时候，服务端会向浏览器推送一条消息，消息包含文件改动后生成的`hash`值

      > 在浏览器接受到这条消息之前，浏览器已经在上一次`socket` 消息中已经记住了此时的`hash` 标识，这时候我们会创建一个 `ajax` 去服务端请求获取到变化内容的 `manifest` 文件

      > `mainfest`文件包含重新`build`生成的`hash`值，以及变化的模块
      >
      > 浏览器根据 `manifest` 文件获取模块变化的内容，从而触发`render`流程，实现局部模块更新

* **总结**
  * 通过`webpack-dev-server`创建两个服务器：提供静态资源的服务（express）和Socket服务
  * express server 负责直接提供静态资源的服务（打包后的资源直接被浏览器请求和解析）
  * socket server 是一个 websocket 的长连接，双方可以通信
  * 当 socket server 监听到对应的模块发生变化时，会生成两个文件.json（manifest文件）和.js文件（update chunk）
  * 通过长连接，socket server 可以直接将这两个文件主动发送给客户端（浏览器）
  * 浏览器拿到两个新的文件后，通过HMR runtime机制，加载这两个文件，并且针对修改的模块进行更新



### 浏览器不能识别jsx文件，需要怎么办

- 配置@bebel/preset-react，用于处理JSX类型的文件，将其转换为JS文件





### 说说webpack proxy工作原理？为什么能解决跨域?

* **是什么**

  * `webpack proxy`，即`webpack`提供的代理服务

  * 基本行为就是接收客户端发送的请求后转发给其他服务器

  * 其目的是为了便于开发者在开发模式下解决跨域问题（浏览器安全策略限制）

  * 想要实现代理首先需要一个中间服务器，`webpack`中提供服务器的工具为`webpack-dev-server`

  * **webpack-dev-server**

    * `webpack-dev-server`是 `webpack` 官方推出的一款开发工具，将自动编译和自动刷新浏览器等一系列对开发友好的功能全部集成在了一起

    * 目的是为了提高开发者日常的开发效率，**只适用在开发阶段**

    * 关于配置方面，在`webpack`配置对象属性中通过`devServer`属性提供，如下：

      ```js
      // ./webpack.config.js
      const path = require('path')
      
      module.exports = {
          // ...
          devServer: {
              contentBase: path.join(__dirname, 'dist'),
              compress: true,
              port: 9000,
              proxy: {
                  '/api/**': {
                      target: 'https://api.github.com',
                      changeOrigin: false,
                      secure: false,
                      pathRewrite: {
                          '^/api': ''
                      }
                  }
              }
              // ...
          }
      }
      ```

    * `devServetr`里面`proxy`则是关于代理的配置，该属性为对象的形式，对象中每一个属性就是一个代理的规则匹配

    * 属性的名称是需要被代理的请求路径前缀，一般为了辨别都会设置前缀为`/api`，值为对应的代理匹配规则，对应如下：

      1. target：表示的是代理到的目标地址

      2. pathRewrite：默认情况下，我们的 /api-hy 也会被写入到URL中，如果希望删除，可以使用pathRewrite

      3. secure：默认情况下不接收转发到https的服务器上，如果希望支持，可以设置为false

      4. changeOrigin：它表示是否更新代理后请求的 headers 中host地址

         > host这个字段不同不会出现跨域的，可改可不改

* **工作原理**

  * `proxy`工作原理实质上是利用`http-proxy-middleware` 这个`http`代理中间件，实现请求转发给其他服务器

  * **栗子**

    在开发阶段，本地地址为`http://localhost:3000`，该浏览器发送一个前缀带有`/api`标识的请求到服务端获取数据，但响应这个请求的服务器只是将请求转发到另一台服务器中

    ```js
    const express = require('express');
    const proxy = require('http-proxy-middleware');
    
    const app = express();
    
    app.use('/api', proxy({target: 'http://www.example.org', changeOrigin: true}));
    app.listen(3000);
    
    // http://localhost:3000/api/foo/bar -> http://www.example.org/api/foo/bar
    ```





### 说说如何借助webpack来优化前端性能？

* **总览**

  - JS代码压缩
  - CSS代码压缩
  - Html文件代码压缩
  - 文件大小压缩
  - 图片压缩
  - Tree Shaking
  - 代码分离
  - 内联 chunk

* **JS代码压缩**

  * 我们可以用`terser`插件帮助我们压缩代码

  * 在`production`模式下,`webpack`默认使用`TerserPlugin`来处理代码

  * 当然我们也可以自定义配置

    > `optimization`主要用来自定义一些优化打包策略
    >
    > `minimize:true`告知 webpack 使用`TerserPlugin`或其它在 `optimization.minimizer`定义的插件压缩 bundle
    >
    > `minimizer`允许你通过提供一个或多个定制过的 `TerserPlugin` 实例，覆盖默认压缩工具(minimizer)

    ```js
    const TerserPlugin = require('terser-webpack-plugin')
    module.exports = {
        ...
        optimization: {
            minimize: true,
            minimizer: [
                new TerserPlugin({
                    parallel: true // 电脑cpu核数-1
                })
            ]
        }
    }
    ```

    > * extractComments：默认值为true，表示会将注释抽取到一个单独的文件中，开发阶段，我们可设置为 false ，不保留注释
    > * parallel：使用多进程并发运行提高构建的速度，默认值是true，并发运行的默认数量： os.cpus().length - 1
    > * terserOptions：设置我们的terser相关的配置：
    > * compress：设置压缩相关的选项，mangle：设置丑化相关的选项，可以直接设置为true
    > * mangle：设置丑化相关的选项，可以直接设置为true
    > * toplevel：底层变量是否进行转换
    > * keep_classnames：保留类的名称
    > * keep_fnames：保留函数的名称

* **CSS代码压缩**

  * `CSS`压缩通常是去除无用的空格等，因为很难去修改选择器、属性的名称、值等
  * CSS的压缩我们可以使用另外一个插件：`css-minimizer-webpack-plugin`

  * 配置和`terser`配置差不多，只是有一些选项不大一样

    ```js
    const CssMinimizerPlugin = require('css-minimizer-webpack-plugin')
    module.exports = {
        // ...
        optimization: {
            minimize: true,
            minimizer: [
                new CssMinimizerPlugin({
                    parallel: true
                })
            ]
        }
    }
    ```

* **Html文件代码压缩**

  在使用`HtmlWebpackPlugin`插件来生成`HTML`的模板时候，通过配置属性`minify`进行`html`优化即可

  ```js
  module.exports = {
      ...
      plugin:[
          new HtmlwebpackPlugin({
              ...
              minify:{
                  minifyCSS:false, // 是否压缩css
                  collapseWhitespace:false, // 是否折叠空格
                  removeComments:true // 是否移除注释
              }
          })
      ]
  }
  ```

* **文件大小压缩**

  对文件的大小进行压缩，减少`http`传输过程中宽带的损耗

  用到`compression-webpack-plugin`插件

  > 这个是真正的压缩，而不是单纯的将代码压缩

  ```js
  new ComepressionPlugin({
      test:/\.(css|js)$/,  // 哪些文件需要压缩
      threshold:500, // 设置文件多大开始压缩
      minRatio:0.7, // 至少压缩的比例
      algorithm:"gzip", // 采用的压缩算法
  })
  ```

* **图片压缩**

  图片压缩主要用到`image-webpack-loader`

* **Tree Shaking**

  消除依赖了但是用不到的代码，比如import了但是没有使用的模块

  有两种不同的方案

  - usedExports：通过标记某些函数是否被使用，之后通过`Terser`来进行优化的

    > 简单配置即可

    ```js
    module.exports = {
        ...
        optimization:{
            usedExports
        }
    }
    ```

  - sideEffects：跳过整个模块/文件，直接查看该文件是否有副作用

    置方法是在`package.json`中设置`sideEffects`属性

    1. 如果`sideEffects`设置为false，就是告知`webpack`可以安全的删除未用到的`exports`

    2. 如果有一些需要保留，可以设置成数组

       ```js
       "sideEffects":[
           "./src/util/format.js",
           "*.css" // 所有的css文件
       ]
       ```

  > css的话可以使用`PurgeCssPlugin`进行treeShaking

  

* **代码分离**

  将代码分离到不同的`bundle`中，之后我们可以按需加载，或者并行加载这些文件

  > 代码分离又分为
  >
  > 1. 入口起点:使用 [`entry`](https://www.webpackjs.com/configuration/entry-context) 配置手动地分离代码
  > 2. 防止重复：使用 [`CommonsChunkPlugin`](https://www.webpackjs.com/plugins/commons-chunk-plugin) 去重和分离 chunk(也就是将共享的chunk分离出去)
  > 3. 动态导入：通过模块的内联函数调用来分离代码

  默认情况下，所有的`JavaScript`代码（业务代码、第三方依赖、暂时没有用到的模块）在首页全部都加载，就会影响首页的加载速度

  通过`splitChunksPlugin`来实现，该插件`webpack`已经默认安装和集成，只需要配置即可，默认配置中，chunks仅仅针对于异步（async）请求，我们可以设置为initial或者all

  ```js
  module.exports = {
      ...
      optimization:{
          splitChunks:{
              chunks:"all"
          }
      }
  }
  ```

* **内联chunk**

  可以通过`InlineChunkHtmlPlugin`插件将一些`chunk`的模块内联到`html`，如`runtime`的代码（对模块进行解析、加载、模块信息相关的代码），代码量并不大，但是必须加载的

  ```js
  const InlineChunkHtmlPlugin = require('react-dev-utils/InlineChunkHtmlPlugin')
  const HtmlWebpackPlugin = require('html-webpack-plugin')
  module.exports = {
      ...
      plugin:[
          new InlineChunkHtmlPlugin(HtmlWebpackPlugin,[/runtime.+\.js/]
  }
  ```

  



### 如何提高webpack的构建速度？

* **背景**

  随着我们的项目涉及到页面越来越多，功能和业务代码也会随着越多，相应的 `webpack` 的构建时间也会越来越久

  构建时间与我们日常开发效率密切相关，当我们本地开发启动 `devServer` 或者 `build` 的时候，如果时间过长，会大大降低我们的工作效率

  所以，优化`webpack` 构建速度是十分重要的环节

* **如何优化**

  常见手段如下

  - 优化 loader 配置
  - 合理使用 resolve.extensions
  - 优化 resolve.modules
  - 优化 resolve.alias
  - 使用 DLLPlugin 插件  `不大清楚`
  - 使用 cache-loader
  - terser 启动多线程
  - 合理使用 sourceMap

* **优化 loader 配置**

  在使用`loader`时，可以通过配置`include`、`exclude`、`test`属性来匹配文件，借助`include`、`exclude`规定哪些匹配应用`loader`

  ```js
  module: {
      // 优化loader配置
      rules: [
          {
              test: /\.js$/,
              // babel-loader 支持缓存转换出的结果，通过 cacheDirectory 选项开启
              use: ['babel-loader?cacheDirectory'],
              // 只对指定目录下的文件采用babel-loader
              include: path.resolve(__dirname, 'src')
          }
  
      ]
  }
  ```

  > 原始时间

  ![OGfllD.png](https://s1.ax1x.com/2022/05/09/OGfllD.png)

  > 缓存后时间

  ![OGf5X4.png](https://s1.ax1x.com/2022/05/09/OGf5X4.png)

  > 指定位置后时间

  ![OGhpBd.png](https://s1.ax1x.com/2022/05/09/OGhpBd.png)



* **合理使用 resolve.extensions**

  `resolve`可以帮助`webpack`从每个 `require/import` 语句中，找到需要引入到合适的模块代码

  通过`resolve.extensions`是解析到文件时自动添加拓展名，默认情况如下

  ```js
  module.exports = {
      // 文件查找扩展名
      resolve:{
          extensions:[".warm",".mjs",".vue",".js",".json"]
      }
  }
  ```

  当我们引入文件的时候，若没有文件后缀名，则会根据数组内的值依次查找

  当我们配置的时候，则`不要随便把所有后缀都写在里面`，这会调用多次文件的查找，这样就会减慢打包速度

* **优化 resolve.modules**

  `resolve.modules` 用于配置 `webpack` 去哪些目录下寻找第三方模块。默认值为`['node_modules']`，所以默认会从`node_modules`中查找文件 当安装的第三方模块都放在项目根目录下的 `./node_modules`目录下时，所以可以指明存放第三方模块的绝对路径，以减少寻找，配置如下

  ```js
  module.exports = {
    resolve: {
      // 使用绝对路径指明第三方模块存放的位置，以减少搜索步骤
      // 其中 __dirname 表示当前工作目录，也就是项目根目录
      modules: [path.resolve(__dirname, 'node_modules')]
    },
  };
  ```

* **优化 resolve.alias**

  `alias`给一些常用的路径起一个别名，特别当我们的项目目录结构比较深的时候，一个文件的路径可能是`./../../`的形式

  通过配置`alias`以减少查找过程

  > `vue-cli`自动配置了

  ```js
  module.exports = {
      ...
      resolve:{
          alias:{
              "@":path.resolve(__dirname,'./src')
          }
      }
  }
  ```

* **使用 cache-loader**

  在一些性能开销较大的 `loader`之前添加 `cache-loader`，以将结果缓存到磁盘里，显著提升二次构建速度

  保存和读取这些缓存文件会有一些时间开销，所以请只对性能开销较大的 `loader` 使用此`loader`

  ```js
  module.exports = {
      module: {
          rules: [
              {
                  test: /\.ext$/,
                  use: ['cache-loader', ...loaders],
                  include: path.resolve('src'),
              },
          ],
      },
  };
  ```

* **terser 启动多线程**

  > 确实很快

  ```js
  module.exports = {
    optimization: {
      minimizer: [
        new TerserPlugin({
          parallel: true,
        }),
      ],
    },
  };
  ```

* **合理使用 sourceMap**

  打包生成 `sourceMap` 的时候，如果信息越详细，打包速度就会越慢



### 除了webpack还知道哪些打包工具

* **Rollup**

  `Rollup` 是一款 `ES Modules` 打包器，从作用上来看，`Rollup` 与 `Webpack` 非常类似。不过相比于 `Webpack`，`Rollup`要小巧的多

  现在很多我们熟知的库都都使用它进行打包，比如：`Vue`、`React`和`three.js`等

  * **优点**
    1. 代码非常简洁，不像`webpack`那样存在大量引导代码和模块函数
    2. 自动`treeSaking`

  * **缺点**

    加载其他类型的资源文件或者支持导入 `CommonJS` 模块，又或是编译 `ES` 新特性，这些额外的需求 `Rollup`需要使用插件去完成

  * **总结**
    * 综合来看，`rollup`并不适合开发应用使用，因为需要使用第三方模块，而目前第三方模块大多数使用`CommonJs`方式导出成员，并且`rollup`不支持`HMR`，使开发效率降低
    * 但是在用于打包`JavaScript` 库时，`rollup`比 `webpack` 更有优势，因为其打包出来的代码更小、更快，其存在的缺点可以忽略

* **Parcel**

  * Parcel ，是一款完全零配置的前端打包器，它提供了 “傻瓜式” 的使用体验，只需了解简单的命令，就能构建前端应用程序

  * `Parcel`不仅打包了应用，同时也启动了一个开发服务器，跟`webpack Dev Server`一样

    跟`webpack`类似，也支持模块热替换，但用法更简单

  * `Parcel`不仅打包了应用，同时也启动了一个开发服务器，跟`webpack Dev Server`一样

    跟`webpack`类似，也支持模块热替换，但用法更简单

  * 同时，`Parcel`能够零配置加载其他类型的资源文件，无须像`webpack`那样配置对应的`loader`

  * 由于打包过程是多进程同时工作，构建速度会比`Webpack` 快，输出文件也会被压缩，并且样式代码也会被单独提取到单个文件中

* **Snowpack**

  * Snowpack，是一种闪电般快速的前端构建工具，专为现代`Web`设计，较复杂的打包工具（如`Webpack`或`Parcel`）的替代方案，利用`JavaScript`的本机模块系统，避免不必要的工作并保持流畅的开发体验

  * 开发阶段，每次保存单个文件时，`Webpack`和`Parcel`都需要重新构建和重新打包应用程序的整个`bundle`。而`Snowpack`为你的应用程序每个文件构建一次，就可以永久缓存，文件更改时，`Snowpack`会重新构建该单个文件

    > 在重新构建每次变更时没有任何的时间浪费，只需要在浏览器中进行HMR更新

* **Vite**

  vite ，是一种新型前端构建工具，能够显著提升前端开发体验

  它主要由两部分组成：

  * 一个开发服务器，它基于 原生 ES 模块 提供了丰富的内建功能，如速度快到惊人的 [模块热更新HMR

  * 一套构建指令，它使用 Rollup打包你的代码，并且它是预配置的，可以输出用于生产环境的优化过的静态资源

  **特点**

  - 快速的冷启动
  - 即时的模块热更新
  - 真正的按需编译

  `vite`会直接启动开发服务器，不需要进行打包操作，也就意味着不需要分析模块的依赖、不需要编译，因此启动速度非常快

  

  利用现代浏览器支持`ES Module`的特性，当浏览器请求某个模块的时候，再根据需要对模块的内容进行编译，这种方式大大缩短了编译时间

  在热模块`HMR`方面，当修改一个模块的时候，仅需让浏览器重新请求该模块即可，无须像`webpack`那样需要把该模块的相关依赖模块全部编译一次，效率更高



* **webpack**

  相比上述的模块化工具，`webpack`大而全，很多常用的功能做到开箱即用。有两大最核心的特点：**一切皆模块**和**按需加载**

  **优势：**

  - 智能解析：对 CommonJS 、 AMD 、ES6 的语法做了兼容
  - 万物模块：对 js、css、图片等资源文件都支持打包
  - 开箱即用：HRM、Tree-shaking等功能
  - 代码分割：可以将代码切割成不同的 chunk，实现按需加载，降低了初始化时间
  - 插件系统，具有强大的 Plugin 接口，具有更好的灵活性和扩展性
  - 易于调试：支持 SourceUrls 和 SourceMaps
  - 快速运行：webpack 使用异步 IO 并具有多级缓存，这使得 webpack 很快且在增量编译上更加快
  - 生态环境好：社区更丰富，出现的问题更容易解决

  

  

  

