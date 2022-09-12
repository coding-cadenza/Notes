

### 什么是作用域、作用域链

* 作用域负责收集和维护由所有声明的标识符（变量）组成的一系列查询，并实施一套非常严格的规则，确定当前执行的代码对这些标识符的访问权限(全局作用域、函数作用域、块级作用域)
* 作用域链就是从当前作用域开始一层一层向上寻找某个变量，直到找到全局作用域还是没找到，就宣布放弃。这种一层一层的关系，就是作用域链

### let const var

* **var**
  1. 在变量未赋值时，变量为undefined（为使用声明变量时也为undefined）
  2. var的作用域为方法作用域
  
  3. 可以重复声明
  
* **let**
  1. 在变量为声明前直接使用会报错
  2. 作用域为块作用域
  3. let禁止重复声明变量
  
* **const**

  1. const为常量声明方式；声明变量时必须初始化，在后面出现的代码中不能再修改该常量的值

  2. const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动





### let a = "sssssss"，存在哪儿？

使用let声明的全局变量不是挂在window对象下的，声明的全局变量存在于一个块级作用域中。

![img](https://uploadfiles.nowcoder.com/images/20220301/4107856_1646126617426/B742135235F1E65B51FA2D04FF2A9F43)

###  js数据类型，区别

* **基本数据类型：**

  Number，String，Boolean，null，undefined，symbol，bigint（后两个为ES6新增）

* **引用数据类型：**

  object，function（**proto** Function.prototype）

  > object：普通对象，数组对象，正则对象，日期对象，Math数学函数对象。

* **数据存储方式：**
  1. 基本数据类型是直接存储在栈中的简单数据段，占据空间小、大小固定，属于被频繁使用的数据。栈是存储基本类型值和执行代码的空间。
  2. 引用数据类型是存储在堆内存中，占据空间大、大小不固定。引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址，当解释器寻找引用值时，会检索其在栈中的地址，取得地址后从堆中获得实体。

* **区别：**
  1. 堆比栈空间大，栈比堆运行速度快。
  2. 堆内存是无序存储，可以根据引用直接获取。
  3. 基础数据类型比较稳定，而且相对来说占用的内存小。
  4. 引用数据类型大小是动态的，而且是无限的。



### Object.assign的理解

* **作用**

  Object.assign可以实现对象的合并

* **语法**

  Object.assign(target, ...sources)

* **注意点**

  1. Object.assign会将source里面的可枚举属性复制到target，如果和target的已有属性重名，则会覆盖。
  2. 后续的source会覆盖前面的source的同名属性。
  3. Object.assign复制的是属性值，如果属性值是一个引用类型，那么复制的其实是引用地址，就会存在引用共享的问题。



### map 和 forEach 的区别

**相同点：**

1. 都是循环遍历数组中的每一项
2. 每次执行匿名函数都支持三个参数，参数分别为item（当前每一项），index（索引值），arr（原数组）
3. 匿名函数中的this都是指向window
4. 只能遍历数组

**不同点：**

1. map()会分配内存空间存储新数组并返回，forEach()不会返回数据。
2. forEach()允许callback更改原始数组的元素。map()返回新的数组。



###  for of 可以遍历哪些对象

它是es6新增的一个遍历方法，但**只限于挂在了迭代器(iterator)**的对象, 所以普通的对象用for..of遍历是会报错的。

可迭代的对象：包括Array, Map, Set, String, TypedArray, arguments对象等等



### js静态类型检查

* **静态类型语言**

  类型检查发生在编译阶段，因此除非修复错误，否则会一直编译失败

* **动态类型语言**

  只有在程序运行了一次的时候错误才会被发现，也就是在运行时，因此即使代码中包含了会 在运行时阻止脚本正常运行的错误类型，这段代码也可以通过编译。**js是动态类型检查。**

* **js静态类型检查的方法**

  **TypeScript**是一个会编译为JavaScript的超集（尽管它看起来几乎像一种新的静态类型语言）

* **使用静态类型的优势**
  - 可以尽早发现bug和错误
  - 减少了复杂的错误处理
  - 将数据和行为分离
  - 减少单元测试的数量
  - 提供了领域建模（domain modeling）工具
  - 帮助我们消除了一整类bug
  - 重构时更有信心

* **使用静态类型的劣势**
  - 代码冗长
  - 需要花时间去掌握类型



### 说说 indexof

* **语法**

  ```js
  str.indexOf(searchValue [, fromIndex])
  ```

* **searchValue**
  * 如果没有提供确切地提供字符串，[searchValue 会被强制设置为"undefined"]， 然后在当前字符串中查 找这个值。

* **fromIndex**

  * 可选，默认值为0。

  * 如果fromIndex的值小于0，或者大于str.length，那么查找分别从0和str.length开始

    > 所以大于str.length找到的都是-1

* **返回值**

  * 查找的字符串searchValue的**第一次**出现的索引，如果没有找到，则返回-1。

  * 若被查找的字符串searchValue是一个空字符串，则返回fromIndex

    > formindex小于0为0，大于长度为长度

* **特点**
  * 严格区分大小写，在使用indexOf检索数组时，用‘===’去匹配，意味着会检查数据类型





### iframe有什么优点、缺点

* **优点**
  1. iframe能够原封不动的把嵌入的网页展现出来。
  2. 如果有多个网页引用iframe，那么你只需要修改iframe的内容，就可以实现调用的每一个页面内容的更改，方便快捷。
  3. 网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用iframe来嵌套，可以增加代码的可重用。
  4. 如果遇到加载缓慢的第三方内容如图标和广告，这些问题可以由iframe来解决。

* **缺点**
  1. iframe会阻塞主页面的onload事件
  2. iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。会产生很多页面，不容易管理。
  3. iframe框架结构有时会让人感到迷惑，如果框架个数多的话，可能会出现上下、左右滚动条，会分散访问者的注意力，用户体验度差。
  4. 不利于SEO
  5. 很多的移动设备无法完全显示框架，设备兼容性差
  6. 增加服务器的http请求，对于大型网站是不可取的







### webComponents

**Web Components** 总的来说是提供一整套完善的封装机制来把 Web 组件化这个东西标准化，每个框架实现 的组件都统一标准地进行输入输出，这样可以更好推动组件的复用。包含四个部分

* **Custom Elements**

  支持 Web Components 标准的浏览器会提供一系列 API 给开发者用于创建自定义的元素，或者扩展现有元素。

* **HTML Imports**

  一种在 HTMLs 中引用以及复用其他的 HTML 文档的方式。

* **HTML Templates**

  模板

* **Shadow DOM**

  提供一种更好地组织页面元素的方式，来为日趋复杂的页面应用提供强大支持，避免代码间的相互影响

### 变量提升

* JavaScript是单线程语言，所以执行肯定是按顺序执行。但是并不是逐行的分析和执行，而是一段一段地分析执行，会先进行编译阶段然后才是执行阶段
* 在编译阶段阶段，代码真正执行前的几毫秒，会检测到所有的变量和函数声明，所有这些函数和变量声明都被添加到名为Lexical Environment的JavaScript数据结构内的内存中。所以这些变量和函数能在它们真正被声明之前使用。



###  HashMap和Object

Objects和Maps类似的是，它们都允许你按键存取一个值、删除键、检测一个键是否绑定了值。但是他们会有一定的区别

|          | map                                                          | Object                                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 意外的键 | Map默认情况不包含任何键。只包含显式插入的键。                | 一个Object有一个原型, 原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。**注意:** 虽然 ES5 开始可以用Object.create(null)来创建一个没有原型的对象，但是这种用法不太常见。 |
| 键的类型 | 一个Map的键可以是**任意值**，包括函数、对象或任意基本类型。  | 一个Object的键必须是一个 [String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String) 或是[Symbol](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)。 |
| 键的顺序 | Map中的 key 是有序的。因此，当迭代的时候，一个Map对象以插入的顺序返回键值。 | 一个Object的键是无序的注意：自ECMAScript 2015规范以来，对象*确实*保留了字符串和Symbol键的创建顺序； 因此，在只有字符串键的对象上进行迭代将按插入顺序产生键。 |
| Size     | Map的键值对个数可以轻易地通过[size](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map/size) 属性获取 | Object的键值对个数只能手动计算                               |
| 迭代     | Map是 [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/iterable) 的，所以可以直接被迭代。 | 迭代一个Object需要以某种方式获取它的键然后才能迭代。         |
| 性能     | 在频繁增删键值对的场景下表现更好。                           | 在频繁添加和删除键值对的场景下未作出优化。                   |







###  null 和 undefined 的区别

* **区别**
  * undefined 表示一个变量自然的、最原始的状态值,其会出现在以下场景
    1. 声明了一个变量，但没有赋值
    2. 访问对象上不存在的属性
    3. 函数定义了形参，但没有传递实参
    4. 使用 void 对表达式求值
  * null 则表示一个变量被人为的设置为空对象，而不是原始状态，js不会讲一个值设置为null，它是用来让程序员表明变量没有值的
  * `undefined`不是一个有效的`JSON`，而`null`是；
  * `null` 和 `undefined` 的值相等，但类型不等：`undefined`的类型(`typeof`)是`undefined`；`null`的类型(typeof)是`object`。
  * 在`null`上执行算术转换时，则值为0，`undefined`不执行任何此类转换。如果尝试将`undefined`添加到数字中，将获得`NaN`



### 数组和伪数组以及其区别

* **定义**
  * 数组是一个特殊对象,与常规对象的区别：
    - 当由新元素添加到列表中时，自动更新length属性
    - 设置length属性，可以截断数组
    - 从Array.protoype中继承了方法
    - 属性为'Array'
  * 类数组是一个拥有length属性，并且他属性为非负整数的普通对象，类数组不能直接调用数组方法

* **区别**

  类数组是简单对象，它的原型关系与数组不同

* **转换**

  * 方法
    - 使用Array.from()
    - 使用Array.prototype.slice.call()
    - 使用Array.prototype.forEach()进行属性遍历并组成新的数组

  * 须知

    转换后的数组长度由length属性决定，索引不连续时转换结果是连续的,并且只考虑0或者正数的索引

    ```js
    let al1 = {
        length: 4,
        0: 0,
        a: 6,
        1: 1,
        3: 3,
        4: 4,
        5: 5,
    };
    console.log(Array.from(al1)) // [0, 1, undefined, 3]
    ```

* **小知识**

  使用push操作的时候，操作的是索引值为length的位置

  ```js
    let arrayLike2 = {
      2: 3,
      3: 4,
      length: 2,
      push: Array.prototype.push
    }
  
    // push 操作的是索引值为 length 的位置
    arrayLike2.push(1);
    console.log(arrayLike2); // {2: 1, 3: 4, length: 3, push: ƒ}
    arrayLike2.push(2);
    console.log(arrayLike2); // {2: 1, 3: 2, length: 4, push: ƒ}
  ```





###  介绍下 Set、Map、WeakSet 和 WeakMap 的区别？

* **Set**
  1. 成员不能重复；
  2. 只有键值，没有键名，有点类似数组；
  3. 可以遍历，方法有add、delete、has
* **WeakSet**
  1. 成员都是对象（引用）；
  2. 成员都是弱引用，随时可以消失（不计入垃圾回收机制）
  3. 不能遍历，方法有add、delete、has；

* **Map**

  1. 本质上是键值对的集合，类似集合；
  2. 可以遍历，方法很多，可以跟各种数据格式转换；

* **WeakMap**

  1. 只接收对象为键名（null 除外），不接受其他类型的值作为键名；
  2. 键名指向的对象，不计入垃圾回收机制；
  3. 不能遍历，方法同get、set、has、delete；

  > ```js
  > let obj = { name: 'fedaily' }
  > const map = new Map()
  > map.set('account', obj)
  > map.get('account') // { name: 'fedaily' }
  > obj = null // 这里将obj置为null
  > map.get('account') // 这里其实obj值还在 { name: 'fedaily' }
  > ```
  >
  > 这里有两个引用，一个是obj，一个是map，所以obj不用了但是没被回收
  >
  > 但是如果换成WeakMap，就会回收

### 简单说说 js 中有哪几种内存泄露的情况

1. 意外的全局变量；
2. 闭包；
3. 未被清空的定时器；
4. 未被销毁的事件监听；
5. DOM 引用；



### json和xml数据的区别

1. 数据体积方面：xml是重量级的，json是轻量级的，传递的速度更快些。
2. 数据传输方面：xml在传输过程中比较占带宽，json占带宽少，易于压缩。
3. 数据交互方面：json与javascript的交互更加方便，更容易解析处理，更好的进行数据交互
4. 数据描述方面：json对数据的描述性比xml较差
5. xml和json都用在项目交互下，xml多用于做配置文件，json用于数据交互。



### JavaScript有几种方法判断变量的类型

* **typeof方法**

  当需要判断变量是否是number, string, boolean, function, undefined等类型时，可以使用typeof进行判断

* **instanceof操作符（基于原型链）**

  1. 左边操作数obj为对象，右边操作数Object为`函数对象或者是函数构造器，否则抛出TypeError`

     > 因为要访问fn.prototype,对象是不能直接访问的

  2. **instanceof操作符判断左操作数对象的原型链上是否有右边这个构造函数的prototype属性**

  3. **指定对象是否是某个构造函数的实例**

  4. instanceof对整个原型链上的对象都有效，因此同一个实例对象，可能会对多个构造函数都返回true

* **Object.prototype.isPrototypeOf()**

  这个和上面那个类似，但是两边都是对象

  > a.isPrototypeOf(b) // 判断a在b的原型链上是否存在
  >

* **Object.prototype.toString**

  [![H5GcOe.png](https://s4.ax1x.com/2022/02/17/H5GcOe.png)](https://imgtu.com/i/H5GcOe)

* **constructor属性**

  所有实例对象都有constructor属性，constructor属性指向prototype对象所在的构造函数，就是说指向创建这个实例的构造函数







### **for循环setTimeout输出1-10解决方式**

1. **setTieOut第三个参数**

   > 箭头函数形成了自己的作用域，setTimeOut第三个参数可以传参

   ```js
   for (var i = 0; i< 10; i++){
      setTimeout((i) => {
         console.log(i)
      }, 1000,i);
   }
   ```

2. **let**

3. **IEEE**

   ```js
   for (var i = 0; i< 10; i++){
     ((i)=>{
       setTimeout(() => {
         console.log(i)
       },1000);
     })(i)
   }
   ```

4. **利用try和catch形成作用域**

   ```js
   for (var i = 0; i< 10; i++){
         try{
           throw i
         }catch(i){
           setTimeout(() => {
             console.log(i)
           }, 1000)
         }
   }
   ```






### call appy bind的作用和区别

* **作用**
  * 都可以改变函数内部的this指向
* **区别**
  * call 和 apply 会调用函数，并且改变函数内部this指向
  * call 和 apply 传递的参数不一样，call 传递参数arg1,arg2...形式 apply 必须数组形式[arg]
  * bind 不会调用函数，可以改变函数内部this指向

* **主要应用场景**

  * call 经常做继承

  * apply 经常跟数组有关系，比如借助于数学对象实现数组最大值最小值

    ```js
    const arr = [1, 22, 3, 44, 5, 66, 7, 88, 9];
    const max = Math.max.apply(Math, arr);
    console.log(max);
    ```

  * bind 不调用函数，但是还想改变this指向，比如改变定时器内部的this指向

    ```JS
    btns.onclick = function() {
        this.disabled = true;
        setTimeout(
            function() {
                this.disabled = false;
            }.bind(this),
            2000
        );
    };
    ```

    

### this绑定

当一个函数被调用时，会创建一个活动记录(执行上下文)。这个记录会包含函数在哪里被调用(调用栈)、函数的调用方法、传入的参数等信息。

this就是记录中的一个属性，会在函数执行的过程中用到

* **默认绑定**

  全局环境中，this默认绑定到window

  > 严格模式中绑定到undefined

* **隐式绑定**

  当函数引用有上下文对象时，隐式绑定规则会把函数调用中的 this 绑定到这个上下文对象

  > 对象属性引用链中只有最顶层或者说`最后一层`会影响调用位置，其实就是这个根本是obj2调用的
  >
  > obj1.obj2.foo();// 这个最后this指向的是obj2

* **隐式丢失**

  隐式丢失是指被隐式绑定的函数丢失绑定对象，从而绑定由调用的位置决定

  ```js
  function foo() { console.log( this.a );}
  var obj = { a: 2,foo: foo };
  var bar = obj.foo; // 函数别名！
  var a = "oops, global"; // a 是全局对象的属性
  bar(); // "oops, global
  ```

  ```js
  let obj = {
      getThis: function () {
          return function () {
              console.log(this);
          }
      }
  }
  obj.getThis()(); //window
  ```

  ```js
  function foo() { console.log( this.a );}
  function doFoo(fn) {
  	this.a = "111111";
  	fn(); // <-- 调用位置！
  }
  var obj = { a: 2,foo: foo };
  var a = "oops, global"; // a 是全局对象的属性
  doFoo( obj.foo ); // "111111"
  ```

  > 函数做作为回调函数也会消失绑定，因为回调函数最后其实在全局下执行的

  
  
* **显示绑定**

  就是上面三个绑定函数了

* **new绑定**

  new绑定绑定到创建的实例上了

  ```js
  function foo(a) { 
   this.a = a;
  } 
  var bar = new foo(2);
  console.log( bar.a ); // 2
  ```

  

### 箭头函数的this

* 箭头函数中的this是在**函数定义的时候**就确定下来的，而不是在函数调用的时候确定的

* 箭头函数中的this指向父级作用域的执行上下文

  > 因为这个this不是自己的，所以在定义的时候就会取到父级的this

* 箭头函数无法使用apply、call和bind方法改变this指向，**因为其this值在函数定义的时候就被确定下来**

  ```js
  let obj = {
      getThis: function () {
          return  ()=> {
              console.log(this);
          }
      }
  }
  obj.getThis()(); //obj!!!!
  
  // 代码中有两个箭头函数，由于找不到对应的function，所以this会指向window对象。
  // obj没有上下文的哦
  let obj = {
      getThis: ()=> {
          return  ()=> {
              console.log(this);
          }
      }
  }
  obj.getThis()(); //window
  ```

  



### js继承的方法和优缺点

* **原型链继承**

  * 描述
    * 将父类的实例作为子类的原型

  * 优点
    * 可继承父类构造函数的属性，父类原型的属性

  * 缺点
    * 无法实现多继承，一个子类只能继承一个父类
    * 无法向父类构造函数传参
    * 一个子类更改共有属性会影响到其他子类

  ```js
  function Cat(color){
      this.color = color 
  }
  Cat.prototype = new Animal('Tom')
  
  let cat = new Cat('white')
  ```

* **构造函数继承**

  * 描述
    * 使用符类的构造函数来增强子类实例
  * 优点
    * 可以实现多继承
    * 可以向父类构造函数传参
  * 缺点
    * 无法继承父类的原型属性和方法

  ```js
  function Cat(name,color){
      Animal.call(this,name)
      this.color = color
  }
  
  let myCat = new Cat('Tom','white')
  ```

* **组合继承**

  * 描述
    * 组合继承就是原型链继承和构造继承
  * 缺点
    * 执行两次父类的构造函数

  ```js
  function Cat(name, color) {
      Animal.call(this, name);
      this.color = color;
  }
  Cat.prototype = new Animal()
  
  let myCat = new Cat('Tom','white')
  ```

* **寄生组合继承**

  * 描述

    通过寄生，砍掉父类的实例，只需要原型属性和方法

  ```js
  function Parent(name){
      this.name=name
  }
  Parent.prototype.head=function(){
      console.log('有着浓密的头发');
  }
  
  function Child(name,school){
      Parent.call(this,name)
      this.school = school
  }
  
  // Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的__proto__
  Child.prototype  = Object.create(Parent.prototype)
  
  // 因为改变了孩子的原型，所以孩子原型上的constructot要变回来
  Child.prototype.constructor = Child
  
  let child = new Child('小明',20)
  console.log(child);
  ```

* **拷贝继承**

  ```js
  function Cat(name){
    var animal = new Animal();
    for(var p in animal){
      Cat.prototype[p] = animal[p];
    }
    this.name = name
  }
  ```

* **实例继承**

  实例是父类的实例，不是子类的实例

  ```js
  function Cat(name, color) {
      let instance = new Animal(name)
      instance.color = color;
      return instance
  }
  ```

  





### new会发生什么

1. 创建一个空对象

2. 将空对象的`__proto__`属性指向构造函数的prototype

   > 箭头函数没有prototype，所以不能new

3. 绑定构造函数的this指向这个对象，执行构造函数

   > 所以，bind要判断，因为先绑定在执行，bind在执行的时候又做绑定

4. 执行后是否返回这个对象视构造函数的返回值定







### 箭头函数

* **基本语法**

  * 参数

    1. 如果没有参数，直接写空括号
    2. 如果只有一个参数，可以省略括号

  * 函数体

    1. 如果只有一句代码，简单返回某个变量或者返回一个简单的JS表达式，可以省去函数体的大括号{ }

    2. 如果只有一句代码，简单返回一个对象，可以只在外面包裹一个小括号

    3. 如果只有一条语句并且返回值（最常见是调用一个函数），在前面加个void

       ```js
       let fn = () => void doesNotReturn();
       ```

* **与普通函数的区别**

  1. 语法简洁、清晰

  2. 不会创建自己的this

     > 会在定义时获取外层执行环境的this，并继承这个值，`并且不会在执行时改变`

     ```js
     var id = 'Global';
     
     function fun1() {
         // setTimeout中使用普通函数
         setTimeout(function(){
             console.log(this.id);
         }, 2000);
     }
     
     function fun2() {
         // setTimeout中使用箭头函数
         setTimeout(() => {
             console.log(this.id);
         }, 2000)
     }
     
     fun1.call({id: 'Obj'});     // 'Global'  
     
     fun2.call({id: 'Obj'});     // 'Obj'
     
     // 两个回调函数其实最后都是在window环境调用,但是func2的this已经订好了所以
     ```

  3. call()/.apply()/.bind()无法改变箭头函数中this的指向

  4. 箭头函数不能作为构造函数使用
     * 首先箭头函数不能改变实例的this
     * 其次因为箭头函数没有prototype，所以new一个箭头函数会报错

  5. 箭头函数没有自己的arguments对象
     * 要是能访问到肯定是作用域链上面找的

  6. 箭头函数不能作为Generator函数



### JS对象属性枚举

* **Object.getOwnPropertyNames()**

  `包括`不可枚举属性但`不包括`Symbol

* **Object.getOwnPropertySymbols()**

  所有Symbol属性，包括不可枚举的Symbol属性

* **Reflect.ownKeys()**

  上面两个的结合

* **Object.keys()**

  不返回`Symbol`和不可枚举的属性

> 上面这些都不返回原型链上的属性

* **sfor...in...**

  考虑原型链上的,除`symbol`和`不可枚举之外

* **Object.entries()**

  自身可枚举属性的键值对数组

  ```js
  let lsc = {
    name: 'lsc',
    age: '21',
    height: 187
  };
  console.log(Object.entries(lsc)); // [ [ 'name', 'lsc' ], [ 'age', '21' ], [ 'height', 187 ] ]
  ```

  





### ES6新特性汇总

1. 增加了`let`、`const`声明变量，有`块级作用域`

2. `解构赋值`

3. `拓展了原生对象的方法`

   * String

     支持字符串遍历（因为iterator）、repeat()等方法的支持、**模板字符串**

     > repeat是复制加长，做题的时候就不用自己复制加长了

   * Function

     **函数参数默认值**、rest参数、**函数内部严格模式**、函数的name属性、**箭头函数**

   * Array

     **扩展运算符...**

   * Object

     支持**简写**、对象中函数声明可以省略function；支持**属性名表达式**、函数名表达式。

     > 属性名表达式:["xxx"+"yyy"],
     >
     > 函数名表达式:差不多
     >
     > 简写和表达式不能同时存在

     新增方法：Object.is()、Object.assign()、Object.setPrototypeOf()、Object.getPrototypeOf()、Object.entries()、Object.keys()、Object.values()、for-in、Object.getOwnPropertyNames()、Object.getOwnPropertySymbols()、Reflect.ownKeys()

   * RegExp
   
     第一个参数是正则表达式，指定第二个参数不再报错、u修饰符、y修饰符、s修饰符
   
   * Number
   
     二进制和八进制新写法、新方法parseInt()、Number.EPSILON极小常量、安全整数、Math新方法
   
4. **新增symble类型**

   * 属性名是独一无二的，避免造成重命名导致的冲突

   * 注意点

     * 创建是调用函数，而不是new关键字

       > const a = Symble('a')

     * 遍历方法如上

5. **数据结构Set和Map**
   * 在set中，NaN只能存一个，所以是NaN等于NaN

6. **元编程相关Proxy和Reflect**

   * Proxy

     原理是改变this

     ```js
     var proxy = new Proxy(p1,p2); //p1是要被代理的目标对象，p2是配置对象。
     ```

   * Reflect

     和Proxy一一对应

7. **异步编程Promise、Generator和Async**

   三家对比：使用Promise的异步代码存在大量自有API的调用，操作本身的语义夹杂其中，不是很清晰；Generator函数实现的异步代码语义比Promise清晰，但需要一个执行器；async函数的写法最简洁、符合语义，不需要执行器。

8. **类、模块的支持**
   * class
   * export

9. **Iterator**

   for-of循环是一种遍历所有数据机构的统一方法。实现原理是数据结构上部署的Symbol.iterator属性





### 哪些对象可以被扩展运算符扩展

复杂数据类型都可以

基础数据只有string可以使用扩展运算符，number,boolean,null,undefined无效

注意只扩展一层





### ES6继承与ES5继承的区别

* **原型区别**

  > 下面讲的是B继承A,b是B的实例

  ES5中的继承如下,从原型上看，B的实例继承了A的原型

  但是A和B两个构造函数是相对独立的，没有继承关系，也就是说B获取不到A构造函数上面挂载的东西

  但是ES6是可以的，它直接B的隐式原型指向了A

  有什么好处呢:挂载在A(非实例)的方法可以通过B访问到，即子类继承了父类的属性

  ```js
  function A() {
    this.a = 'hello';
  }
  function B() {
    A.call(this);
    this.b = 'world';
  }
  B.prototype = Object.create(A.prototype, {
    constructor: { value: B, writable: true, configurable: true }
  });
  let b = new B();
  ```

  > 这个是实例的原型链

  <img src="https://uploadfiles.nowcoder.com/images/20220301/4107856_1646122217808/5EFC2E2CCA7CF0C0ED3AF97C57C347E8" alt="img" style="zoom: 50%;" />

​	

> 下面是ES5继承构造函数的原型链

![img](https://uploadfiles.nowcoder.com/images/20220301/4107856_1646122228075/C639481859D093429EF31DB41F59479D)

![img](https://uploadfiles.nowcoder.com/images/20220301/4107856_1646122234815/8F1CBB5E756E67FF00FA75B75E1198FD)

> 下图为ES6中继承时构造函数的改变

![img](https://uploadfiles.nowcoder.com/images/20220301/4107856_1646122317746/A439A948D436C4F8564F01CFC41DA1F6)

* **super与call的区别**
  * 在ES5中，继承使用call，也就是子类先构造一个对象，然后调用父亲的构造函数挂载对象，但是这样有一个问题，内置对象有的属性不是靠this挂载的，而是在创建对象实例的时候直接写入的，则子类实例获取不到这些属性，比如数组的length
  * 在ES6中，super一定要写在最前面。这样父类会产生一个实例对象，从而时super后面的this能够操作这个对象。所以其实ES6中的实例是父类生成的。所以可以访问到内置对象的内置属性。



### 暂时性死区

只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

* let 、const与暂时性死区，声明前获取或者设置会抛出ReferenceError





### 面向对象三个特征分别说一下是什么意思

* **封装**

  将对象运行时所需要的资源封装在程序对象中（基本上是方法和数据），对外只提供接口。

  > 隐藏实现细节，代码模块化

* **继承**

  当多个类存在相同的属性(变量)和方法时，可以从这些类中抽象出父类，在父类中定义这些相同的属性和方法

  > 代码重用，更接近人的思维

* **多态**

  多态指一个引用(类型)在不同情况下可以拥有多种状态

  多态是指通过指向父类的引用，来调用在不同子类中实现的方法

  > 相同事物相同方法但是行为不同





### 文件上传怎么实现

1. **普通的表单上传**

   > 这种方法容易超时

   ```html
   <form action="/index.php" method="POST" enctype="multipart/form-data">
     <input type="file" name="myfile">
     <input type="submit">
   </form>
   ```

2. **文件编码上传**

   * **base64**

     > 缺点是体积比原来的大

     ```js
     let imgURL = URL.createObjectURL(file);
     ctx.drawImage(imgURL,0,0);  // 生成canvas上下文
     var data = canvas.toDataURL("image/jpeg", 0.5);
     ```

   * **二进制上传**

     ```js
     // 读取二进制文件
     function readBinary(text){
         // 创建文件容器
         const data = new ArrayBuffer(text.length); // 缓冲区
         const ui8a = new Unit8Array(data,0);  // 8位无符号整型数组,体积小
         for(let i = 0;i<text.length;++i){
             ui8a[i] = (text.charCodeAt(i) & 0xff); // 只取最低8位
         }
     }
     
     const reader = new FileReader();
     reader.onload = function(){
         readBinary(this.result);
     }
     // 把从input里读取的文件内容，放到fileReader的result字段里
     reader.readAsBinaryString(file);
     ```



3. **formData异步上传**

   FormData对象主要用来组装一组用 XMLHttpRequest发送请求的键/值对，可以更加灵活地发送Ajax请求

   ```js
   const files = e.target.files // form的表单对象
   const formData = new FormData()
   formData.append("file",file)
   axios.post(url, formData);
   ```

4. **大文件上传**

   大文件上传最主要的问题就在于：**在同一个请求中，要上传大量的数据，导致整个过程会比较漫长，且失败后需要重头开始上传**

   如果某个请求失败，只需要重新发送这一次请求即可，无需从头开始，这样是否可以解决大文件上传的问题呢

   > 需要三个点：支持拆分上传请求(即切片)、支持断点续传、支持显示上传进度和暂停上传

   * **文件切片**

     编码方式上传中，在前端我们只要先获取文件的二进制内容，然后对其内容进行拆分，最后将每个切片上传到服务端即可

     在JavaScript中，文件FIle对象是Blob对象的子类，Blob对象包含一个重要的方法slice，通过这个方法，我们就可以对二进制文件进行拆分。

     ```js
     // 对文件进行拆分
     function slice(file,piece = 1024 * 1024 *5){
         let totalSize = file.size; 
         let start = 0;
         let end = start + piece;
         let chunks = []
         while(start < totalSize){
             if(start === end){
                 break;
             }
             // File对象继承自Blob对象，因此包含slice方法
             let blod = file.slice(start,end);
             chunks.push(blod)
             start = end
             end = start+piece <= totalSize ? start+piece : totalSize;
         }
         return chunks
     }
     
     // 上传侧
     let file = document.querySelector("[name=file]").files[0];
     const LENGTH = 1024 * 1024 * 0.1;
     let chunks = silce(file,LENGTH)
     let context = createContext(file); // 创建上下文区分文件
     chunks.forEach(chunk =>{
         let fd = new FormData();
         fd.append("file",chunk);
         fd.append("context",context); // 传递上下文
         fd.append("chunk",index+1); // 增加索引，识别在一个问价中的位置
         post('/mkblk.php', fd);
     })
     ```

   * **断点续传**

     将上传完成的切片标识(context,index)保存到localStorage

     然后上传的地方检查localStorage中有没有已经上传完成的记录，这样刷新浏览器之后上传完成的就不会再上传了

   * **上传进度**

     通过xhr.upload中的progress方法可以实现监控每一个切片上传进度







### 闭包

* **定义**
  * 闭包是指有权访问另一个函数作用域中变量的函数
  * 一个函数和对其周围状态的引用捆绑在一起， 这样的组合就是**闭包**

* **形成**

  创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量

  其实就是因为引用的变量没有被回收

* **闭包变量储存位置**

  闭包中的变量存储的位置是堆内存，而不是栈，因为栈是要释放的

* **特点**

  * 保护函数的私有变量不受外部的干扰,不污染全局变量

  * 保存，把一些函数内的值保存下来。

  * 会造成内存泄漏

* **应用**

  * **闭包可以实现方法和属性的私有化**

    > 就是将类的构造函数从一个函数里面返回

  * **闭包可以用来制作模块**

  * **模仿块级作用域**

  * **埋点计数器**



### CommonJS规范

* CommonJS规范加载模块是同步的，只有加载完成，才能执行后面的操作

* 每个文件就是一个模块，有自己的作用域。每个模块内部，module变量代表当前模块，是一个对象。

* module.exports属性表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取module.exports变量

* 为了方便，Node为每个模块提供一个exports变量，指向module.exports

  > 不能直接将exports变量指向一个值，因为这样等于切断了exports与module.exports的联系.只能通过exports修改module.exports的属性

  ```js
  let exports = module.exports;
  ```

* CommonJS模块导入用require，导出用module.exports

  > 导出的对象需注意，如果是静态值，而且非常量，后期可能会有所改动的，请使用函数动态获取，否则无法获取修改值。



###  ES6 module 和 CommonJS module 的区别

* 为**CommonJS**的require语法是同步的，所以就导致了**CommonJS**模块规范只适合用在服务端，而ES6模块无论是在浏览器端还是服务端都是可以使用的（因为他是异步的），但是在服务端中，还需要遵循一些特殊的规则才能使用；
* **CommonJS** 模块输出的是一个值的拷贝，而ES6模块输出的是值的引用；
* **CommonJS**有缓存，只会输出已经执行的部分，后续的输出或者变化，是不会影响已经输出的变量。而ES6模块相反，使用import加载一个变量，变量不会被缓存，真正取值的时候就能取到最终的值；
* **CommonJS** 模块是运行时加载，而ES6 模块是编译时输出接口，使得对JS的模块进行静态分析成为了可能
* 关于模块顶层的this指向问题，在**CommonJS**顶层，this指向当前模块；而在ES6模块中，this指向undefined；
* 关于两个模块互相引用的问题，在ES6模块当中，是支持加载**CommonJS**模块的。但是反过来，**CommonJS**并不能requireES6模块，在NodeJS中，两种模块方案是分开处理的。



###  ES6 module、CommonJS module 循环引用的问题

循环加载指的是a脚本的执行依赖b脚本，b脚本的执行依赖a脚本

* **CommonJS的循环加载**

  CommonJS模块是加载时执行，即脚本代码在require时就全部执行。一旦出现某个模块被“循环加载”，就只**输出已经执行的部分**，没有执行的部分不会输出。

  且是有缓存的，执行过一遍就不会再被执行，而是直接取之前缓存的exports对象

  > 如下：
  >
  > * a中调引用b，b执行。b执行时引用a时发现了循环依赖，则只取得a已经执行了的部分
  >
  > * 在main中引用b时，因为b已经再main引用a的时候执行过了，所以有缓存，直接取得缓存加过，所以b中不会再输出一次

  ```js
  //a.js
  exports.done = false;
  
  var b = require('./b.js');
  console.log('在a.js中，b.done = %j', b.done); // true
  
  exports.done = true;
  console.log('a.js执行完毕！')
  
  //b.js
  exports.done = false;
  
  var a = require('./a.js');
  console.log('在b.js中，a.done = %j', a.done); // false
  
  exports.done = true;
  console.log('b.js执行完毕！')
  
  //main.js
  var a = require('./a.js');
  var b = require('./b.js');
  
  console.log('在main.js中，a.done = %j, b.done = %j', a.done, b.done);// true true
  
  ```

* **ES6模块的循环加载**

  ES6模块与CommonJS有本质区别，ES6模块对导出变量，方法，对象是动态引用，遇到模块加载命令import时不会去执行模块，只是生成一个指向被加载模块的引用，需要开发者保证真正取值时能够取到值，只要引用是存在的，代码就能执行。

  > 下面代码是没问题的，因为import的时候并没有去执行，而是去解析(解析不等于执行)，所以它只要在odd.js中只要保证even.js中有解析到even即可，因为import了even

  但是真正执行起来还得看开发者到底怎么设计，所以循环引用是可能导致问题的，也就是值取不到的问题

  ```js
  //even.js
  import {odd} from './odd';
  
  var counter = 0;
  export function even(n){
      counter ++;
      console.log(counter);
  
      return n == 0 || odd(n-1);
  }
  
  
  //odd.**ES6模块的循环加载**
  import {even} from './even.js';
  
  export function odd(n){
      return n != 0 && even(n-1);
  }
  
  
  //index.js
  import * as m from './even.js';
  
  var x = m.even(5);
  console.log(x);
  
  var y = m.even(4);
  console.log(y);
  
  ```

  > 改用commonJS，就会报错,因为引用的时候执行了even.js，even.js又去执行了odd.js，但是此时even.js里面的even方法其实还没有完成挂载，所以报错

  ```js
  //even.js
  var odd = require('./odd.js');
  
  var counter = 0;
  module.exports = function even(n){
      counter ++;
      console.log(counter);
  
      return n == 0 || odd(n-1);
  }
  //odd.js
  var even = require('./even.js');
  
  module.exports = function odd(n){
      return n != 0 && even(n-1);
  }
  //index.js
  var even = require('./even.js');
  
  var x = even(5);
  console.log(x);
  
  var y = even(5);
  console.log(y);
  
  ```

  ```js
  $ babel-node index.js
  1
  /Users/name/Projects/node/ES6/odd.1.js:6
      return n != 0 && even(n - 1);
                       ^
  
  TypeError: even is not a function
      at odd (/Users/name/Projects/node/ES6/odd.1.js:4:22)
  
  ```

  





### 说一下Commonjs、AMD和CMD

**Commonjs(同步)**

* 一个单独的文件就是一个模块。每一个模块都是一个单独的作用域
* 输出模块变量的最好方法是使用`module.exports`对象。
* 加载模块使用`require`方法，该方法读取一个文件并执行，返回文件内部的`module.exports`对象
* 是有缓存的，会导出已执行的部分

**AMD(异步加载)**

* 解决的问题
  1. 多个文件有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
  2. 加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应的时间越长,所以需要异步

* 在定义的时候要指定依赖

* require（）函数在加载依赖函数的时候是异步加载的，这样浏览器不会失去响应，它指定回调函数，只有前面的模块加载成功，才会去执行

  ```js
  // 定义的时候要声明所有依赖
  define(['dependency'], function(){
  	var name = 'Byron';
  	function printName(){
  		console.log(name);
  	}
  	return {
  		printName: printName
  	};
  });
  
  // 使用的时候用回调函数使用
  require(['myModule'], function (my){
  	my.printName();
  }
  ```

**CMD**

* 在 CMD 规范中，一个模块就是一个文件

* CMD是按需加载依赖就近,只有在用到某个模块的时候再去require，不同于AMD

  ```js
  // CMD
  define(function(require, exports, module) {
    var a = require('./a')
    a.doSomething()
    // 此处略去 100 行
    var b = require('./b') // 依赖可以就近书写
    b.doSomething()
    // ... 
  })
  
  // AMD 默认推荐的是
  define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
    a.doSomething()
    // 此处略去 100 行
    b.doSomething()
    ...
  }) 
  ```

  





### 前端性能优化

前端性能优化手段从以下几个方面入手：**加载优化**、**执行优化**、**渲染优化**、**样式优化**、**脚本优化**

* **加载优化**

  | **减少HTTP请求**       | **合并CSS和JS、使用CSS精灵图**                 |
  | ---------------------- | ---------------------------------------------- |
  | **DNS预解析**          |                                                |
  | **缓存资源**           |                                                |
  | **压缩代码**           | 压缩代码(多余的缩进、空格和换行符)、启用Gzip   |
  | **按需加载**           | 懒加载、滚屏加载                               |
  | **预加载**             | 进入页面时Loading、提前加载下一页              |
  | **压缩图像**           |                                                |
  | **减少Cookie**         | Cookie会影响加载速度，静态资源域名不使用Cookie |
  | **避免重定向**         |                                                |
  | **异步加载第三方资源** |                                                |

* **执行优化**

  | CSS写在头部，JS写在尾部并异步  |                                                              |
  | ------------------------------ | ------------------------------------------------------------ |
  | **避免img、iframe等的src为空** | 空src会重新加载当前页面，影响速度和效率                      |
  | **尽量避免重置图像大小**       | 多次重置图像大小会引发图像的多次重绘，影响性能               |
  | **图像尽量避免使用DataURL**    | DataURL图像没有使用图像的压缩算法，文件会变大，并且要解码后再渲染，加载慢耗时长 |

* **渲染优化**

  | 设置viewport     | HTML的viewport可加速页面的渲染                               |
  | ---------------- | ------------------------------------------------------------ |
  | **减少DOM节点**  | DOM节点太多影响页面的渲染，尽量减少DOM节点                   |
  | **优化动画**     | 尽量使用CSS3动画、合理使用requestAnimationFrame动画代替setTimeout |
  | **优化高频事件** | 防抖、节流、使用requestAnimationFrame监听帧变化：使得在正确的时间进行渲染、增加响应变化的时间间隔 |
  | **GPU加速**      | 使用某些HTML5标签和CSS3属性会触发GPU渲染                     |

* **样式优化**

  | **避免在HTML中书写style** |                                                   |
  | ------------------------- | ------------------------------------------------- |
  | **避免CSS表达式**         | CSS表达式的执行需跳出CSS树的渲染                  |
  | **移除CSS空规则**         | CSS空规则增加了css文件的大小，影响CSS树的执行     |
  | **正确使用display**       |                                                   |
  | **不滥用float**           | float在渲染时计算量比较大，尽量减少使用           |
  | **不滥用Web字体**         | Web字体需要下载、解析、重绘当前页面，尽量减少使用 |
  | **不声明过多的font-size** | 过多的font-size影响CSS树的效率                    |
  | **值为0时不需要任何单位** | 为了浏览器的兼容性和性能，值为0时不要带单位       |
  |                           |                                                   |

* **脚本优化**

  | **减少重绘和回流**    |                                 |
  | --------------------- | ------------------------------- |
  | **缓存DOM选择与计算** |                                 |
  | **缓存.length的值**   | 每次.length计算用一个变量保存值 |
  | **尽量使用事件代理**  | 避免批量绑定事件                |
  | **尽量使用id选择器**  | id选择器选择元素是最快的        |

  



### BOM对象

* `BOM（Browser Object Model）`是指浏览器对象模型，可以对浏览器窗口进行访问和操作
* 使用 BOM，开发者可以**移动窗口、改变状态栏中的文本以及执行其他与页面内容不直接相关的动作**，使 `JavaScript` 有能力与浏览器"对话“

### DOM对象

* `DOM （Document Object Model）`是指文档对象模型，通过它，可以访问`HTML`文档的所有元素





### 说说前端中的事件流

事件流描述的是从页面中接收事件的顺序,DOM2级事件流包括下面几个阶段：

* 事件捕获阶段
* 处于目标阶段
* 事件冒泡阶段

addEventListener 是DOM2 级事件新增的指定事件处理程序的操作，这个方法接收3个参数

1. 要处理的事件名
2. 作为事件处理程序的函数
3. 一个布尔值
   1. 如果是true，表示在捕获阶段调用事件处理程序
   2. 如果是false，表示在冒泡阶段调用事件处理程序
   3. IE只支持事件冒泡



### 说一下事件冒泡

**事件冒泡**指在在一个对象上触发某类事件，如果此对象绑定了事件，就会触发事件，如果没有，就会向这个对象的父级对象传播，最终父级对象触发了事件



### 说一下事件委托

* **是什么**
  * 事件委托指的是，不在事件的发生地（直接dom）上设置监听函数，而是在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素DOM的类型(利用参数e)，来做出不同的响应。
* **好处**
  1. 比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触发机制。
  2. 减少内存消耗，节约效率





### 说一下图片的懒加载和预加载

* **预加载**

  提前加载图片，当用户需要查看时可直接从本地缓存中渲染

* **懒加载**

  懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。

  > 用户滚动到它们之前，可视区域外的图像不会加载

  > * 对服务器前端有一定的缓解压力作用，
  > * 提升用户体验（减少网页等待时间）
  > * 防止并发加载的资源过多会阻塞js的加载





### JS中各种位置

* **clientHeight**

  表示的是可视区域的高度，不包含border和滚动条

* **offsetHeight** -- 一般用这个

  表示可视区域的高度，包含了border和滚动条

* **scrollHeight**

  表示了所有区域的高度，包含了因为滚动被隐藏的部分。

* **clientTop**

  表示边框border的厚度，在未指定的情况下一般为

* **scrollTop**

  滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度



### 如何理解前端模块化

* 前端模块化就是复杂的文件编成一个一个独立的模块，比如js文件等等
* 分成独立的模块有利于重用（复用性）和维护（版本迭代）
* 这样会引来模块之间相互依赖的问题，所以有了commonJS规范，AMD，CMD规范等等，以及用于js打包（编译等处理）的工具webpack





### 如何监听对象属性的改变

* **ES5中用Object.defineProperty来实现已有属性的监听**

  ```js
  var person ={
      _age:10
  }
  
  Obj.defineProperty(person,'age',{
      get(){
          return this._age
      },
      set(newValue){
          if(value<10){
              return
          }
          this._age = newValue
      }
  })
  ```

* **在ES6中可以通过Proxy来实现**

  ```js
  // 创建proxy对象
  let proxy = new Proxy(person,{
      get(target,key){
           //target就是person，key就是访问的属性// 这里value省略了
           //注意，不能直接访问person 
      },
      set(target, key, newValue){
          
      }
  })
  ```





### ==和===、以及Object.is的区别

* ==

  等同，比较运算符，两边值类型不同的时候，先进行类型转换，再比较

  * `null == undefined`  

    > 虽然null和undefined不能转换成任何值，但是ES中规定这个相等

* **===**

  恒等，严格比较运算符，**不做类型转换**，类型不同就是不等

  * `NaN !== NaN`
  * `null !== undefile`
  * `+0 === -0`

* **Object.is**

  严格相等，与===基本一致，但是改了两个点

  * `NaN === NaN`
  * `+0 !== -0`



### setTimeout、setInterval和requestAnimationFrame之间的区别

* requestAnimationFrame不需要设置时间间隔
* 大多数电脑显示器的刷新频率是60Hz，大概相当于每秒钟重绘60次。大多数浏览器都会对重绘操作加以限制，不超过显示器的重绘频率，因为即使超过那个频率用户体验也不会有提升。因此，最平滑动画的最佳循环间隔是1000ms/60，约等于16.6ms
* setTimeout和setInterval的问题是，它们都不精确。
* RAF采用的是系统时间间隔，不会因为前面的任务影响RAF
* 特点
  * requestAnimationFrame会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率
  * 在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这当然就意味着更少的CPU、GPU和内存使用量
  * requestAnimationFrame是由浏览器专门为动画提供的API，在运行时浏览器会自动优化方法的调用，并且如果页面不是激活状态下的话，动画会自动暂停，有效节省了CPU开销。





### 什么是按需加载

* 当用户触发了动作时才加载对应的功能
* 触发的动作，是要看具体的业务场景而言，包括但不限于以下几个情况：鼠标点击、输入文字、拉动滚动条，鼠标移动、窗口大小更改等。加载的文件，可以是JS、图片、CSS、HTML等。





### js原型链是什么？原型链的顶端是什么？

* **原型链**

  * 在JS中一个构造函数默认带有一个prototype属性，这个的属性值是一个对象，即原型对象。同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数。
  * 同时每一个实例都会有一个\_\_proto\_\_属性指向这个prototype对象，我们可以把这个叫做隐式原型
  * 我们在使用一个实例的属性/方法的时候，会先检查这个实例中是否有这个属性/方法，没有的话就会其原型对象是否有这个属性/方法，如果其原型对象没有这个属性/方法,就会去这个原型对象的隐式原型上再找，这就是原型链。
  * 原型链顶端是Object.prototype

  ![HTpXOU.png](https://s4.ax1x.com/2022/02/18/HTpXOU.png)

  

  

  

### 0.1 + 0.2 === 0.3 嘛？为什么？

* `不相等`

* 两数相加的时候，会先转换成二进制，0.1和0.2在转换成二进制的时候**位数无限循环**，然后对阶运算，JS引擎堆二进制进行截断（因为使用的IEEE标准对尾数有限制），造成精度丢失

  ```js
  0.1 -> 0.0001100110011001...(无限循环)
  0.2 -> 0.0011001100110011...(无限循环)
  ```

* x = 0.1是0.1是因为对超过精度后截去，截去后，还是0.1

* 可以通过将数字转化成整数再运算，也可以借助第三方库



### JS 整数是怎么表示的？

通过 Number 类型来表示，遵循 IEEE754 标准，通过 64 位来表示一个数字，（1 + 11 + 52），最大安全数字是 Math.pow(2, 53) - 1，对于 16 位十进制。（符号位 + 指数位 + 小数部分有效位）。如果超过，会发生截断。

> 因为尾数有个默认的1，所以最大是2^53-1
>
> 那指数这么大，明明它还可以有很多个0在后面，为什么2^53-1就最大了？你想，如果是整数确实可以很大，但是如果要做运算呢，就不整数了，那么就会出问题了。所以最大要按能表示的全1来决定。



### symbol 有什么用处

* 表示一个独一无二的变量防止命名冲突
* 还可以利用 `symbol` 不会被常规的方法遍历，模拟私有变量
* 用来提供遍历接口，布置了 `symbol.iterator` 的对象才可以使用 `for···of` 循环，可以统一处理数据结构





### JS的变量提升

* js 引擎在代码执行前有一个解析的过程，创建了执行上下文，初始化了一些代码执行时需要用到的对象。

* 变量提升是指在 `JS` 代码执行过程中，`JS` 引擎把变量的声明部分和函数的声明部分提升到代码开头的行为。变量被提升后，会给变量设置默认值为 undefined

* 函数内部的变量声明会被提升至函数作用域的顶端

* JavaScript中具名的函数的声明形式有两种

  * **变量形式声明**

    和普通的变量提升的现象一样

    ```js
    fn()
    var fn = function () {
    	console.log(1)  
    }
    // 输出结果：Uncaught TypeError: fn is not a function
    ```

  * **函数式声明**

    函数声明式会将内容一起提升

    > 所以同时用函数式声名和变量式声名时，最后函数的值是变量式声名的值，因为被`重载`

    ```js
    foo()
    function foo () {
    	console.log(2)
    }
    // 输出结果：2
    ```

    

### 为什么要变量提升

* **提高性能**

  函数可以在执行时预先为变量分配栈空间

* **容错性更好**

  有时代码很复杂，可能因为疏忽而先使用后定义了，而由于变量提升的存在，代码会正常运行





### definePropoty有什么参数

`Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象

* **configurable**

  当且仅当该属性的 `configurable` 键值为 `true` 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除

* **enumerable**

  当且仅当该属性的 `enumerable` 键值为 `true` 时，该属性才会出现在对象的枚举属性中。默认为`false`

* **value**

* **writable**

  当且仅当该属性的 `writable` 键值为 `true` 时，属性的值，也就是上面的 `value`，才能被`赋值运算符`改变,**默认为 `false`**

* **get**

  属性的`getter`函数,当访问该属性时，会调用此函数

* **set**

  属性的`setter`函数，当属性值被修改时，会调用此函数.





### 大量的数据渲染，比如刷短视频这样的场景，该怎么优化

> 虚拟列表

* 后端对数据进行分页处理，前端每次请求并渲染少量数据 
* 维持整个数据列表的一个[最大数]()据上限，类似于一个滑动窗口 
* 当用户即将访问窗口底部的数据，请求后端服务加载新的数据并填充 
* 当整个窗口的数据量达到我们指定的渲染上限时，移除窗口头部的部分数据 
* 确保整个列表容器的总数据量不会太大 
* 在渲染数据时，必须确保每一条数据有唯一的标识作为key值，以提升列表渲染性能



### 如果一个对象原型链上层有一个`foo`属性，但是该对象没有`foo`属性，那么`myObj.foo="bar"`会发生什么

* 如果原型链上的`foo`访问属性没有标志位只读，那么就会再`myObj`上创建这个`foo`并屏蔽原型链上的
* 如果原型链上的`foo`访问属性标记为只读，那么无法修改已有`foo`，也无法创建屏蔽属性。在严格模式下还会报错
* 如果原型链上的`foo`是一个`setter`，那么会调用这个`setter`，并且不会创建屏蔽属性

### base64编码的原理和优缺点

* **是什么**

  Base64是网络上最常见的用于传输8Bit[字节码](https://so.csdn.net/so/search?q=字节码&spm=1001.2101.3001.7020)的编码方式之一，Base64就是一种基于64个可打印字符来标识二进制数据的方法。

* **用处**

  * Base64一般用于在HTTP协议下传输二进制数据，由于HTTP协议是文本协议，所以在HTTP写一下传输二进制数据需要将二进制数据转化为字符数据

    > 网络传输只能传输`可打印字符`
    >
    > 在ASCII码中规定，0-31、128这33个字符属于控制字符，32~127这95个字符属于可打印字符
    >
    > Base64就是其中一种传输不可打印字符的一种方式，注意并不是从0-63，因为0-31属于不可打印

  * 将图片等资源文件以Base64编码形式**直接放于代码中**，使用的时候反Base64后转换成Image对象使用，减少请求

  * 偶尔需要用`纯文本通道`传一张图片之类的情况发生的时候，就会用到Base64

* **原理**

  1. 对二进制数据进行处理，每3个字节一组，一共3x8=24bit

  2. 将这24bit划分为4组，每组正好6个bit

  3. 6bit的数据刚好可以表示0～63的范围,也就可以对应`base64表`的64个字符

  4. 通过上面4组数字进行索引，得到`base64表`中对应的字符

  5. 如果要传输的数据不是3的倍数，最后剩下1-2个字节，那么就会在多出的地方补0，然后在字符串后面添加`=`,而不是对`0`查询`base64表`，后面遇到等号的时候就会、会把等号对应的字节去掉

     > 那么前面多出来的自然也会去掉


* **优点**
  1. 可以将二进制数据转化为可打印字符，方便传输数据
  2. 对数据进行简单的加密，肉眼安全
  3. 将图片等内容放在代码中，减少http请求
* **缺点**
  1. 要消耗CPU进行编码
  2. 内容编码后体积变大，编码和解码需要额外工作量。



### 关于类

```js
class Animal {
    // constructor
    constructor() {
        this.name = 'cat'
        this.go = function(){}    // 实例方法
    }
    // Getter
    get name() {
        return this.name
    }
    
    //普通方法，则该方法是原型方法
    speak() {
        console.log(this.name)
    }
    // 静态方法-类方法
    static sleep() {}  //this指向类
    // 静态方法-箭头函数
    static sleep = ()=>{}  // 后面会变成类上普通方法，拥有this并且this指向类
    
    // 箭头函数，该方法会绑定在实例上
    eat = ()=>{}
}
```



### ++i和+=1区别

* i+=1是会进行类型转换后去相加
* i++是不会进行类型转换的，默认是Number类型操作，如果i不是Number，就会得到Nan

