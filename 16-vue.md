### 谈谈你对vue的理解

* **是什么**

  * 是一个用于创建用户界面的开源JavaScript框架，也是一个创建单页应用的Web应用框架

  * Vue所关注的核心是MVC模式中的视图层，同时，它也能方便地获取数据更新，并通过组件内部特定的方法实现视图与模型的交互


* **特点**

  1. **数据驱动（MVVM)**
     
     - Model：模型层，负责处理业务逻辑以及和服务器端进行交互
     - View：视图层：负责将数据模型转化为UI展示出来，可以简单的理解为HTML页面
     - ViewModel：视图模型层，用来连接Model和View，是Model和View之间的通信桥梁
     
  2. **组件化**

     `Vue`中每一个`.vue`文件都可以视为一个组件，组件化的作用

     * 降低整个系统的耦合度，在保持接口不变的情况下，我们可以替换不同的组件快速完成需求，例如输入框，可以替换为日历、时间、范围等组件作具体的实现
     * 调试方便，由于整个系统是通过组件组合起来的，在出现问题的时候，可以用排除法直接移除组件，或者根据报错的组件快速定位问题
     * 提高可维护性，由于每个组件的职责单一，并且组件在系统中是被复用的，所以对代码进行优化可获得系统的整体升级

  3. **指令系统**

     指令 (Directives) 是带有 v- 前缀的特殊属性作用：当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM

     > - 条件渲染指令 `v-if`
     > - 列表渲染指令`v-for`
     > - 属性绑定指令`v-bind`
     > - 事件绑定指令`v-on`
     > - 双向数据绑定指令`v-model`

* **Vue和传统开发的区别**

  * Vue所有的界面事件，都是只去操作数据的，不会直接在事件里面操作DOM
  * Vue所有界面的变动，都是根据数据自动绑定出来的，也就是不用操作DOM

* **Vue和React对比**

  * **相同点**

    1. 都有组件化思想
    2. 都支持服务器端渲染
    3. 都有Virtual DOM（虚拟dom）
    4. 数据驱动视图
    5. 都有支持native的方案：`Vue`的`weex`、`React`的`React native`
    6. 都有自己的构建工具：`Vue`的`vue-cli`、`React`的`Create React App`

  * **区别**

    1. 数据流向的不同。`react`从诞生开始就推崇单向数据流，而`Vue`是双向数据流

    2. 数据变化的实现原理不同。`react`使用的是不可变数据，而`Vue`使用的是可变的数据

       > react是重新生成一份

    3. 组件化通信的不同。`react`中我们通过使用回调函数来进行通信的，而`Vue`中子组件向父组件传递消息有两种方式：事件和回调函数
    4. diff算法不同。`react`主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。`Vue` 使用双向指针，边对比，边更新DOM



### 你对SPA单页面的理解，它的优缺点分别是什么？如何实现SPA应用呢

* **是什么**
  * 单页应用`SPA`是一种网络应用程序或网站的模型，它通过动态重写当前页面来与用户交互，这种方法避免了页面之间切换打断用户体验在单页应用中，所有必要的代码（`HTML`、`JavaScript`和`CSS`）都通过单个页面的加载而检索，或者根据需要（通常是为响应用户操作）动态装载适当的资源并添加到页面。页面在任何时间点都不会重新加载，也不会将控制转移到其他页面
  * 在多页面应用`MPA`中，每个页面都是一个主页面，都是独立的当我们在访问另一个页面的时候，都需要重新加载`html`、`css`、`js`文件，公共文件则根据需求按需加载

* **优点**

  * 具有桌面应用的即时性、网站的可移植性和可访问性
  * 用户体验好、快，内容的改变不需要重新加载整个页面
  * 良好的前后端分离，分工更明确

* **实现原理**

  1. 监听地址栏中`hash`变化驱动界面变化
  2. 用`pushsate`记录浏览器的历史，驱动界面发送变化

* **缺点**

  * 不利于搜索引擎的抓取

    > 单页面的情况下的页面中的很多内容都是根据匹配到的路由动态生成并展示出来的,而且很多页面内容是通过ajax异步获取的,网络抓取工具并不会等待异步请求完成后再行抓取页面内容,
    >
    > 可通过服务段渲染

  * 首次渲染速度相对较慢



### v-if和v-show的区别,使用场景分别是什么？

* **控制手段不同**

  * `v-show`隐藏则是为该元素添加`css--display:none`，`dom`元素依旧还在
  * `v-if`显示隐藏是将`dom`元素整个添加或删除

* **编译过程不同**

  * `v-if`切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；
  * `v-show`只是简单的基于css切换

* **编译条件不同**

  * `v-if`是真正的条件渲染，它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。只有渲染条件为假时，并不做操作，直到为真才渲染
  * `v-show` 由`false`变为`true`的时候不会触发组件的生命周期
  * `v-if`由`false`变为`true`的时候，触发组件的`beforeCreate`、`created`、`beforeMount`、`mounted`钩子，由`true`变为`false`的时候触发组件的`beforeDestory`、`destoryed`方法

* **原理分析**

  具体模板解析流程这里不展开讲，大致流程如下

  - 将模板`template`转为`ast`结构的`JS`对象
  - 用`ast`得到的`JS`对象拼装`render`和`staticRenderFns`函数
  - `render`和`staticRenderFns`函数被调用后生成虚拟`VNODE`节点，该节点包含创建`DOM`节点所需信息
  - `vm.patch`函数通过虚拟`DOM`算法利用`VNODE`节点创建真实`DOM`节点

  1. **v-show原理**

     不管初始条件是什么，元素总是会被渲染

  2. **v-if原理**

     v-if生成render函数的时候带上了条件，如果条件不符合就不会生成VNODD

* **性能消耗**

  * `v-if`有更高的切换消耗

    > 改变很少时可以用这个

  * `v-show`有更高的初始渲染消耗；

    > 频繁切换时用这个



### Vue实例挂载的过程发生了什么

* `new Vue`的时候调用会调用`_init`方法
  * 定义 `$set`、`$get` 、`$delete`、`$watch` 等方法
  * 定义 `$on`、`$off`、`$emit`、`$off`等事件
  * 定义 `_update`、`$forceUpdate`、`$destroy`生命周期
* 调用`$mount`进行页面的挂载
* 挂载的时候主要是通过`mountComponent`方法
* 定义`updateComponent`更新函数
* 执行`render`生成虚拟`DOM`
* `_update`将虚拟`DOM`生成真实`DOM`结构，并且渲染到页面中



### 谈谈对vue生命周期的理解，有什么使用场景

* **什么是vue生命周期**

  Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载DOM、更新、卸载等一系列的过程，我们称这是 Vue 的生命周期

* **vue生命周期的作用是什么**

  Vue 所有的功能的实现都是围绕其生命周期进行的，在生命周期的不同阶段调用对应的钩子函数可以实现组件数据管理和DOM渲染两大重要功能

* **具体分析**

  * **beforeCreate -> created**

    * 初始化`vue`实例，进行数据观测

  * **created**

    * 完成数据观测，属性与方法的运算，`watch`、`event`事件回调的配置
    * 可调用`methods`中的方法，访问和修改data数据触发响应式渲染`dom`，可通过`computed`和`watch`完成数据计算
    * 此时`vm.$el` 并没有被创建

  * **created -> beforeMount**

    * 判断是否存在`el`选项，若不存在则停止编译，直到调用`vm.$mount(el)`才会继续编译
    * 优先级：`render` > `template` > `outerHTML`
    * `vm.el`获取到的是挂载`DOM`的

  * **beforeMount**

    * 在此阶段可获取到`vm.el`
    * 此阶段`vm.el`虽已完成DOM初始化，但并未挂载在`el`选项上

  * **beforeMount -> mounted**

    * 此阶段`vm.el`完成挂载，`vm.$el`生成的`DOM`替换了`el`选项所对应的`DOM`

  * **mounted**

    * `vm.el`已完成`DOM`的挂载与渲染，此刻打印`vm.$el`，发现之前的挂载点及内容已被替换成新的DOM

  * **beforeUpdate**

    * 更新的数据必须是被渲染在模板上的（`el`、`template`、`render`之一）
    * 此时`view`层还未更新
    * 若在`beforeUpdate`中再次修改数据，不会再次触发更新方法

  * **updated**

    * 完成`view`层的更新
    * 若在`updated`中再次修改数据，会再次触发更新方法（`beforeUpdate`、`updated`）

    > 会循环

  * **beforeDestroy**

    * 实例被销毁前调用，此时实例属性与方法仍可访问

  * **destroyed**

    * 完全销毁一个实例。可清理它与其它实例的连接，解绑它的全部指令及事件监听器
    * 并不能清除DOM，仅仅销毁实例

* **使用场景**

  | 生命周期      | 描述                                                         |
  | :------------ | :----------------------------------------------------------- |
  | beforeCreate  | 执行时组件实例还未创建，通常用于插件开发中执行一些初始化任务 |
  | created       | 组件初始化完毕，各种数据可以使用，常用于异步数据获取         |
  | beforeMount   | 未执行渲染、更新，dom未创建                                  |
  | mounted       | 初始化结束，dom已创建，可用于获取访问数据和dom元素           |
  | beforeUpdate  | 更新前，可用于获取更新前各种状态                             |
  | updated       | 更新后，所有状态已是最新                                     |
  | beforeDestroy | 销毁前，可用于一些定时器或订阅的取消                         |
  | destroyed     | 组件已销毁，作用同上                                         |

* **数据请求**

  在`mounted`中的请求有可能导致页面闪动（因为此时页面`dom`结构已经生成），但如果在页面加载前完成请求，则不会出现此情况。建议对页面内容的改动放在`created`生命周期当中







### v-if 与 v-for 为什么不建议一起使用

* **作用**

  * `v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 `true`值的时候被渲染
  * `v-for` 指令基于一个数组来渲染一个列表。`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组或者对象，而 `item` 则是被迭代的数组元素的别名
  * 在 `v-for` 的时候，建议设置`key`值，并且保证每个`key`值是独一无二的，这便于`diff`算法进行优化

* **优先级**

  * `v-if`与`v-for`都是`vue`模板系统中的指令

  * 在`vue2`模板编译的时候，会将指令系统转化成可执行的`render`函数

  * 例子

    * 编写一个p标签，同时使用`v-if`和`v-for`

      ```vue
      <div id="app">
          <p v-if="isShow" v-for="item in items">
              {{ item.title }}
          </p>
      </div>
      ```

    * 模板指令的代码都会生成在`render`函数中，通过`app.$options.render`就能得到渲染函数

      ```js
      ƒ anonymous() {
        with (this) { return 
          _c('div', { attrs: { "id": "app" } }, 
          _l((items), function (item) 
          { return (isShow) ? _c('p', [_v("\n" + _s(item.title) + "\n")]) : _e() }), 0) }
      }
      ```

      > 1. `_l`是`vue`的列表渲染函数，函数内部都会进行一次`if`判断
      > 2. 初步得到结论：`v-for`优先级是比`v-if`高

    * 再将`v-for`与`v-if`置于不同标签

      ```html
      <div id="app">
          <template v-if="isShow">
              <p v-for="item in items">{{item.title}}</p>
          </template>
      </div>
      ```

    * 再输出下`render`函数

      ```js
      ƒ anonymous() {
        with(this){return 
          _c('div',{attrs:{"id":"app"}},
          [(isShow)?[_v("\n"),
          _l((items),function(item){return _c('p',[_v(_s(item.title))])})]:_e()],2)}
      }
      ```

    * 这时候我们可以看到，`v-for`与`v-if`作用在不同标签时候，是先进行判断，再进行列表的渲染

* **结论**

  * 永远不要把 `v-if` 和 `v-for` 同时用在同一个元素上，带来性能方面的浪费（每次渲染都会先循环再进行条件判断）

    > 最极端的情况就是`v-if`条件永远是`false`，但是渲染函数却将每一个都遍历了一遍
    >
    > 就算有一部分是`true`，那也有点浪费

  * 如果避免出现这种情况，则在外层嵌套`template`（页面渲染不生成`dom`节点），在这一层进行v-if判断，然后在内部进行v-for循环

    > 这个是`v-if`的条件永远不变的情况下

  * 如果条件出现在循环内部，可通过计算属性`computed`提前过滤掉那些不需要显示的项

    > 这个是`v-if`条件根据循环来确定的情况



>  注意，vue3改了





### SPA首屏加载速度慢的怎么解决？

* **什么是首屏加载**

  首屏时间（First Contentful Paint），指的是浏览器从响应用户输入网址地址，到首屏内容渲染完成的时间，此时整个网页不一定要全部渲染完成，但需要展示当前视窗需要的内容

* **加载慢的原因**

  * 网络延时问题
  * 资源文件体积是否过大
  * 资源是否重复发送请求去加载了
  * 加载脚本的时候，渲染内容堵塞了

* **解决方案**

  - **减小入口文件积**

    * 常用的手段是路由懒加载，把不同路由对应的组件分割成不同的代码块，待路由被请求的时候会单独打包路由，使得入口文件变小，加载速度大大增加

      > 在`vue-router`配置路由的时候，采用动态加载路由的形式
      >
      > 以函数的形式加载路由，这样就可以把各自的`路由文件分别打包`，只有在`解析给定的路由时`，才会加载路由组件

      > 这是怎么实现按需加载的标答

  - **静态资源本地缓存**

    * 后端返回资源问题:
      * 采用`HTTP`缓存，设置`Cache-Control`，`Last-Modified`，`Etag`等响应头
      * 采用`Service Worker`离线缓存

    * 前端合理利用`localStorage`

  - **UI框架按需加载**

  - **图片资源的压缩**

    * 对于所有的图片资源，我们可以进行适当的压缩
    * 可以使用精灵图减少http请求的压力

  - **避免组件重复打包**

    * 假设`A.js`文件是一个常用的库，现在有多个路由使用了`A.js`文件，这就造成了重复下载

    * 解决方案：在`webpack`的`config`文件中，修改`CommonsChunkPlugin`的配置

      ```js
      minChunks: 3
      ```

    * `minChunks`为3表示会把使用3次及以上的包抽离出来，放进公共依赖文件，避免了重复加载组件

  - **开启GZip压缩**

    * 拆完包之后，我们再用`gzip`做一下压缩 安装`compression-webpack-plugin`

      ```js
      nmp i compression-webpack-plugin -D
      ```

    * 在`vue.congig.js`中引入并修改`webpack`配置

      ```js
      const CompressionPlugin = require('compression-webpack-plugin')
      
      configureWebpack: (config) => {
          if (process.env.NODE_ENV === 'production') {
              // 为生产环境修改配置...
              config.mode = 'production'
              return {
                  plugins: [new CompressionPlugin({
                      test: /\.js$|\.html$|\.css/, //匹配文件名
                      threshold: 10240, //对超过10k的数据进行压缩
                      deleteOriginalAssets: false //是否删除原文件
                  })]
              }
          }
      ```

    * 在服务器我们也要做相应的配置 如果发送请求的浏览器支持`gzip`，就发送给它`gzip`格式的文件

      > 下面是express的例子

      ```js
      const compression = require('compression')
      app.use(compression())  // 在其他中间件使用之前调用
      ```

      

  - **使用SSR**

    SSR（Server side ），也就是服务端渲染，组件或页面通过服务器生成html字符串，再发送到浏览器

    从头搭建一个服务端渲染是很复杂的，`vue`应用建议使用`Nuxt.js`实现服务端渲染



### 为什么data属性是一个函数而不是一个对象？

* **实例和组件定义data的区别**

  * `vue`实例的时候定义`data`属性既可以是一个对象，也可以是一个函数
  * 组件中定义`data`属性，只能是一个函数

* **组件data定义函数与对象的区别**

  * 在我们定义好一个组件的时候，`vue`最终都会通过`Vue.extend()`构成组件实例
  * 如果直接将data写成对象，那么不同组件就会用同一片地址，而函数不会

  ```tsx
  function Component(){
   
  }
  Component.prototype.data = {
  	count : 0
  }
  ```

* **结论**

  - 根实例对象`data`可以是对象也可以是函数（根实例是单例），不会产生数据污染情况
  - 组件实例对象`data`必须为函数，目的是为了防止多个组件实例对象之间共用一个`data`，产生数据污染。采用函数的形式，`initData`时会将其作为工厂函数都会返回全新`data`对象



### 动态给vue的data添加一个新的属性时会发生什么？怎样解决？

* **直接添加属性的问题**

  直接添加新属性页面不会更新

  如下，定义一个`p`标签，通过`v-for`指令进行遍历

  然后给`botton`标签绑定点击事件，我们预期点击按钮时，数据新增一个属性，界面也 新增一行。

  但是点击后界面并没有变化

  ```tsx
  <p v-for="(value,key) in item" :key="key">
      {{ value }}
  </p>
  <button @click="addProperty">动态添加新属性</button>
  ```

  ```tsx
  const app = new Vue({
      el:"#app",
     	data:()=>{
         	item:{
              oldProperty:"旧属性"
          }
      },
      methods:{
          addProperty(){
              this.items.newProperty = "新属性"  // 为items添加新属性
              console.log(this.items)  // 输出带有newProperty的items
          }
      }
  })
  ```

  

* **原因**

  我们在为data添加属性的时候，并不能触发其getter和setter。新增加的属性没有经过`Object.defineProperty`设置成响应式数据

* **解决方法**

  采用下面三种方法添加属性

  - Vue.set()

    > 本质是再次调用`defineProperty`方法，适用于添加少量属性

  - Object.assign()

    > 创建一个新对象，利用这个对象和新的对象混入，适用于添加大量属性
    >
    > 因为直接改变了对象，所以重新收集依赖

    ```js
    this.someObject = Object.assign({},this.someObject,{newProperty1:1,newProperty2:2 ...})
    ```

  - $forcecUpdated()

    > 强迫组件实例本身和插入插槽内容的子组件重新渲染，不建议使用，每次增加个数据都刷新，多次刷新违背了vue的初衷


> `vue3`是用过`proxy`实现数据响应式的，直接动态添加新属性仍可以实现数据响应式



### Vue中组件和插件有什么区别？

* **组件？**

  组件就是把图形、非图形的各种逻辑均抽象为一个统一的概念（组件）来实现开发的模式，在`Vue`中每一个`.vue`文件都可以视为一个组件

  优势：

  1. 降低整个系统的耦合度，在保持接口不变的情况下，我们可以替换不同的组件快速完成需求，例如输入框，可以替换为日历、时间、范围等组件作具体的实现
  2. 调试方便，由于整个系统是通过组件组合起来的，在出现问题的时候，可以用排除法直接移除组件，或者根据报错的组件快速定位问题，之所以能够快速定位，是因为每个组件之间低耦合，职责单一，所以逻辑会比分析整个系统要简单
  3. 提高可维护性，由于每个组件的职责单一，并且组件在系统中是被复用的，所以对代码进行优化可获得系统的整体升级

* **插件？**

  插件通常用来为 `Vue` 添加全局功能。插件的功能范围没有严格的限制——一般有下面几种：

  * **添加全局方法或者属性**。如: `vue-custom-element`
  * **添加全局资源**：指令/过滤器/过渡等。如 `vue-touch`
  * **通过全局混入来添加一些组件选项**。如`vue-router`
  * **添加 `Vue` 实例方法**，通过把它们添加到 `Vue.prototype` 上实现
  * **一个库**，**提供自己的 `API`**，同时提供上面提到的一个或多个功能。如`vue-router`

* **区别？**

  区别主要在于三个方面

  - **编写形式**

    * 编写组件

      编写一个组件，可以有很多方式，我们最常见的就是`vue`单文件的这种格式，每一个`.vue`文件我们都可以看成是一个组件

      我们还可以通过`template`属性来编写一个组件，如果组件内容多，我们可以在外部定义`template`组件内容，如果组件内容并不多，我们可直接写在`template`属性上

      ```js
      <template id="testComponent">     // 组件显示的内容
          <div>component!</div>   
      </template>
      
      Vue.component('componentA',{ 
          template: '#testComponent'  
          template: `<div>component</div>`  // 组件内容少可以通过这种形式
          
          // 其他属性
      })
      ```

    * 编写插件

      `vue`插件的实现应该暴露一个 `install` 方法。这个方法的第一个参数是 `Vue` 构造器，第二个参数是一个可选的选项对象

      ```js
      MyPlugin.install = function (Vue, options) {
        // 1. 添加全局方法或 property
        Vue.myGlobalMethod = function () {
          // 逻辑...
        }
      
        // 2. 添加全局资源
        Vue.directive('my-directive', {
          bind (el, binding, vnode, oldVnode) {
            // 逻辑...
          }
          ...
        })
      
        // 3. 注入组件选项
        Vue.mixin({
          created: function () {
            // 逻辑...
          }
          ...
        })
      
        // 4. 添加实例方法
        Vue.prototype.$myMethod = function (methodOptions) {
          // 逻辑...
        }
      }
      ```

      

  - **注册形式**

    * 组件注册

      `vue`组件注册主要分为全局注册与局部注册

      全局注册通过`Vue.component`方法，第一个参数为组件的名称，第二个参数为传入的配置项

      ```js
      Vue.component('my-component-name', { /* ... */ })
      ```

      局部注册只需在用到的地方通过`components`属性注册一个组件

      ```js
      const component1 = {...} // 定义一个组件
      
      export default {
      	components:{
      		component1   // 局部注册
      	}
      }
      ```

    * 插件注册

      插件的注册通过`Vue.use()`的方式进行注册（安装），第一个参数为插件的名字，第二个参数是可选择的配置项

      > 注册插件的时候，需要在调用 `new Vue()` 启动应用之前完成
      >
      > `Vue.use`会自动阻止多次注册相同插件，只会注册一次

      ```js
      Vue.use(插件名字,{ /* ... */} )
      ```

      

  - **使用场景**

    * 组件 `(Component)` 是用来构成你的 `App` 的业务模块，它的目标是 `App.vue`
    * 插件 `(Plugin)` 是用来增强你的技术栈的功能模块，它的目标是 `Vue` 本身
    * 简单来说，插件就是指对`Vue`的功能的增强或补充









### Vue组件之间的通信方式都有哪些

* **分类**

  组件间通信的分类可以分成以下：

  - 父子组件之间的通信
  - 兄弟组件之间的通信
  - 祖孙与后代组件之间的通信
  - 非关系组件间之间的通信

* **方案**

  `vue`中有8种常规的通信方案

  1. 通过 props 传递
  2. 通过 $emit 触发自定义事件
  3. 使用 ref
  4. EventBus
  5. $parent 或$root
  6. attrs 与 listeners
  7. Provide 与 Inject
  8. Vuex

* **详细**

  1. **通过 props 传递**

     - 适用场景：父组件传递数据给子组件
     - 子组件设置`props`属性，定义接收父组件传递过来的参数
     - 父组件在使用子组件标签中通过字面量来传递值

  2. **$emit 触发自定义事件**

     - 适用场景：子组件传递数据给父组件
     - 子组件通过`$emit触发`自定义事件，`$emit`第二个参数为传递的数值
     - 父组件绑定监听器获取到子组件传递过来的参数

  3. **ref**

     - 父组件在使用子组件的时候设置`ref`
     - 父组件通过设置子组件`ref`来获取数据

     ```js
     <Children ref="foo" />  
       
     this.$refs.foo  // 获取子组件实例，通过子组件实例我们就能拿到对应的数据  
     ```

  4. **EventBus**

     - 使用场景：兄弟组件传值
     - 创建一个中央事件总线`EventBus`
     - 兄弟组件通过`$emit`触发自定义事件，`$emit`第二个参数为传递的数值
     - 另一个兄弟组件通过`$on`监听自定义事件

     > 在vue2中一般用Vue实例来作为一个Bus，但是Vue3中不行，因为废除了$on，应该使用第三方的api

  5. **$parent 或$ root**

     - 通过共同祖辈`$parent`或者`$root`搭建通信桥连

     * 兄弟组件

       ```js
       this.$parent.on('add',this.add)
       ```

     * 另一个

       ```js
       this.$parent.emit('add')
       ```

  6. **$attrs 与$ listeners**

     - 适用场景：祖先传递数据给子孙
     - 设置批量向下传属性`$attrs`和 `$listeners`
     - 包含了父级作用域中不作为 `prop` 被识别 (且获取) 的特性绑定 ( class 和 style 除外)。
     - 可以通过 `v-bind="$attrs"` 传⼊内部组件

     > 这个还是得孩子负责传给孙子的

     ```js
     // child：并未在props中声明foo  
     <p>{{$attrs.foo}}</p>  
       
     // parent  
     <HelloWorld foo="foo"/> 
     ```

     ```js
     // 给Grandson隔代传值，communication/index.vue  
     <Child2 msg="lalala" @some-event="onSomeEvent"></Child2>  
       
     // Child2做展开  
     <Grandson v-bind="$attrs" v-on="$listeners"></Grandson>  
       
     // Grandson使⽤  
     <div @click="$emit('some-event', 'msg from grandson')">  
     {{msg}}  
     </div>  
     ```

  7. **provide 与 inject**

     - 在祖先组件定义`provide`属性，返回传递的值
     - 在后代组件通过`inject`接收组件传递过来的值

     ```js
     // 祖先组件
     provide(){  
         return {  
             foo:'foo'  
         }  
     }  
     ```

     ```js
     // 后代组件
     inject:['foo'] // 获取到祖先组件传递过来的值  
     ```

  8. **`vuex`**

     - 适用场景: 复杂关系的组件数据传递
     - `Vuex`作用相当于一个用来存储共享变量的容器



* **小结**
  - 父子关系的组件数据传递选择 `props` 与 `$emit`进行传递，也可选择`ref`
  - 兄弟关系的组件数据传递可选择`$bus`，其次可以选择`$parent`进行传递
  - 祖先与后代组件数据传递可选择`attrs`与`listeners`或者 `Provide`与 `Inject`
  - 复杂关系的组件数据传递可以通过`vuex`存放共享的变量







### 双向数据绑定是什么

* **是什么**

  * **单向数据绑定**

    就是把`Model`绑定到`View`，当我们用`JavaScript`代码更新`Model`时，`View`就会自动更新双向绑定就很容易联想到了

  * **双向数据绑定**

    在单向绑定的基础上，用户更新了`View`，`Model`的数据也自动被更新了，这种情况就是双向绑定举个栗子

* **原理**

  1. `new Vue()`首先执行初始化，对`data`执行响应化处理，这个过程发生`Observe`中
  2. 处理的过程会劫持`data`中每个`key`的访问和获取，也就是`getter`和`setter`。在劫持的时候，创建了一个依赖收集数组`dep`来收集依赖这个`key`的对象。当触发`getter`的时候，把对象加入到`dep`中。当触发`setter`的时候，提醒所有依赖该`key`的对象该`key`的值已经更新。
  3. 对模板执行编译过程中，找到其中动态绑定的数据，从`data`中获取并初始化视图，这个过程发生在`Compile`中。其中获取数据通过一个`watcher`实例去获取，则`watcher`被该`key`的`dep`收集，并给予`watcher`实例一个更新函数，当`watcher`被提醒的时候执行这个更新函数从而重新渲染视图。
  4. 当`data`中某个`key`被改变的时候，就会找到对应的`dep`，提醒里面的`watcher`该数据被更新了

  > 一个key会收集多个watcher，但是只有一个dep数组

* **实现**

  构造函数中，执行初始化，对data执行响应化处理

  ```tsx
  class Vue {  
    constructor(options) {  
      this.$options = options;  
      this.$data = options.data;  
          
      // 对data选项做响应式处理  
      observe(this.$data);  
          
      // 代理data到vm上  
      proxy(this);  
          
      // 执行编译  
      new Compile(options.el, this);  
    }  
  }  
  ```

  响应化处理中，对data进行监听

  ```tsx
  function observe(obj) {  
    if (typeof obj !== "object" || obj == null) {  
      return;  
    }  
    new Observer(obj);  
  }  
  
  class Observer {  
    constructor(value) {  
      this.value = value;  
      this.walk(value);  
    }  
      
    // 对data的每一项进行劫持
    walk(obj) {  
      Object.keys(obj).forEach((key) => {  
        defineReactive(obj, key, obj[key]);  
      });  
    }  
  }  
  ```

  编译模板时，Compile对每个元素节点的指令进行扫描跟解析,根据指令模板替换数据,以及绑定相应的更新函数

  ```tsx
  class Compile {  
    constructor(el, vm) {  
      this.$vm = vm;  
      this.$el = document.querySelector(el);  // 获取dom  
      if (this.$el) {  
        this.compile(this.$el);  
      }  
    }  
    compile(el) {  
      const childNodes = el.childNodes;   
      Array.from(childNodes).forEach((node) => { // 遍历子元素  
        if (this.isElement(node)) {   // 判断是否为节点  
          console.log("编译元素" + node.nodeName);  
        } else if (this.isInterpolation(node)) {  
          console.log("编译插值⽂本" + node.textContent);  // 判断是否为插值文本 {{}}  
        }  
        if (node.childNodes && node.childNodes.length > 0) {  // 判断是否有子元素  
          this.compile(node);  // 对子元素进行递归遍历  
        }  
      });  
    }  
    isElement(node) {  
      return node.nodeType == 1;  
    }  
    isInterpolation(node) {  
      return node.nodeType == 3 && /\{\{(.*)\}\}/.test(node.textContent);  
    }  
  }  
  ```

  **依赖收集**

  视图中会用到`data`中某`key`，这称为依赖。同⼀个`key`可能出现多次，每次都需要收集出来用⼀个`Watcher`来维护它们，此过程称为依赖收集多个`Watcher`需要⼀个`Dep`来管理，需要更新时由`Dep`统⼀通知

  ![img](https://static.vue-js.com/fa191f40-3ac9-11eb-ab90-d9ae814b240d.png)

  **实现思路**

  1. `defineReactive`时为每⼀个`key`创建⼀个`Dep`实例
  2. 初始化视图时读取某个`key`，例如`name1`，创建⼀个`watcher1`
  3. 由于触发`name1`的`getter`方法，便将`watcher1`添加到`name1`对应的Dep中
  4. 当`name1`更新，`setter`触发时，便可通过对应`Dep`通知其管理所有`Watcher`更新

  ```tsx
  // 负责更新视图  
  class Watcher {  
    constructor(vm, key, updater) {  
      this.vm = vm  
      this.key = key  
      this.updaterFn = updater  
    
      // 创建实例时，把当前实例指定到Dep.target静态属性上  
      // Dep数组会push Dep.target
      Dep.target = this  
      // 读一下key，触发get  
      vm[key]  
      // 置空  
      Dep.target = null  
    }  
    
    // 未来执行dom更新函数，由dep调用的  
    update() {  
      this.updaterFn.call(this.vm, this.vm[this.key])  
    }  
  }  
  ```

  声明`Dep`

  ```tsx
  class Dep {  
    constructor() {  
      this.deps = [];  // 依赖管理  
    }  
    addDep(dep) {  
      this.deps.push(dep);  
    }  
    notify() {   
      this.deps.forEach((dep) => dep.update());  
    }  
  }  
  ```

  getter和setter中依赖收集和分发

  ```tsx
  function defineReactive(obj, key, val) {
    // 深度观察
    this.observe(val);  
    const dep = new Dep();  // 闭包
    Object.defineProperty(obj, key, {  
      get() {  
        Dep.target && dep.addDep(Dep.target);// Dep.target也就是Watcher实例  
        return val;  
      },  
      set(newVal) {  
        if (newVal === val) return;  
        dep.notify(); // 通知dep执行更新方法  
      },  
    });  
  }  
  ```

  

### Vue中的$nextTick有什么作用？

* **是什么**

  `Vue` 在更新 `DOM` 时是异步执行的。当数据发生变化，`Vue`将开启一个异步更新队列，视图需要等队列中所有数据变化完成之后，再统一进行更新

  nextTick是下次 DOM 更新循环结束之后执行延迟回调

* **有什么用**

  * 如果想要在修改数据后立刻得到更新后的`DOM`结构，可以使用`Vue.nextTick()`

* **原理**

  1. 当nextTick被调用时，先将回调函数添加到`callback`数组中

  2. 如果是事件循环中第一次使用nextTick，则向任务队列中添加任务。使用timerFunc函数封装Promise.then，利用Promise.then将任务(就是一个函数)添加到任务队列

     > 用pending来表示现在是否还没使用过nextTick，true表示还没有，false表示任务队列中的callback还没有被执行，直接将新任务push进去好了

     > `Promise.then`、`MutationObserver`、`setImmediate`、`setTimeout`
     >
     > 根据兼容性从前往后优先使用

  3. 如果不是本轮事件循环中第一次使用nextTick,那么就不用重复将任务添加到队列,只增加`callback`

  4. 当任务被执行的时候，将本轮nextTick注册的回调全部执行一遍，再将回调数组清空，将当前nextTick状态设置为`pending=true`





### 说说你对vue的mixin的理解，有什么应用场景？

* **是什么**

  官方定义

  > `mixin`（混入），提供了一种非常灵活的方式，来分发 `Vue` 组件中的可复用功能。

  本质其实就是一个`js`对象，它可以包含我们组件中任意功能选项，如`data`、`components`、`methods`、`created`、`computed`等等

  我们只要将共用的功能以对象的方式传入 `mixins`选项中，当组件使用 `mixins`对象时所有`mixins`对象的选项都将被混入该组件本身的选项中来

  在`Vue`中我们可以**局部混入**跟**全局混入**

* **局部混入**

  定义一个`mixin`对象，有组件`options`的`data`、`methods`属性

  ```tsx
  var myMixin = {
    created: function () {
      this.hello()
    },
    methods: {
      hello: function () {
        console.log('hello from mixin!')
      }
    }
  }
  ```

  组件通过`mixins`属性调用`mixin`对象，则该组件会混入上面的东西

  ```tsx
  Vue.component('componentA',{
    mixins: [myMixin]
  })
  ```

* **全局混入**

  通过`Vue.mixin()`进行全局的混入，他会影响每一个组件

  ```tsx
  Vue.mixin({
    created: function () {
        console.log("全局混入")
      }
  })
  ```

* **使用场景**

  在日常的开发中，我们经常会遇到在不同的组件中经常会需要用到一些相同或者相似的代码，这些代码的功能相对独立，这时，可以通过`Vue`的`mixin`功能将相同或者相似的代码提出来

  举个例子

  定义一个`modal`弹窗组件，内部通过`isShowing`来控制显示

  ```tsx
  const Modal = {
    template: '#modal',
    data() {
      return {
        isShowing: false
      }
    },
    methods: {
      toggleShow() {
        this.isShowing = !this.isShowing;
      }
    }
  }
  ```

  定义一个`tooltip`提示框，内部通过`isShowing`来控制显示

  ```tsx
  const Tooltip = {
    template: '#tooltip',
    data() {
      return {
        isShowing: false
      }
    },
    methods: {
      toggleShow() {
        this.isShowing = !this.isShowing;
      }
    }
  }
  ```

  抽离

  ```tsx
  const toggle = {
    data() {
      return {
        isShowing: false
      }
    },
    methods: {
      toggleShow() {
        this.isShowing = !this.isShowing;
      }
    }
  }
  ```

  注入

  ```tsx
  const Modal = {
    template: '#modal',
    mixins: [toggle]
  };
   
  const Tooltip = {
    template: '#tooltip',
    mixins: [toggle]
  }
  ```

* **策略**

  下面是关于`Vue`的几种类型的合并策略

  - 替换型
  - 合并型
  - 队列型
  - 叠加型

* **替换型**

  替换型合并有`props`、`methods`、`inject`、`computed`

  同名的`props`、`methods`、`inject`、`computed`会被后来者代

* **合并型**

  和并型合并有：`data`，遍历要合并的 data 的所有属性，然后根据不同情况进行合并

  * 当目标 data 对象不包含当前属性时，调用 `set` 方法进行合并（set方法其实就是一些合并重新赋值的方法）
  * 当目标 data 对象包含当前属性并且当前值为纯对象时，递归合并当前对象值，这样做是为了防止对象存在新增属性

* **队列性**

  队列性合并有：全部生命周期和`watch`
  生命周期钩子和`watch`被合并为一个数组，然后正序遍历一次执行

* **叠加型**

  叠加型合并有：`component`、`directives`、`filters`

  叠加型主要是通过原型链进行层层的叠加







### 说说你对slot的理解？slot使用场景有哪些？

* **是什么**

  `Slot` 艺名插槽，花名“占坑”，我们可以理解为`solt`在组件模板中占好了位置，当使用该组件标签时候，组件标签里面的内容就会自动填坑（替换组件模板中`slot`位置），作为承载分发内容的出口

* **使用场景**

  * 通过插槽可以让用户可以拓展组件，去更好地复用组件和对其做定制化处理

  * 如果父组件在使用到一个复用组件的时候，获取这个组件在不同的地方有少量的更改，如果去重写组件是一件不明智的事情

  * 通过`slot`插槽向组件内部指定位置传递内容，完成这个复用组件在不同场景的应用

    比如布局组件、表格列、下拉选、弹框显示内容等

* **分类**

  `slot`可以分来以下三种：

  - 默认插槽
  - 具名插槽
  - 作用域插槽

* **默认插槽**

  * 子组件用`<slot>`标签来确定渲染的位置，标签里面可以放`DOM`结构，当父组件使用的时候没有往插槽传入内容，标签内`DOM`结构就会显示在页面
  * 父组件在使用的时候，直接在子组件的标签内写入内容即可

  ```tsx
  // 子组件
  template: `
          <div :style="style1">
              <slot>后备内容</slot> // 定义插槽
          </div>
  `,
      
  // 父组件
  template: `
  <div>
      <com-one>
      	<span>{{val1}}</span> // 使用插槽
      </com-one>
  </div>`
  ```

* **具名插槽**

  * 子组件用`name`属性来表示插槽的名字，不传为默认插槽
  * 父组件中在使用时在默认插槽的基础上加上`slot`属性，值为子组件插槽`name`属性值

  ```tsx
  <template>
      <slot>插槽后备的内容</slot>
    <slot name="content">插槽后备的内容</slot>
  </template>
  
  <child>
      <template v-slot:default>具名插槽</template>
      <!-- 具名插槽⽤插槽名做参数 -->
      <template v-slot:content>内容...</template>
  </child>
  ```

* **作用域插槽scoped slots**

  * 子组件在作用域上绑定属性来将子组件的信息传给父组件使用，这些属性会被挂在父组件`v-slot`接受的对象上
  * 父组件中在使用时通过`v-slot:`（简写：#）获取子组件的信息，在内容中使用

  ```js
  <template> 
    <slot name="footer" testProps="子组件的值">
            <h3>没传footer插槽</h3>
      </slot>
  </template>
  
  父组件
  template: `
  <child> 
      <!-- 把v-slot的值指定为作⽤域上下⽂对象 -->
      <template v-slot:default="slotProps">          // 也可以解构
        来⾃⼦组件数据：{{slotProps.testProps}}
      </template>
      <template #default="slotProps">
        来⾃⼦组件数据：{{slotProps.testProps}}
      </template>
  </child>
  ```

* **原理** 

  先看一个例子。先看父组件的模板，其使用的子组件，并在子组件中中放入孩子，插对应的插槽
  
  ```vue
  <test>
    <template v-slot:foo="prop">
      <span>{{prop.msg}}</span>
    </template>
  </test>
  ```
  
  这段模板最终会编译成这样的渲染函数,也就是插槽的内容当做属性`scopedSlots`传给了test。最终经过一系列处理（`resolveScopedSlots`, `normalizeScopedSlots`），`test`组件的实例 `this.$scopedSlots` 就可以访问到这两个 `foo` 函数
  
  > 未命名的话是key是default
  
  ```tsx
  with (this) { // 上下文为父组件
    return _c("test", { 
      scopedSlots: _u([
        {
          key: "foo",
          fn: function (prop) {
            return [_c("span", [_v(_s(prop.msg))])];
          },
        },
      ]),
    });
  }
  ```
  
  假设text组件模板是这样的
  
  ```vue
  <div>
    <slot name="foo" v-bind="{ msg }"></slot>
  </div>
  ```
  
  那么这个模板会被编译成这这样。
  
  ```tsx
  with (this) { // 上下文为子组件
    return _c("div", [_t("foo", null, null, { msg })]);
  }
  ```
  
  主要就是这个`_t`了,`_t` 也就是 `renderSlot`的别名，简化后的实现是这样的：
  
  > 可以看到作用域插槽和普通插槽的区别就是在使用插槽的时候消不消费props
  
  ```tsx
  export function renderSlot (
    name: string,
    fallback: ?Array<VNode>,
    props: ?Object,
    bindObject: ?Object
  ): ?Array<VNode> {
    // 通过 name 拿到函数
    const scopedSlotFn = this.$scopedSlots[name]
    let nodes
    if (scopedSlotFn) { // scoped slot
      props = props || {}
      // 执行函数返回 vnode
      nodes = scopedSlotFn(props) || fallback
    }
    return nodes
  }
  ```

> 总结就是父组件将插槽要渲染的容传递给子组件，然后子组件根据`name`拿到相应的函数并传入`props`拿渲染函数，然后生成vnode，所以是子组件负责渲染

* **更新**

  如下，如果插槽里面消费的是父组件里面的数据，按理来说msgInParent变应该会触发父组件的更新，因为`<span>Hello {{msgInParent}}</span>`在父组件中。

  但是其实只触发子组件的更新，因为插槽生成vnode的过程，插槽的`_c`发生在子组件的渲染过程中，其全局上下文为子组件:`with(this)`,所以依赖收集到的是绑定了子组件的watcher。

  > 可以这么理解，`_c`才是读取真正数据的，数据在哪个`_c`被读取，那么就收集绑定了这个`_c`执行时的执行剩下文的`watcher`

  ```tsx
  <test>
    <template v-slot:bar>
      <span>Hello {{msgInParent}}</span> // 消费的是父组件的数据
    </template>
  </test>
  <script>
    new Vue({
      name: "App",
      el: "#app",
      mounted() {
        setTimeout(() => {
          this.msgInParent = "Changed";
        }, 1000);
      },
      data() {
        return {
          msgInParent: "msgInParent",
        };
      },
      components: {
        test: {
          name: "test",
          template: `
            <div>
              <slot name="bar"></slot>
            </div>
          `,
        },
      },
    });
  </script>
  ```

  

### 面试官：Vue.observable你有了解过吗？说说看

* **是什么**

  `Observable` 翻译过来我们可以理解成**可观察的**,让一个对象变成响应式数据。

  返回的对象可以直接用于渲染函数和计算属性内，并且会在发生变更时触发相应的更新。也可以作为最小化的跨组件状态存储器

  ```tsx
  Vue.observable({ count : 1})
  ```

  在 `Vue 2.x` 中，被传入的对象会直接被 `Vue.observable` 变更，它和被返回的对象是同一个对象,也就是直接改变传进去观察的对象也能触发响应式

  在 `Vue 3.x` 中，则会返回一个可响应的代理，而对源对象直接进行变更仍然是不可响应的

* **怎么用**

  在非父子组件通信时，可以使用通常的`bus`或者使用`vuex`，但是实现的功能不是太复杂，而使用上面两个又有点繁琐。这时，`observable`就是一个很好的选择

  > 新建一个js文件存放响应式的对象

  ```tsx
  // store.js
  
  // 引入vue
  import Vue from 'vue
  // 创建state对象，使用observable让state对象可响应
  export let state = Vue.observable({
    name: '张三',
    'age': 38
  })
  // 创建对应的方法
  export let mutations = {
    changeName(name) {
      state.name = name
    },
    setAge(age) {
      state.age = age
    }
  }
  ```

  > 在`.vue`文件中直接使用即可

  ```tsx
  <template>
    <div>
      姓名：{{ name }}
      年龄：{{ age }}
      <button @click="changeName('李四')">改变姓名</button>
      <button @click="setAge(18)">改变年龄</button>
    </div>
  </template>
  import { state, mutations } from '@/store
  export default {
    // 在计算属性中拿到值
    computed: {
      name() {
        return state.name
      },
      age() {
        return state.age
      }
    },
    // 调用mutations里面的方法，更新数据
    methods: {
      changeName: mutations.changeName,
      setAge: mutations.setAge
    }
  }
  ```

* **原理**

  其原理和响应式的原理一样，都是对这个对象进行observe





### 你知道vue中key的原理吗？说说你对它的理解

* **是什么**

  key是给每一个vnode的唯一id，也是diff的一种优化策略，可以根据key，更准确， 更快的找到对应的vnode节点

* **v-for时不使用key会怎样**

  > tip: patch就是详细对比两个vnode的各项数据，不同就更新，包括子节点，子节点比较的时候又进行一次diff，是递归的过程

  * key的作用主要是为了更高效的对比虚拟DOM中每个节点是否是相同节点


  * Vue在patch过程中判断两个节点是否是相同节点,key是一个必要条件，渲染一组列表时，key往往是唯一标识，所以如果不定义key的话，Vue只能认为比较的两个节点是同一个，哪怕它们实际上不是，这导致了频繁更新元素，使得整个patch过程比较低效，影响性能


  * Vue判断两个节点是否相同时主要判断两者的`key`和`元素类型`等，因此如果不设置key,它的值就是undefined，则可能永远认为这是两个相同的节点，只能去做更新操作，这造成了大量的dom更新操作，明显是不可取的  

  * 下面是不使用key的例子，则对应位置两两patch，节点不同的时候都需要操作DOM，最后还创建了一个本来存在的节点

    ![img](https://static.vue-js.com/c9da6790-3f41-11eb-85f6-6fac77c0c9b3.png)

* **设置key值一定能提高diff效率吗？**

  如果两个Vnode只是文本不一样，那么其实更新数据比移动Dom更加高效。所以Vue的这个默认就地复用(对应位置两两patch)也是有原因的。



### Vue常用的修饰符有哪些有什么应用场景

* **是什么**

  在`Vue`中，修饰符处理了许多`DOM`事件的细节，让我们不再需要花大量的时间去处理这些烦恼的事情，而能有更多的精力专注于程序的逻辑处理

  `vue`中修饰符分为以下五种：

  - 表单修饰符
  - 事件修饰符
  - 鼠标按键修饰符
  - 键值修饰符
  - v-bind修饰符

* **表单修饰符**

  在我们填写表单的时候用得最多的是`input`标签，指令用得最多的是`v-model`

  关于表单的修饰符有如下：

  - **lazy**

    在我们填完信息，光标离开标签的时候，才会将值赋予给`value`，也就是在`change`事件之后再进行信息同步

    ```vue
    <input type="text" v-model.lazy="value">
    <p>{{value}}</p>
    ```

  - **trim**

    自动过滤用户输入的首空格字符，而中间的空格不会过滤

  - **number**

    自动将用户的输入值转为数值类型，但如果这个值无法被`parseFloat`解析，则会返回原来的值

    ```tsx
    <input v-model.number="age" type="number">
    ```

* **事件修饰符**

  事件修饰符是对事件捕获以及目标进行了处理，有如下修饰符：

  - **stop**

    阻止了事件冒泡，相当于调用了`event.stopPropagation`方法

  - **prevent**

    阻止了事件的默认行为，相当于调用了`event.preventDefault`方法

    ```tsx
    <form v-on:submit.prevent="onSubmit"></form>
    ```

  - **self**

    只当在 `event.target` 是当前元素自身时触发处理函数

    ```tsx
    <div v-on:click.self="doThat">...</div>
    ```

  - **once**

    绑定了事件以后只能触发一次，第二次就不会触发

  - **capture**

    使事件触发从包含这个元素的顶层开始往下触发

    ```vue
    <div @click.capture="shout(1)">
        obj1
        <div @click.capture="shout(2)">
            obj2
            <div @click="shout(3)">
                obj3
                <div @click="shout(4)">
                    obj4
                </div>
            </div>
        </div>
    </div>
    // 输出结构: 1 2 4 3 
    // 因为后面的没有这个属性，所以还是冒泡
    ```

  - **passive**

    在移动端，当我们在监听元素滚动事件的时候，会一直触发`onscroll`事件会让我们的网页变卡，因此我们使用这个修饰符的时候，相当于给`onscroll`事件整了一个`.lazy`修饰符

  - **native**

    让组件变成像`html`内置标签那样监听根元素的原生事件，否则组件上使用 `v-on` 只会监听自定义事件

    ```tsx
    <my-component v-on:click.native="doSomething"></my-component>
    ```

* **鼠标修饰符**

  鼠标按钮修饰符针对的就是左键、右键、中键点击，有如下

  - left 左键点击
  - right 右键点击
  - middle 中键点击

  ```tsx
  <button @click.left="shout(1)">ok</button>
  <button @click.right="shout(1)">ok</button>
  <button @click.middle="shout(1)">ok</button>
  ```

* **键盘修饰符**

  键盘修饰符是用来修饰键盘事件（`onkeyup`，`onkeydown`）的，有如下：

  `keyCode`存在很多，但`vue`为我们提供了别名，分为以下两种：

  - 普通键（enter、tab、delete、space、esc、up...）
  - 系统修饰键（ctrl、alt、meta、shift...）

  ```tsx
  // 只有按键为keyCode的时候才触发
  <input type="text" @keyup.keyCode="shout()">
  ```

  还可以通过以下方式自定义一些全局的键盘码别名

  ```tsx
  Vue.config.keyCodes.f2 = 113
  ```

* **v-bind修饰符**

  v-bind修饰符主要是为属性进行操作，用来分别有如下：

  - async

    能对`props`进行一个双向绑定,自动为其绑定事件

    ```tsx
    //父组件
    <comp :myMessage.sync="bar"></comp> 
    //子组件
    this.$emit('update:myMessage',params);
    ```

  - prop

    设置自定义标签属性

  - camel

    将命名变为驼峰命名法



### 你有写过自定义指令吗？自定义指令的应用场景有哪些

* **是什么**

  在`vue`中提供了一套为数据驱动视图更为方便的操作，这些操作被称为指令系统

  我们看到的`v-`开头的行内属性，都是指令，不同的指令可以完成或实现不同的功能

  除了核心功能默认内置的指令 (`v-model` 和 `v-show`)，`Vue` 也允许注册自定义指令

  使用的几种方式

  ```js
  //会实例化一个指令，但这个指令没有参数 
  `v-xxx`
  
  // -- 将值传到指令中
  `v-xxx="value"`  
  
  // -- 将字符串传入到指令中，如`v-html="'<p>内容</p>'"`
  `v-xxx="'string'"` 
  
  // -- 传参数（`arg`），如`v-bind:class="className"`
  `v-xxx:arg="value"` 
  
  // -- 使用修饰符（`modifier`）
  `v-xxx:arg.modifier="value"` 
  ```

* **实现**

  注册一个自定义指令有全局注册与局部注册

  全局注册主要是通过`Vue.directive`方法进行注册

  `Vue.directive`第一个参数是指令的名字（不需要写上`v-`前缀），第二个参数可以是对象数据，也可以是一个指令函数

  ```js
  // 注册一个全局自定义指令 `v-focus`
  Vue.directive('focus', {
    // 当被绑定的元素插入到 DOM 中时……
    inserted: function (el) {
      // 聚焦元素
      el.focus()  // 页面加载完成之后自动让输入框获取到焦点的小功能
    }
  })
  ```

  局部注册通过在组件`options`选项中设置`directive`属性

  ```tsx
  directives: {
    focus: {
      // 指令的定义
      inserted: function (el) {
        el.focus() // 页面加载完成之后自动让输入框获取到焦点的小功能
      }
    }
  }
  ```

  然后你可以在模板中任何元素上使用新的 `v-focus` property，如下：

  ```js
  <input v-focus />
  ```

* **钩子**

  自定义指令也像组件那样存在钩子函数：

  - `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
  - `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)
  - `update`：所在组件的 `VNode` 更新时调用，但是可能发生在其子 `VNode` 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新
  - `componentUpdated`：指令所在组件的 `VNode` 及其子 `VNode` 全部更新后调用
  - `unbind`：只调用一次，指令与元素解绑时调用

  所有的钩子函数的参数都有以下：

  - `el`：指令所绑定的元素，可以用来直接操作 `DOM`
  - binding：一个对象，包含以下property
    - `name`：指令名，不包括 `v-` 前缀。
    - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
    - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
    - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
    - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
    - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`
  - `vnode`：`Vue` 编译生成的虚拟节点
  - `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用

  ```js
  <div v-demo="{ color: 'white', text: 'hello!' }"></div>
  <script>
      Vue.directive('demo', function (el, binding) {
      console.log(binding.value.color) // "white"
      console.log(binding.value.text)  // "hello!"
      })
  </script>
  ```

* **应用场景**

  使用自定义指令可以满足我们日常一些场景，这里给出几个自定义指令的案例：

  - **表单防止重复提交**

    也就是防抖

    ```tsx
    // 1.设置v-throttle自定义指令
    Vue.directive('throttle', {
      bind: (el, binding) => {
        let throttleTime = binding.value; // 节流时间
        if (!throttleTime) { // 用户若不设置节流时间，则默认2s
          throttleTime = 2000;
        }
        let cbFun;
        el.addEventListener('click', event => {
          if (!cbFun) { // 第一次执行
            cbFun = setTimeout(() => {
              cbFun = null;
            }, throttleTime);
          } else {
            event && event.stopImmediatePropagation();
          }
        }, true);
      },
    });
    // 2.为button标签设置v-throttle自定义指令
    <button @click="sayHello" v-throttle>提交</button>
    ```

  - 图片懒加载

  - 一键 Copy的功能

  - 拖拽指令

  - 页面水印

  - 权限校验

  反正就是，我能获取到你的元素和传进来的参数和值，我想干嘛就干嘛哈哈

> 使用的其实是订阅者模式





### Vue中的过滤器了解吗？过滤器的应用场景有哪些？

* **是什么**

  过滤器实质不改变原始数据，只是对数据进行加工处理后返回过滤后的数据再进行调用处理，我们也可以理解其为一个纯函数

  `Vue` 允许你自定义过滤器，可被用于一些常见的文本格式化

  > `Vue3`中已废弃`filter`

* **如何使用**

  `vue`中的过滤器可以用在两个地方：双花括号插值和 `v-bind` 表达式，过滤器应该被添加在 `JavaScript`表达式的尾部，由“管道”符号指示：

  ```tsx
  <!-- 在双花括号中 -->
  {{ message | capitalize }}
  
  <!-- 在 `v-bind` 中 -->
  <div v-bind:id="rawId | formatId"></div>
  
  // 串联
  {{ message | filterA | filterB }}
  ```

* **定义过滤器**

  组件中定义

  ```js
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
  ```

* **定义全局过滤器**

  ```js
  Vue.filter('capitalize', function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  })
  
  new Vue({
    // ...
  })
  ```

> 当全局过滤器和局部过滤器重名时，会采用局部过滤器,其实很多都是这样，全局的权重是比较低的

* **应用场景**

  比如单位转换、数字打点、文本格式化、时间格式化之类的等







### 什么是虚拟DOM？如何实现一个虚拟DOM？说说你的思路

* **是什么**

  虚拟DOM实际上只是一层对真实`DOM`的抽象，以`JavaScript` 对象 (`VNode` 节点) 作为基础的树，用对象的属性来描述节点，最终可以通过一系列操作使这棵树映射到真实环境上

  其中最少包含标签名 (`tag`)、属性 (`attrs`) 和子元素对象 (`children`) 三个属性，不同框架对这三个属性的名命可能会有差别

  创建虚拟`DOM`就是为了更好将虚拟的节点渲染到页面视图中，所以虚拟`DOM`对象的节点与真实`DOM`的属性一一照应

  一个Vue的模板如下

  ```tsx
  <div id="app">
      <p class="p">节点内容</p>
      <h3>{{ foo }}</h3>
  </div>
  ```

  观察其render，我们可以看到虚拟dom的绉型

  ```js
  (function anonymous(
  ) {
      with(this){return _c('div',{attrs:{"id":"app"}},[_c('p',{staticClass:"p"},
                                                          [_v("节点内容")]),_v(" "),_c('h3',[_v(_s(foo))])])}})
  ```

* **为什么**

  `DOM`是很慢的，其元素非常庞大，页面的性能问题，大部分都是由`DOM`操作引起的

  真实的`DOM`节点，哪怕一个最简单的`div`也包含着很多属性，操作`DOM`的代价仍旧是昂贵的，频繁操作还是会出现页面卡顿，影响用户的体验

  ![img](https://static.vue-js.com/cc95c7f0-442c-11eb-ab90-d9ae814b240d.png)

  **栗子**

  ```js
  <input id="a" type="text">
  <input id="b" type="text">
  <input id="c" type="text">
  <input id="d" type="text">
  <script type="text/javascript">
  // 获取4个输入框对象
  let ipt1 = document.querySelector('#a')
  let ipt2 = document.querySelector('#b')
  let ipt3 = document.querySelector('#c')
  let ipt4 = document.querySelector('#d')
  // 修改4个输入框的内容
  ipt1.value = 1
  ipt2.value = 2
  ipt3.value = 3
  ipt4.value = 4
  </script> 
  ```

  假设我们有四个input的value需要手动更新，那么传统步骤就是找到这四个input，然后分别对其value进行更改。

  由于JavaScript同步代码顺序运行，DOM操作也是同步触发的，首先在获取4个输入框对象时就会触发4次对DOM树的遍历，来碰撞相匹配的元素对象，再次是当每个DOM对象通过value属性赋值的时候，会直接触发一次视图更新，所以实际上网页是通过4次遍历和4次DOM更新来实现最终展示结果的、

  如果使用虚拟DOM

  那么首先由于当初存放了原始DOM的引用，就不会便利4次DOM树，要知道遍历DOM成本很大

  其次在虚拟DOM中对数值进行修改，不会触发DOM的更新，最后再一次性映射到视图即可

  > 至于怎么实现一次性映射的，我也不知道啊哈哈哈





### 你了解vue的diff算法吗？说说看

* **是什么**

  `diff` 算法是一种通过同层的树节点进行比较的高效算法

  vue的diff算法有两个特点

  - 比较只会在同层级进行, 不会跨层级比较
  - 在diff比较的过程中，循环从两边向中间比较

  `diff` 算法在很多场景下都有应用，在 `vue` 中，作用于虚拟 `dom` 渲染成真实 `dom` 的新旧 `VNode` 节点比较

* **方式**

  `diff`整体策略为：深度优先，同层比较

  1. 比较只会在同层级进行, 不会跨层级比较

     ![img](https://static001.infoq.cn/resource/image/91/54/91e9c9519a11caa0c5bf70714383f054.png)

  2. 比较的过程中，循环从两边向中间收拢

     ![img](https://static001.infoq.cn/resource/image/2d/ec/2dcd6ad5cf82c65b9cfc43a27ba1e4ec.png)

* **原理和过程**

  > sameVnode函数用来**判断两个几点是否可以复用**，要求首先新老节点的key必须相等，其次是标签要相同，接下来判断两个Vnode是否都具有data属性。

  1. 当数据发生改变时，`set`方法会调用`Dep.notify`通知所有订阅者`Watcher`，订阅者就会调用`patch`给真实的`DOM`打补丁，更新相应的视图
  2. `patch`函数前两个参数位为`oldVnode` 和 `Vnode` ，分别代表新的节点和之前的旧节点，主要做了四个判断：
     - 没有新节点，直接触发旧节点的`destory`钩子
     - 没有旧节点，说明是页面刚开始初始化的时候，此时，根本不需要比较了，直接全是新建，所以只调用 `createElm`
     - 旧节点和新节点自身一样，通过 `sameVnode` 判断节点是否一样，一样时，直接调用 `patchVnode`去处理这两个节点;若旧节点和新节点自身不一样，直接创建新节点，删除旧节点

  3. `patchVnode`主要做了几个判断：
     * 新节点是否是文本节点，如果是，则直接更新`dom`的文本内容为新节点的文本内容
     * 新节点和旧节点如果都有子节点，则处理比较更新子节点
     * 只有新节点有子节点，旧节点没有，那么不用比较了，所有节点都是全新的，所以直接全部新建就好了，新建是指创建出所有新`DOM`，并且添加进父节点
     * 只有旧节点有子节点而新节点没有，说明更新后的页面，旧节点全部都不见了，那么要做的，就是把所有的旧节点的子节点删除删除，也就是直接把`DOM` 删除

  4. 子节点不完全一致，则调用`updateChildren`，也就是比较新旧子序列

     * 当新老`VNode` 节点的 `start` 相同时，直接 `patchVnode` ，同时新老 `VNode` 节点的开始索引都加 1
     * 当新老 `VNode` 节点的 `end`相同时，同样直接 `patchVnode` ，同时新老 `VNode` 节点的结束索引都减 1
     * 当老 `VNode` 节点的 `start` 和新 `VNode` 节点的 `end` 相同时，这时候在 `patchVnode` 后，还需要将当前真实 `dom` 节点移动到 `oldEndVnode` 的后面，同时老 `VNode` 节点开始索引加 1，新 `VNode` 节点的结束索引减 1
     * 当老 `VNode` 节点的 `end` 和新 `VNode` 节点的 `start` 相同时，这时候在 `patchVnode` 后，还需要将当前真实 `dom` 节点移动到 `oldStartVnode` 的前面，同时老 `VNode` 节点结束索引减 1，新 `VNode` 节点的开始索引加 1
     * 如果都不满足以上四种情形，那说明没有相同的节点可以复用，则会分为以下两种情况
       1. 从旧的 `VNode`中找到与 `newStartVnode` 一致 `key` 的旧节点，再进行`patchVnode`，同时将这个真实 `dom`移动到 `oldStartVnode` 对应的真实 `dom` 的前面
       2. 若找不到，则调用 `createElm` 创建一个新的 `dom` 节点放到当前 `oldStartVnode` 的前面并使`newStartinx+1`

     * 最后把oldVnode中多余的节点删除



### Vue项目中有封装过axios吗？主要是封装哪方面的？

* **是什么**

  `axios` 是一个轻量的 `HTTP`客户端

  基于 `XMLHttpRequest` 服务来执行 `HTTP` 请求，支持丰富的配置，支持 `Promise`，支持浏览器端和 `Node.js` 端。自`Vue`2.0起，尤大宣布取消对 `vue-resource` 的官方推荐，转而推荐 `axios`。现在 `axios` 已经成为大部分 `Vue` 开发者的首选

* **特性**

  - 从浏览器中创建 `XMLHttpRequests`

  - 从 `node.js` 创建 `http`请求

  - 支持 `Promise` API

    ```js
    axios({        
      url:'xxx',    // 设置请求的地址
      method:"GET", // 设置请求方法
      params:{      // get请求使用params进行参数凭借,如果是post请求用data
        type: '',
        page: 1
      }
    }).then(res => {  
      // res为后端返回的数据
      console.log(res);   
    })
    ```

    ```js
    function getUserAccount() {
        return axios.get('/user/12345');
    }
    
    function getUserPermissions() {
        return axios.get('/user/12345/permissions');
    }
    
    axios.all([getUserAccount(), getUserPermissions()])
        .then(axios.spread(function (res1, res2) { 
        // res1第一个请求的返回的内容，res2第二个请求返回的内容
        // 两个请求都执行完成才会执行
    }));
    ```

  - 拦截请求和响应

  - 转换请求数据和响应数据，自动转换`JSON` 数据

  - 取消请求

    方法1

    ```js
    const CancelToken = axios.CancelToken;
    const source = CancelToken.source();
    
    axios.get('xxxx', {
      cancelToken: source.token
    })
    // 取消请求 (请求原因是可选的)
    source.cancel('主动取消请求');
    ```

    方法2

    ```js
    const CancelToken = axios.CancelToken;
    let cancel;
    
    axios.get('xxxx', {
      cancelToken: new CancelToken(function executor(c) {
        cancel = c;
      })
    });
    cancel('主动取消请求'); 
    ```

    

  - 客户端支持防御`XSRF`

* **为什么封装**

  `axios` 的 API 很友好，你完全可以很轻松地在项目中直接使用。不过随着项目规模增大，如果每发起一次`HTTP`请求，就要把这些比如设置超时时间、设置请求头、根据项目环境判断使用哪个请求地址、错误处理等等操作，都需要写一遍

  这种重复劳动不仅浪费时间，而且让代码变得冗余不堪，难以维护。为了提高我们的代码质量，我们应该在项目中二次封装一下 `axios` 再使用

* **具体封装**

  * **设置接口请求前缀**

    根据开发、测试、生产环境的不同，前缀需要加以区分

    ```js
    if (process.env.NODE_ENV === 'development') {
        axios.defaults.baseURL = 'http://dev.xxx.com'
    } else if (process.env.NODE_ENV === 'production') {
        axios.defaults.baseURL = 'http://prod.xxx.com'
    }
    ```

  * **请求头与超时时间**

    来实现一些具体的业务，必须携带一些参数才可以请求(例如：会员业务)

  * **封装请求方法**

    根据`get`、`post`等方法进行一个再次封装，使用起来更为方便

    > 先是对通用方法封装，这样就不用每次写axios.get了

    ```js
    // get 请求
    export function httpGet({
      url,
      params = {}
    }) {
      return new Promise((resolve, reject) => {
        axios.get(url, {
          params
        }).then((res) => {
          resolve(res.data)
        }).catch(err => {
          reject(err)
        })
      })
    }
    
    // post
    // post请求
    export function httpPost({
      url,
      data = {},
      params = {}
    }) {
      return new Promise((resolve, reject) => {
        axios({
          url,
          method: 'post',
          transformRequest: [function (data) {
            let ret = ''
            for (let it in data) {
              ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
            }
            return ret
          }],
          // 发送的数据
          data,
          // url参数
          params
    
        }).then(res => {
          resolve(res.data)
        })
      })
    }
    ```

    > 再封装出具体的请求

    ```js
    import { httpGet, httpPost } from './http'
    export const getorglist = (params = {}) => httpGet({ url: 'apps/api/org/list', params })
    ```

    > 页面中直接使用

    ```js
    // .vue
    import { getorglist } from '@/assets/js/api'
    
    getorglist({ id: 200 }).then(res => {
      console.log(res)
    })
    ```

  * **请求拦截器**

    请求拦截器可以在每个请求里加上token，做了统一处理后维护起来也方便

    ```js
    // 请求拦截器
    axios.interceptors.request.use(
      config => {
        // 每次发送请求之前判断是否存在token
        // 如果存在，则统一在http请求的header都加上token，这样后台根据token判断你的登录情况，此处token一般是用户完成登录后储存到localstorage里的
        token && (config.headers.Authorization = token)
        return config
      },
      error => {
        return Promise.error(error)
      })
    ```

  * **响应拦截器**

    响应拦截器可以在接收到响应后先做一层操作，如根据状态码判断登录状态、授权

    ```js
    // 响应拦截器
    axios.interceptors.response.use(response => {
      // 如果返回的状态码为200，说明接口请求成功，可以正常拿到数据
      // 否则的话抛出错误
      if (response.status === 200) {
        if (response.data.code === 511) {
          // 未授权调取授权接口
        } else if (response.data.code === 510) {
          // 未登录跳转登录页
        } else {
          return Promise.resolve(response)
        }
      } else {
        return Promise.reject(response)
      }
    }, error => {
      // 我们可以在这里对异常状态作统一处理
      if (error.response.status) {
        // 处理请求失败的情况
        // 对不同返回码对相应处理
        return Promise.reject(error.response)
      }
    })
    ```

> 封装没有统一的方案，按照需要来





### 说下你的vue项目的目录结构，如果是大型项目你该怎么划分结构和划分组

* **为什么要划分**

  使用`vue`构建项目，项目结构清晰会提高开发效率，熟悉项目的各种配置同样会让开发效率更高

* **怎么划分**

  在划分项目结构的时候，需要遵循一些基本的原则：

  - 文件夹和文件夹内部文件的语义一致性
  - 单一入口/出口
  - 就近原则，紧耦合的文件应该放到一起，且应以相对路径引用
  - 公共的文件应该以绝对路径的方式从根目录引用
  - `/src` 外的文件不应该被引入

* **文件夹和文件夹内部文件的语义一致性**

  我们的目录结构都会有一个文件夹是按照路由模块来划分的，如`pages`文件夹，这个文件夹里面应该包含我们项目所有的路由模块，并且仅应该包含路由模块，而不应该有别的其他的非路由模块的文件夹

  这样做的好处在于一眼就从 `pages`文件夹看出这个项目的路由有哪些

* **单一入口/出口**

  举个例子，在`pages`文件夹里面存在一个`seller`文件夹，这时候`seller` 文件夹应该作为一个独立的模块由外部引入，并且 `seller/index.js` 应该作为外部引入 seller 模块的唯一入口

  ```js
  // 错误用法
  import sellerReducer from 'src/pages/seller/reducer'
  
  // 正确用法
  import { reducer as sellerReducer } from 'src/pages/seller'
  ```





### vue要做权限管理该怎么做？如果控制到按钮级别的权限怎么做？

* **是什么**

  权限是对特定资源的访问许可，所谓权限控制，也就是确保用户只能访问到被分配的资源

  而前端权限归根结底是请求的发起权，请求的发起可能有下面两种形式触发

  - 页面加载触发
  - 页面上的按钮点击触发

  总的来说，所有的请求发起都触发自前端路由或视图

  * 路由方面，用户登录后只能看到自己有权访问的导航菜单，也只能访问自己有权访问的路由地址，否则将跳转 `4xx` 提示页
  * 视图方面，用户只能看到自己有权浏览的内容和有权操作的控件
  * 最后再加上请求控制作为最后一道防线，路由可能配置失误，按钮可能忘了加权限，这种时候请求控制可以用来兜底，越权请求将在前端被拦截

* **如何做**

  前端权限控制可以分为四个方面：

  - **接口权限**
  - **路由权限**
  - **按钮权限**
  - **菜单权限**

* **接口权限**

  > 也就是请求那道方防线

  接口权限目前一般采用`jwt`的形式来验证，没有通过的话一般返回`401`，跳转到登录页面重新进行登录

  可以通过请求拦截器

  ```js
  axios.interceptors.request.use(config => {
      // 统一加token
      config.headers['token'] = cookie.get('token')
      return config
  })
  axios.interceptors.response.use(res=>{},{response}=>{
      if (response.data.code === 40099 || response.data.code === 40098) { //token过期或者错误
          router.push('/login')
      }
  })
  ```

* **路由鉴权**

  1. **路由标记**

     初始化即挂载全部路由，并且在路由上标记相应的权限信息，每次路由跳转前做校验

     > 使用meta

  2. **路由守卫**

     在守卫中获取用户的权限信息，然后筛选又权限访问的路由

* **菜单权限**

  1. 菜单与路由分离，菜单由后端返回
  2. 菜单和路由都由后端返回

  > 也就是由后端鉴权后返回只有这个用户能使用的菜单或者路由





### Vue项目中你是如何解决跨域的

* **如何解决**

  Vue中主要通过Proxy进行跨域，

* **方案一**

  如果是通过`vue-cli`脚手架工具搭建项目，我们可以通过`webpack`为我们起一个本地服务器作为请求的代理对象

  通过该服务器转发请求至目标服务器，得到结果再转发给前端，但是最终发布上线时如果web应用和接口服务器不在一起仍会跨域

  > 这是正向代理，因为告诉了代理服务器目标地址

  ```js
  amodule.exports = {
      devServer: {
          host: '127.0.0.1',
          port: 8084,
          open: true,// vue项目启动时自动打开浏览器
          proxy: {
              '/api': { // '/api'是代理标识，用于告诉node，url前面是/api的就是使用代理的
                  target: "http://xxx.xxx.xx.xx:8080", //目标地址，一般是指后台服务器地址
                  changeOrigin: true, //是否改变源信息
                  pathRewrite: { // pathRewrite 的作用是把实际Request Url中的'/api'用""代替
                      '^/api': "" 
                  }
              }
          }
      }
  }
  ```

* **方案二**

  可以自己搭建一个服务器代理

  ```js
  var express = require('express');
  const proxy = require('http-proxy-middleware')
  const app = express()
  app.use(express.static(__dirname + '/'))
  app.use('/api', proxy({ target: 'http://localhost:4000', changeOrigin: false
                        }));
  module.exports = app
  ```

* **方案三**

  配置ngix

  > 不熟悉





### 你是怎么处理vue项目中的错误的？

* **错误类型**

  主要的错误来源包括：

  - 后端接口错误
  - 代码中本身逻辑错误

* **后端接口错误**

  通过`axios`的`interceptor`实现网络请求的`response`先进行一层拦截

  ```js
  apiClient.interceptors.response.use(
    response => {
      return response;
    },
    error => {
      if (error.response.status == 401) {
        router.push({ name: "Login" });
      } else {
        message.error("出错了");
        return Promise.reject(error);
      }
    }
  )
  ```

* **代码本身逻辑错误**

  1. **全局设置错误处理**

     ```js
     Vue.config.errorHandler = function (err, vm, info) {
       // handle error
       // `info` 是 Vue 特定的错误信息，比如错误所在的生命周期钩子
       // 只在 2.2.0+ 可用
     }
     ```

  2. **生命周期钩子**

     `errorCaptured`是 2.5.0 新增的一个生命钩子函数，当捕获到一个来自子孙组件的错误时被调用

     > * 如果全局的 `config.errorHandler` 被定义，所有的错误仍会发送它
     > * 如果一个组件的继承或父级从属链路中存在多个 `errorCaptured` 钩子，则它们将会被相同的错误逐个唤起
     > * 如果此 `errorCaptured` 钩子自身抛出了一个错误，则这个新错误和原本被捕获的错误都会发送给全局的 `config.errorHandler`
     > * 一个 `errorCaptured` 钩子能够返回 `false` 以阻止错误继续向上传播

     ```js
     (err: Error, vm: Component, info: string) => ?boolean
     ```

     

  

### computed与watch的区别是么

* **watch 属性监听**
  
  * 是一个对象，键是需要观察的属性，值是对应回调函数，主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作
  * 监听属性的变化，需要在数据变化时执行异步或开销较大的操作时使用
  
* **computed 计算属性**
  
  * 属性的结果会被缓存，当`computed`中的函数所依赖的属性没有发生改变的时候，那么调用当前函数的时候结果会从缓存中读取，除非依赖的响应式属性变化时才会重新计算
  * 主要当做属性来使用 
  * computed中的函数必须用return返回最终的结果
  *  computed更高效，优先使用
  
* 使用场景

  * 当一个属性受多个属性影响的时候使用，用computed
  * 当一条数据影响多条数据的时候使用，用watch

  



### vue响应式原理

* 当你把一个普通的 JavaScript 对象传入 Vue 实例作为 `data` 选项，Vue 将遍历此对象所有的 property，并使用 [`Object.defineProperty`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 把这些 property 全部转为 [getter/setter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_Objects#定义_getters_与_setters)。
* 每个组件实例都对应一个 **Watcher** 实例，它会在组件渲染的过程中把`接触`过的数据`property`记录为依赖。之后当依赖项的`setter`触发时，会通知`watcher`，从而使它关联的组件重新渲染

> 就是getter的时候收集依赖，在set的时候通知更新

* 如果设置状态改变的值和之前的一样，没变，或者设置的状态根本没有被收集，那就不会做更新的操作`vm._update`，更不会触发`beforeUpdate()`函数

* 在Vue挂载的时候，会生成一个`watcher`,`updateComponent`中使用到的数据会收集这个`watcher`,当数据改变的时候，这个`watcher`得到更新，重新获取一次数据

  ```js
  new Watcher(vm, updateComponent, noop, {
      before () {
        if (vm._isMounted && !vm._isDestroyed) {
          callHook(vm, 'beforeUpdate')
        }
      }
    }, true /* isRenderWatcher */)
  ```

  

### vue-router工作原理，有几种模式

* **工作原理**

  1. url改变
  2. 触发监听事件
  3. 改变vue-router里面的current变量
  4. 监视current变量（变量的监视者）
  5. 获取对应的组件
  6. render新组件

* 模式

  1. **hash模式**
  
     1. location.hash 的值实际就是`URL`中`#`后面的东西 它的特点在于：hash 虽然出现 URL 中，但不会被包含在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。
     2. 每一次改变 hash（window.location.hash），都会在浏览器的访问历史中增加一个记录利用 hash 的以上特点，就可以来实现前端路由`更新视图但不重新请求页面`的功能了
     2. 只改变了hash浏览器不会发送请求
     2. 监听 window 的 onhashchange 事件，当散列值改变时，可以通过 location.hash 来获取和设置hash值
  
     ```js
     // 定义Router
     class Router {
         constructor() {
             this.routes = {} // 存放路由path以及callback
             this.currentUrl = ""
     
             // 监听change调用相对应的路由回调
             // 注意要把this传进去
             window.addEventListener('load', this.refresh, false);
             window.addEventListener('hashchange', this.refresh, false);
         }
     
         // 配置一个路由的函数
         route(path, callback) {
             this.routes[path] = callback
         }
     
         // push一个路径的时候
         push(path) {
             // 修改浏览器的路径
             window.location.hash = path
             this.routes[path] && this.routes[path]()
         }
     
     
         // 这个比较难搞，因为不能够获取到那个实例
         refresh(){
     
         }
     }
     // 使用Router
     window.myRouter = new Router()
     myRouter.route('/', () => console.log('page1'))
     myRouter.route('/page2', () => console.log('page2'))
     myRouter.push('/') // page1  
     myRouter.push('/page2') // page2 
     ```
  
     
  
  2. **history模式**
  
     * window.history 属性指向 History 对象，它表示当前窗口的浏览历史。当发生改变时，只会改变页面的路径，不会刷新页面
     
     * 浏览器工具栏的“前进”和“后退”按钮，其实就是对 History 对象进行操作。
     
     * **History.pushState(state,title,url)**
       
       * 该方法用于在历史中添加一条记录。pushState()方法`不会触发页面刷新`(不会自动加载url)，只是导致 History 对象发生变化，地址栏会有变化
       
         > 刷新页面会触发新的url请求
       
       * 注意push的网址和当前的网址要同源，不然会报错
       
       > 所以下面代码要启动服务才行
       
     * **onPopstate**
     
       在浏览器后退按钮或者在调用`history.back()`的时候触发
     
     ```js
     // 定义Router
     class Router {
         constructor() {
             this.routes = {}
             // 对popState进行监听
             // 这个是监听回退行为的
             window.addEventListener('popstate', e => {
                 const path = e.state && e.state.path;
                 this.routers[path] && this.routers[path]()
             })
         }
     
         // 初始化
         init(path) {
             // 第一个参数是记录，第二个是传递简短标题，第三个是url
             history.replaceState({ path: path }, null, path)
             this.routes[path] && this.routes[path]()
         }
     
         // 创建路由
         route(path, callback) {
             this.route[path] = callback
         }
     
         // 改变状态
         push(path) {
             history.pushState({ path: path }, null, path)
             this.route[path] && this.route[path]()
         }
     
     }
     
     // 使用router
     window.myRoute = new Router()
     myRoute.route('/', () => console.log('page1'))
     myRoute.route('/page2', () => console.log('page2'))
     
     myRoute.push('/page2')
     ```
     
     
  
  

### has模式用哪个api监听路由的变化的

* 用addEventListener监听变化`onHashChange`，修改current
* 然后由于`current`用defineReactive设置了响应式

### vueX工作原理

Vuex 通过 Vue 的插件系统将 store 实例从根组件中`注入`到所有的子组件里。且子组件能通过 `this.$store` 访问到





### Vue 事件绑定原理

* 原生事件绑定是通过 `addEventListener` 绑定给真实元素的
* 组件事件绑定是通过 Vue 自定义的`$on`实现的,如果要在组件上使用原生事件，需要加.native 修饰符，这样就相当于在父组件中把子组件当做普通 html 标签，然后加上原生事件

* $on、$emit 是基于发布订阅模式的，维护一个事件中心，$on 的时候将事件按名称存在事件中心里，称之为订阅者，然后 $emit 将对应的事件进行发布，去执行事件中心里的对应的监听器



### vue-router 动态路由是什么 有什么问题

* **概念**

  把某种模式匹配到的所有路由，全都映射到同个组件.例如，我们有一个 User 组件，对于所有 ID 各不相同的用户，都要使用这个组件来渲染。那么，我们可以在 vue-router 的路由路径中使用“动态路径参数”(dynamic segment) 来达到这个效果

* **问题**---组件复用问题

  使用带有参数的路由时需要注意的是，当用户从 `/users/johnny` 导航到 `/users/jolyne` 时，**相同的组件实例将被重复使用**。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。**不过，这也意味着组件的生命周期钩子不会被调用**，所以发送请求的时候就不能在钩子发送了

* **解决方法**

  1. **通过watch监听路由参数再发送请求**

     > 虽然data数据没改变，但是直接通过路由得到新的ID，再改

     ```js
     watch: { //通过watch来监听路由变化
      	"$route": function(){
      	    this.getData(this.$route.params.xxx);
         }
     }
     ```

  2. **使用veforeRouteUpdate守卫**

     ```js
     const User = {
       template: '...',
       async beforeRouteUpdate(to, from) {
         // 对路由变化做出响应...
         this.userData = await fetchUser(to.params.id)
       },
     }
     ```

  3. **通过:key阻止组件复用**

     ```js
     <router-view :key="$route.fullPath" />
     ```

  

#### 说说Vue SSR

SSR 也就是服务端渲染，也就是将 Vue 在客户端把标签渲染成 HTML 的工作放在服务端完成，然后再把 html 直接返回给客户端

* **优点**

  1. SSR 有着更好的 SEO

     > 搜索引擎爬虫抓取工具可以直接查看完全渲染的页面

  2. 并且首屏加载速度更快

* **缺点**
  
  1.  开发条件会受到限制，服务器端渲染只支持 beforeCreate 和 created 两个钩子
  2. 服务器会有更大的负载需求





### Vuex为何叫做Vuex

* 因为他是专门为Vue开发的
* 因为他是用Vue开发的，实际上就是个Vue实例



### 路由懒加载是怎样实现的

我们通过import引入路由组件，通过Webpack编译打包后，会把每个路由组件的代码分割成一一个bendule文件,而不是耦合在一个bundle。初始化时不会加载这些bundle，只当激活路由组件才会去加载对应的js文件



### keep-alive如何限制缓存数

- `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。
- `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
- `max` - 数字。最多可以缓存多少组件实例。



### Element-ui表单验证原理

* **方法**

  1. 获取用户传的rules进行验证，主要是安装了[async](https://so.csdn.net/so/search?q=async&spm=1001.2101.3001.7020)-validator插件

  2. 点击提交按钮验证所有[表单](https://so.csdn.net/so/search?q=表单&spm=1001.2101.3001.7020)，主要是触发了父组件el-form的`validate`，`validate`会查找所有el-form-item，然后调用el-form-item的validate。
     el-form.vue

     > 也可以自己定义用哪个validate方法

  3. 通过rules里设置的trigger去触发验证的话，实际上是靠子组件，比如el-input进行发布订阅。然后触发el-form-item的validate





### Vue是如何在数据变化的时候重新更新组件的

* 每个组件实例`对应`（不是存在）一个`watcher`
* 当组件`读取`某个数据的时候，`watcher`就会被这个数据收集
* 当这个数据改变的时候，就会提醒这些`watcher`
* 重新执行render函数，生成新的newVnode
* 然后就是`patch`的过程





### scoped的实现原理

- 给HTML的DOM节点加一个不重复属性`data-v-469af010`标志唯一性
- 在添加`scoped`属性的组件的每个样式选择器后添加这个属性，也就是属性选择器
- 如果组件内部还有组件，只会给最外层的组件里的标签加上唯一属性字段，不影响组件内部引用的组件
- 慎用
  1. 父组件无`scoped`属性，子组件带有`scoped`，父组件是无法操作子组件的样式的（原因在原理中可知），虽然我们可以在全局中通过该类标签的标签选择器设置样式，但会影响到其他组件
  2. 父子组建都有，同理也无法设置样式，更改起来增加代码量







