### 说说对 React 的理解？有哪些特性？

* **是什么**
  
  * React，用于构建用户界面的 JavaScript 库，只提供了 UI 层面的解决方案
  * 遵循组件设计模式、声明式编程范式和函数式编程概念，以使前端应用程序更高效
  * 使用虚拟 `DOM` 来有效地操作 `DOM`，遵循从高阶组件到低阶组件的单向数据流
  * 帮助我们将界面成了各个独立的小块，每一个块就是组件，这些组件之间可以组合、嵌套，构成整体页面
  * `react` 类组件使用一个名为 `render()` 的方法或者函数组件`return`，接收输入的数据并返回需要展示的内容
  
* **特性**
  * JSX语法
  * 单向数据绑定
  * 虚拟 DOM
  * 声明式编程zhonfdian
  * Component

* **声明式编程**

  * 声明式编程是一种编程范式，它关注的是你要做什么，而不是如何做

    > 怎么做是内部的事情

  * 它表达逻辑而不显式地定义步骤。这意味着我们需要根据逻辑的计算来声明要显示的组件

  * 例子

    * 我们要实现一个标记的地图,通过命令式创建地图、创建标记、以及在地图上添加的标记的步骤如下：

      ```ts
      // 创建地图
      const map = new Map.map(document.getElementById("map"), {
        zoom: 4,
        center: { lat, lng },
      });
      
      // 创建标记
      const marker = new Map.marker({
        position: { lat, lng },
        title: "Hello Marker",
      });
      
      // 地图上添加标记
      marker.setMap(map);
      ```

    * 而用 `React` 实现上述功能则如下

      ```jsx
      <Map zoom={4} center={(lat, lng)}>
        <Marker position={(lat, lng)} title={"Hello Marker"} />
      </Map>
      ```

  * 声明式编程方式使得 `React` 组件很容易使用，最终的代码简单易于维护

* **Component**

  * 在 `React` 中，一切皆为组件。通常将应用程序的整个逻辑分解为小的单个部分。 我们将每个单独的部分称为组件
  * 组件可以是一个函数或者是一个类，接受数据输入，处理它并返回在 `UI` 中呈现的 `React` 元素

  * 一个组件该有的特点如下：
    * 可组合：每个组件易于和其它组件一起使用，或者嵌套在另一个组件内部
    * 可重用：每个组件都是具有独立功能的，它可以被使用在多个 UI 场景
    * 可维护：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护

* **优势**
  - 高效灵活
  - 声明式的设计，简单使用
  - 组件式开发，提高代码复用率
  - 单向响应的数据流会比双向绑定的更安全，速度更快







### 说说 Real DOM 和 Virtual DOM 的区别？优缺点？

* **是什么**
  * Real DOM，真实 `DOM`，意思为文档对象模型，是一个结构化文本的抽象，在页面渲染出的每一个结点都是一个真实 `DOM` 结构
  * `Virtual Dom`，本质上是以 `JavaScript` 对象形式存在的对 `DOM` 的描述
  * 创建虚拟 `DOM` 目的就是为了更好将虚拟的节点渲染到页面视图中，虚拟 `DOM` 对象的节点与真实 `DOM` 的属性一一照应

* **怎么做**

  * 在 `React` 中，`JSX` 是其一大特性，可以让你在 `JS` 中通过使用 `XML` 的方式去直接声明界面的 `DOM` 结构

    > `ReactDOM.render()` 用于将你创建好的虚拟 `DOM` 节点插入到某个真实节点上，并渲染到页面上

    ```ts
    // 创建 h1 标签，右边千万不能加引号
    const vDom = <h1>Hello World</h1>; 
    // 找到 <div id="root"></div> 节点
    const root = document.getElementById("root"); 
    // 把创建的 h1 标签渲染到 root 节点上
    ReactDOM.render(vDom, root); 
    ```

  * `JSX` 实际是一种语法糖，在使用过程中会被 `babel` 进行编译转化成 `JS` 代码，上述 `VDOM` 转化为如下：

    ```ts
    const vDom = React.createElement(
      'h1'，
      { className: 'hClass', id: 'hId' },
      'hello world'
    )
    ```

  * 可以看到，`JSX` 就是为了简化直接调用 `React.createElement()` 方法

  

* **区别**

  * 操作虚拟 DOM 不会进行排版与重绘操作，而真实 DOM 会频繁重排与重绘
  * 虚拟 DOM 的总损耗是“虚拟 DOM 增删改+真实 DOM 差异增删改+排版与重绘”，真实 DOM 的总损耗是“真实 DOM 完全增删改+排版与重绘”

  * 例子

    > 传统的原生 `api` 或 `jQuery` 去操作 `DOM` 时，浏览器会从构建 `DOM` 树开始从头到尾执行一遍流程
    >
    > 当你在一次操作时，需要更新 10 个 `DOM` 节点，浏览器没这么智能，收到第一个更新 `DOM` 请求后，并不知道后续还有 9 次更新操作，因此会马上执行流程，最终执行 10 次流程
    >
    > 而通过 `VNode`，同样更新 10 个 `DOM` 节点，虚拟 `DOM` 不会立即操作 `DOM`，而是将这 10 次更新的 `diff` 内容保存到本地的一个 `js` 对象中，最终将这个 `js` 对象一次性 `pattach` 到 `DOM` 树上，避免大量的无谓计算，至于怎么pacth那要看patch的内容了

* **优缺点**

  * **真实DOM**
    * 优点
      1. 易用
    * 缺点
      1. 效率低，解析速度慢，内存占用量过高
      2. 性能差：频繁操作真实 DOM，易于导致重绘与回流

  * 虚拟DOM

    * 优点
      1. 简单方便：如果使用手动操作真实 `DOM` 来完成页面，繁琐又容易出错，在大规模应用下维护起来也很困难
      2. 性能方面：使用 Virtual DOM，能够有效避免真实 DOM 数频繁更新，减少多次引起重绘与回流，提高性能
      3. 跨平台：React 借助虚拟 DOM，带来了跨平台的能力，一套代码多端运行

    * **去缺点**
      - 在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化
      - 首次渲染大量 DOM 时，由于多了一层虚拟 DOM 的计算，速度比正常稍慢







### 说说 React 生命周期有哪些不同阶段？每个阶段对应的方法是？

* **是什么**

  `React`整个组件生命周期包括从创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程

* **流程**

  这里主要讲述`react16.4`之后的生命周期，可以分成三个阶段

  - 创建阶段
  - 更新阶段
  - 卸载阶段

* **创建阶段**

  创建阶段主要分成了以下几个生命周期方法：

  * **constructor**

    实例过程中自动调用的方法，在方法内部通过`super`关键字获取来自父组件的`props`

    在该方法中，通常的操作为初始化`state`状态或者在`this`上挂载方法

  * **getDerivedStateFromProps**

    该方法是新增的生命周期方法，是一个静态的方法，因此不能访问到组件的实例

    执行时机：组件创建和更新阶段，不论是`props`变化还是`state`变化，也会调用

    在每次`render`方法前调用，第一个参数为即将更新的`props`，第二个参数为上一个状态的`state`，可以比较`props` 和 `state`来加一些限制条件，防止无用的state更新

    该方法需要返回一个新的对象作为新的`state`或者返回`null`表示`state`状态不需要更新

  * **render**

    组件必须实现的方法，用于渲染`DOM`结构，可以访问组件`state`与`prop`属性

  * **componentDidMount**

    组件挂载到真实`DOM`节点后执行，其在`render`方法之后执行

*  **更新阶段**

  * **getDerivedStateFromProps**

  * **shouldComponentUpdate**

    用于告知组件本身基于当前的`props`和`state`是否需要重新渲染组件，默认情况返回`true`

    执行时机：遇到新的props或者state时都会调用，通过返回true或者false告知组件更新与否

    一般情况，不建议在该周期方法中进行深层比较，会影响效率同时也不能调用`setState`，否则会导致无限循环调用更新

  * **render**

  * **getSnapshotBeforeUpdate**

    该周期函数在`render`后执行，执行之时`DOM`元素还没有被更新

    该方法返回的一个`Snapshot`值，作为`componentDidUpdate`第三个参数传入

    目的在于获取组件更新前的一些信息，比如组件的滚动位置之类的，在组件更新后可以根据这些信息恢复一些UI视觉上的状态

    ```ts
    getSnapshotBeforeUpdate(prevProps, prevState) {
        console.log('#enter getSnapshotBeforeUpdate');
        return 'foo';
    }
    
    componentDidUpdate(prevProps, prevState, snapshot) {
        console.log('#enter componentDidUpdate snapshot = ', snapshot);
    }
    ```

  * **componentDidUpdate**

    组件更新结束后触发，可以根据前后的`props`和`state`的变化做相应的操作，如获取数据，修改`DOM`样式等

* **卸载阶段**

  * **componentWillUnmount**

    此方法用于组件卸载前，清理一些注册是监听事件，或者取消订阅的网络请求等

    一旦一个组件实例被卸载，其不会被再次挂载，而只可能是被重新创建

  





### state 和 props 有什么区别？

* **state**

  一个组件的显示形态可以由数据状态和外部参数所决定，而数据状态就是 `state`，一般在 `constructor` 中初始化

  当需要修改里面的值的状态需要通过调用 `setState` 来改变，从而达到更新组件内部数据的作用，并且重新调用组件 `render` 方法

  `setState` 还可以接受第二个参数，它是一个函数，会在 `setState` 调用完成并且组件开始重新渲染时被调用，可以用来监听渲染是否完成

  ```ts
  class Button extends React.Component {
    constructor() {
      super();
      this.state = {
        count: 0,
      };
    }
  
    updateCount() {
      this.setState((prevState, props) => {
        return { count: prevState.count + 1 };
      });
    }
  
    render() {
      return (
        <button onClick={() => this.updateCount()}>
          Clicked {this.state.count} times
        </button>
      );
    }
  }
  ```

* **props**

  `React` 的核心思想就是组件化思想，页面会被切分成一些独立的、可复用的组件组件

  从概念上看就是一个函数，可以接受一个参数作为输入值，这个参数就是 `props`，所以可以把 `props` 理解为从外部传入组件内部的数据

  `react` 具有单向数据流的特性，所以他的主要作用是从父组件向子组件中传递数据

  ```ts
  class Welcome extends React.Component {
    render() {
      return <h1>Hello {this.props.name}</h1>;
    }
  }
  
  const element = <Welcome name="Sara" onNameChanged={this.handleName} />;
  ```

* **相同**
  - 两者都是 JavaScript 对象
  - 两者都是用于保存信息
  - props 和 state 都能触发渲染更新

* **区别**
  - props 是外部传递给组件的，而 state 是在组件内被组件自己管理的，一般在 constructor 中初始化
  - props 在组件内部是不可修改的，但 state 在组件内部可以进行修改



### super和super(props)的区别

* **ES6类**

  在类中，子类得到的不是子类的实例，而是父类构造的实例，再将this给子类加工，`super()` 就是将父类中的 `this` 对象继承给子类的，没有 `super()` 子类就得不到实例对象

* **类组件**

  * 在 `React` 中，类组件是基于 `ES6` 的规范实现的，继承 `React.Component`，因此如果用到 `constructor` 就必须写 `super()` 才初始化 `this`

  * 这时候，在调用 `super()` 的时候，我们一般都需要传入 `props` 作为参数，如果不传进去，`React` 内部也会将其定义在组件实例中

    ```ts
    // React 内部
    const instance = new YourComponent(props); // 想接收一个props
    instance.props = props; // 你不传我react也会找到它
    ```

  * 也不建议使用 `super()` 代替 `super(props)`，因为`React` 会在类组件构造函数生成实例后再给 `this.props` 赋值,所以不传在构造函数里面用this就访问不到

    ```ts
    lass Button extends React.Component {
      constructor(props) {
        super(); // 没传入 props
        console.log(props);      //  {a:1} 
        console.log(this.props); //  undefined
        // ...
      }
    }
    ```

    

  

### 说说 React中的setState执行机制

* **是什么**

  个组件的显示形态可以由数据状态和外部参数所决定，而数据状态就是`state`

  需要修改里面的值的状态需要通过调用`setState`来改变，从而达到更新组件内部数据的作用

  ```ts
  constructor(props) {
      super(props);
  
      this.state = {
          message: "Hello World"
      }
  }
  
  changeText() {
      this.setState({
          message: "JS每日一题"
      })
  }
  ```

* **特点**

  `React`并不像`vue2`中调用`Object.defineProperty`数据响应式或者`Vue3`调用`Proxy`监听数据的变化，所以直接改变state是不会触发界面更新的

  必须通过`setState`方法来告知`react`组件`state`已经发生了改变

  `setState`第一个参数可以是一个对象，或者是一个函数，而第二个参数是一个回调函数，用于可以实时的获取到更新之后的数据

* **异步更新**

  在组件生命周期或React合成事件中，不能在后面获取到更新后的值，但是可以通过回调函数

  ```TS
  <button onClick={e => this.changeText()}>面试官系列</button>
  changeText() {
    this.setState({
      message: "你好啊"
    }, () => {
      console.log(this.state.message); // 你好啊
    });
    console.log(this.state.message); // hello
  }
  ```

* **同步更新**

  在setTimeout或者原生dom事件中

  ```ts
  changeText() {
    setTimeout(() => {
      this.setState({
        message: "你好啊
      });
      console.log(this.state.message); // 你好啊
    }, 0);
  }
  ```

* **批量更新**

  对同一个值进行多次 `setState`， `setState` 的批量更新策略会对其进行覆盖，取最后一次的执行结果

  > 但在`setTimeout`或者原生`dom`事件中，由于是同步的操作，所以并不会进行覆盖现象





### 说说React的事件机制？

* **是什么**

  `React`基于浏览器的事件机制自身实现了一套事件机制，包括事件注册、事件的合成、事件冒泡、事件派发等

  在`React`中这套事件机制被称之为合成事件

  * **合成事件**

    合成事件是 `React`模拟原生`DOM`事件所有能力的一个事件对象，即浏览器原生事件的跨浏览器包装器

    根据 `W3C`规范来定义合成事件，兼容所有浏览器，拥有与浏览器原生事件相同的接口

    ```ts
    const button = <button onClick={handleClick}>按钮</button>
    ```

    如果想要获得原生`DOM`事件，可以通过`e.nativeEvent`属性获取

    ```ts
    const handleClick = (e) => console.log(e.nativeEvent);
    ```

    与原生事件的区别：

    * **事件名称命名方式不同**:`onclick` `onClick`

    * **事件处理函数书写不同**

      ```ts
      // React 合成事件 事件处理函数写法
      const button = <button onClick={handleClick}>按钮命名</button>
      
      // 原生事件 事件处理函数写法
      <button onclick="handleClick()">按钮命名</button>
      ```

    * **绑定上**

      虽然`onclick`看似绑定到`DOM`元素上，但实际并不会把事件代理函数直接绑定到真实的节点上，而是把所有的事件绑定到结构的最外层，使用一个统一的事件去监听

      这个事件监听器上维持了一个映射来保存所有组件内部的事件监听和处理函数。当组件挂载或卸载时，只是在这个统一的事件监听器上插入或删除一些对象

      当事件发生时，首先被这个统一的事件监听器处理，然后在映射里找到真正的事件处理函数并调用。这样做简化了事件处理和回收机制，效率也有很大提升

* **执行顺序**
  * React 所有事件都挂载在 document 对象上
  * 当真实 DOM 元素触发事件，会冒泡到 document 对象后，再处理 React 事件
  * 所以会先执行原生事件，然后处理 React 事件
  * 最后真正执行 document 上挂载的事件

* **总结**
  * React 上注册的事件最终会绑定在document这个 DOM 上，而不是 React 组件对应的 DOM(减少内存开销就是因为所有的事件都绑定在 document 上，其他节点没有绑定事件)
  * React 自身实现了一套事件冒泡机制，所以这也就是为什么我们 event.stopPropagation()无效的原因。
  * React 通过队列的形式，从触发的组件向父组件回溯，然后调用他们 JSX 中定义的 callback



### React事件绑定的方式有哪些？区别？

* **是什么**

  在`react`应用中，事件名都是用小驼峰格式进行书写，例如`onclick`要改写成`onClick`，事件绑定的方法需要使用`{}`包住

  ```ts
   <button onClick={this.showAlert}>show</button>;
  ```

  但是下面点击时会输出undefine

  ```ts
   <button onClick={console.log(this)}>show</button>;
  ```

* **如何绑定**

  为了解决上面正确输出`this`的问题，常见的绑定方式有如下：

  * **render方法中使用bind**

    如果使用一个类组件，在其中给某个组件/元素一个`onClick`属性，它不会自动绑定其`this`到当前组件，可用bind

    > 回调函数中的this会变

    ```ts
    class App extends React.Component {
      handleClick() {
        console.log('this > ', this);
      }
      render() {
        return (
          <div onClick={this.handleClick.bind(this)}>test</div>
        )
      }
    }
    ```

  * **render方法中使用箭头函数**

    通过`ES6`的上下文来将`this`的指向绑定给当前组件，但是每一次`render`的时候都会生成新的方法，影响性能

    > 箭头函数this刚开始就定死了

    ```ts
    class App extends React.Component {
      handleClick() {
        console.log('this > ', this);
      }
      render() {
        return ( 
          <div onClick={e => this.handleClick(e)}>test</div>
        )
      }
    }
    ```

  * **constructor中bind**

    在`constructor`中预先`bind`当前组件，可以避免在`render`操作中重复绑定

    ```ts
    constructor(props) {
        super(props);
        this.handleClick = this.handleClick.bind(this);
    }
    ```

  * **定义阶段使用箭头函数绑定**

    定义的时候就定死this，最优

    ```ts
      handleClick = () => {
        console.log('this > ', this);
      }
    ```

    

  

  

### React构建组件的方式有哪些？区别？

* **是什么**

  组件就是把图形、非图形的各种逻辑均抽象为一个统一的概念（组件）来实现开发的模式

  在`React`中，一个类、一个函数都可以视为一个组件

* **如何构建**

  在`React`目前来讲，组件的创建主要分成了三种方式：

  - 函数式创建
  - 通过 React.createClass 方法创建
  - 继承 React.Component 创建

* **函数式创建**

  在`React Hooks`出来之前，函数式组件可以视为无状态组件，只负责根据传入的`props`来展示视图，不涉及对`state`状态的操作

  大多数组件可以写为无状态组件，通过简单组合构建其他组件

  ```ts
  function HelloComponent(props, /* context */) {
    return <div>Hello {props.name}</div>
  }
  ```

* **通过 React.createClass 方法创建**

  `React.createClass`是react刚开始推荐的创建组件的方式，目前这种创建方式已经不怎么用了

  像上述通过函数式创建的组件的方式，最终会通过`babel`转化成`React.createClass`这种形式，

  ```ts
  function HelloComponent(props) /* context */{
    return React.createElement(
      "div",
      null,
      "Hello ",
      props.name
    );
  }
  ```

* **继承 React.Component 创建**

  同样在`react hooks`出来之前，有状态的组件只能通过继承`React.Component`这种形式进行创建

  有状态的组件也就是组件内部存在维护的数据，在类创建的方式中通过`this.state`进行访问

  当调用`this.setState`修改组件的状态时，组价会再次会调用`render()`方法进行重新渲染

* **区别**
  * 对于一些无状态的组件创建，建议使用函数式创建的方式
  * 由于`react hooks`的出现，函数式组件创建的组件通过使用`hooks`方法也能使之成为有状态组件，再加上目前推崇函数式编程，所以这里建议都使用函数式的方式来创建组件



### React中组件之间如何通信？

* **是什么**

  组件间通信可以拆分为两个词：

  - 组件
  - 通信

  相比`vue`，`React`的组件更加灵活和多样，按照不同的方式可以分成很多类型的组件

  组件间通信即指组件通过某种方式来传递信息以达到某个目的	

* **如何通信**

  组件传递的方式有很多种，根据传送者和接收者可以分为如下：

  - 父组件向子组件传递
  - 子组件向父组件传递
  - 兄弟组件之间的通信
  - 父组件向后代组件传递
  - 非关系组件传递

* **父组件向子组件传递**

  由于`React`的数据流动为单向的，父组件向子组件传递是最常见的方式,一般用props传递

* **子组件向父组件传递**

  子组件向父组件通信的基本思路是，父组件向子组件传一个函数，然后通过这个函数的回调，拿到子组件传过来的值

* **兄弟组件之间的通信**

  如果是兄弟组件之间的传递，则父组件作为中间层来实现数据的互通，通过使用父组件传递

* **父组件向后代组件传递**

  使用`context`提供了组件之间通讯的一种方式，可以共享数据，其他数据都能读取对应的数据

  通过使用`React.createContext`创建一个`context`

  ```ts
  const PriceContext = React.createContext('price')
  ```

  `context`创建成功后，其下存在`Provider`组件用于创建数据源，`Consumer`组件用于接收数据，使用实例如下

  ```ts
  <PriceContext.Provider value={100}>
  </PriceContext.Provider>
  ```

  如果想要获取`Provider`传递的数据，可以通过`Consumer`组件或者或者使用`contextType`属性接收，对应分别如下：

  ```ts
  class MyClass extends React.Component {
    static contextType = PriceContext;
    render() {
      let price = this.context;
      /* 基于这个值进行渲染工作 */
    }
  }
  ```

  ```tsx
  <PriceContext.Consumer>
      { /*这里是一个函数*/ }
      {
         price => <div>price：{price}</div>
      }
  </PriceContext.Consumer>
  ```

* **非关系组件传递**

  建议将数据进行一个全局资源管理，从而实现通信，例如`redux`



* **总结**

  由于`React`是单向数据流，主要思想是组件不会改变接收的数据，只会监听数据的变化，当数据发生变化时它们会使用接收到的新值，而不是去修改已有的值

  因此，可以看到通信过程中，数据的存储位置都是存放在上级位置中





### React中的key有什么作用？

* **是什么**

  react中渲染列表的每一个子元素都应该需要一个唯一的`key`值，否则会警告

* **作用**

  跟`Vue`一样，`React` 也存在 `Diff`算法，而元素`key`属性的作用是用于判断元素是新创建的还是被移动的元素，从而减少不必要的元素渲染

  因此`key`的值需要为每一个元素赋予一个确定的标识

* **场景**

  1. **列表数据渲染中，在数据后面插入一条数据**

  此时`key`作用并不大，前面的元素在`diff`算法中，前面的元素由于是完全相同的，并不会产生删除创建操作,在最后一个比较的时候，则需要插入到新的`DOM`树中

  2. **列表数据渲染中，在数据前面插入一条数据**

     * 有key

       `react`根据`key`属性匹配原有树上的子元素以及最新树上的子元素，只需要将000元素插入到最前面位置

     * 无key

       所有子元素重新渲染，因为比较的时候没比较到相同的了，后面diff会讲

* **注意**

  不是写key性能就高，比如如果每次渲染只是文本变了，那么就算是每个都更改也只是更改以下文本，非常简单，节点不会变

  > 检测到不同之后会根据具体去更新，只是文本变了就不用更新节点

  但是使用key，发现旧的节点不在了还需要删除新增节点，但其实直接改文本会更方便

* **总结**
  * key 应该是唯一的
  * key不要使用随机值（随机数在下一次 render 时，会重新生成一个数字，则和之前完全不同，就没什么意义了，每次都会导致所有更新的）
  * 使用 index 作为 key值，对性能没有优化(增或删除，位置一变，全部重搞)

![img](https://static.vue-js.com/3b9afe10-dd69-11eb-ab90-d9ae814b240d.png)





### 说说对React refs 的理解？应用场景？

* **是什么**

  `React` 中的 `Refs`提供了一种方式，允许我们访问`DOM`节点或在 `render`方法中创建的 `React`元素

* **使用**

  创建`ref`的形式有四种：

  * 传入字符串
  * 传入对象
  * 传入函数
  * 传入hook

* **传入字符串(不推荐)**

  ```ts
  class MyComponent extends React.Component {
    handleClick = ()=>{console.log(this.refs.myref)}
    render() {
      return <><div ref="myref"/><button onclick = {handleClick}>点我</button></>
    }
  }
  ```

* **传入对象**

  `refs`通过`React.createRef()`创建，然后将`ref`属性添加到`React`元素中，如下：

  ```ts
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.myRef = React.createRef();
    }
    handleClick = ()=>{
        console.log(this.myRef.current)
    }
    
    render() {
      return <div ref={this.myRef} />;
    }
  }
  ```

* **传入函数**

  当`ref`传入为一个函数的时候，在渲染过程中，回调函数参数会传入一个元素对象，然后通过实例将对象进行保存

  ```ts
  class MyComponent extends React.Component {
    // 直接访问 
    handleClick = ()=>{
       console.log(this.myRef)
    }
    render() {
      return <div ref={element => this.myref = element} />;
    }
  }
  ```

* **传入hook**

  > 推荐

  通过`useRef`创建一个`ref`，整体使用方式与`React.createRef`一致

  ```ts
  function App(props) {
    const myref = useRef()
    return (
      <>
        <div ref={myref}></div>
      </>
    )
  }
  ```

* **注意**

  上述三种情况都是`ref`属性用于原生`HTML`元素上，如果`ref`设置的组件为一个类组件的时候，`ref`对象接收到的是组件的挂载实例，所以不能在函数组件上使用`ref`属性，因为他们并没有实例

  

* **应用场景**
  * 对Dom元素的焦点控制、内容选择、控制
  * 对Dom元素的内容设置及媒体播放
  * 对Dom元素的操作和对组件实例的操作
  * 集成第三方 DOM 库







### 说说对React中类组件和函数组件的理解？有什么区别？

* **类组件**

  * 使用`ES6`类的编写形式去编写组件，该类必须继承`React.Component`

  * 如果想要访问父组件传递过来的参数，可通过`this.props`的方式去访问
  * 在组件中必须实现`render`方法，在`return`中返回`React`对象

* **函数组件**

  * 通过函数编写的形式去实现一个`React`组件，是`React`中定义组件最简单的方式
  * 函数第一个参数为`props`用于接收父组件传递过来的参数

* **区别**

  两种组件主要区别

  - 编写形式
  - 状态管理
  - `生命周期`
  - `调用方式`

* **编写形式**

  一个用类，一个用函数

* **状态管理**

  函数用useState管理状态，而类本身有setState

* **生命周期**

  在函数组件中，并不存在生命周期，这是因为这些生命周期钩子都来自于继承的`React.Component`

  但是函数组件使用`useEffect`等也能够完成`替代`生命周期的作用

* **调用方式**

  如果是一个函数组件，调用则是执行函数即可

  ```ts
  // 你的代码 
  function SayHi() { 
      return <p>Hello, React</p > 
  } 
  // React内部 
  const result = SayHi(props) // » <p>Hello, React</p >
  ```

  如果是一个类组件，则需要将组件进行实例化，然后调用实例对象的`render`方法

  ```ts
  // 你的代码 
  class SayHi extends React.Component { 
      render() { 
          return <p>Hello, React</p > 
      } 
  } 
  // React内部 
  const instance = new SayHi(props) // » SayHi {} 
  const result = instance.render() // » <p>Hello, React</p >
  ```

* **总结**

  各有优缺点，函数组件语法短，简单，更容易开发、理解和测试，并且不会大量使用this使人疑惑







### 说说对受控组件和非受控组件的理解？应用场景

* **受控组件**

  受控组件，简单来讲，就是受我们控制的组件，组件的状态全程响应外部数据

  > 受控组件我们一般需要初始状态和一个状态更新事件函数

  ```ts
  class TestComponent extends React.Component {
    constructor (props) {
      super(props);
      this.state = { username: 'lindaidai' };
    }
    render () {
      // 这里value完全由我们控制 
      return <input name="username" value={this.state.username} onChange={....}/>
    }
  }
  ```

* **非受控组件**

  非受控组件，简单来讲，就是不受我们控制的组件。一般情况是在初始化的时候接受外部数据，然后自己在内部存储其自身状态

  当需要时，可以使用`ref` 查询 `DOM`并查找其当前值

  ```ts
  export class UnControll extends Component {
    constructor (props) {
      super(props);
      this.inputRef = React.createRef();
    }
    handleSubmit = (e) => {
      console.log('我们可以获得input内的值为', this.inputRef.current.value);
      e.preventDefault();
    }
    render () {
      return (
        <form onSubmit={e => this.handleSubmit(e)}>
          // 初始化的时候受我们控制
          <input defaultValue="lindaidai" ref={this.inputRef} />
          <input type="submit" value="提交" />
        </form>
      )
    }
  }
  ```

* **应用场景**

  大部分时候推荐使用受控组件来实现表单，因为在受控组件中，表单数据由`React`组件负责处

  如果选择非受控组件的话，控制能力较弱，表单数据就由`DOM`本身处理，但更加方便快捷，代码量少

  举一些一定要受控的例子

  > * 有条件的禁用提交按钮
  > * 强制输入格式
  > * 动态输入





### 说说对高阶组件的理解，应用场景

* **是什么**

  高阶函数（Higher-order function），至少满足下列一个条件的函数

  - 接受一个或多个函数作为输入
  - 输出一个函数

  在`React`中，高阶组件即接受一个或多个组件作为参数并且返回一个组件，本质也就是一个函数，并不是一个组件

  ```ts
  const EnhancedComponent = highOrderComponent(WrappedComponent);
  ```

  高阶组件的这种实现方式，本质上是一个装饰者设计模式

* **有什么用**

  通过对传入的原始组件 `WrappedComponent` 做一些你想要的操作（比如操作 props，提取 state，给原始组件包裹其他元素等），从而加工出想要的组件 `EnhancedComponent`

  把通用的逻辑放在高阶组件中，对组件实现一致的处理，从而实现代码的复用

  所以，高阶组件的主要功能是封装并分离组件的通用逻辑，让通用逻辑在组件间更好地被复用

* **约定**

  但在使用高阶组件的同时，一般遵循一些约定

  * props 保持一致

    > 传入封装后组件的props和原本应该传入被封装组件的保持一致

  * 你不能在函数式（无状态）组件上使用 ref 属性，因为它没有实例

  * 不要以任何方式改变原始组件 WrappedComponent

  * 透传不相关 props 属性给被包裹的组件 WrappedComponent

    > 也就是这些都要透下去

  * 不要在 render() 方法中使用高阶组件
  * 使用 compose 组合高阶组件

* **注意**

  高阶组件可以传递所有的`props`，但是不能传递`ref`，如果需要传递`refs`的话，则用`React.forwardRef`

  ```ts
  function withLogging(WrappedComponent) {
      class Enhance extends WrappedComponent {
          componentWillReceiveProps() {
              console.log('Current props', this.props);
              console.log('Next props', nextProps);
          }
          render() {
              const {forwardedRef, ...rest} = this.props;
              // 把 forwardedRef 赋值给 ref
              return <WrappedComponent {...rest} ref={forwardedRef} />;
          }
      };
  
      // React.forwardRef 方法会传入 props 和 ref 两个参数给其回调函数
      // 所以这边的 ref 是由 React.forwardRef 提供的
      function forwardRef(props, ref) {
          return <Enhance {...props} forwardRef={ref} />
      }
  
      return React.forwardRef(forwardRef);
  }
  const EnhancedComponent = withLogging(SomeComponent);
  ```

* **应用场景**

  通过上面的了解，高阶组件能够提高代码的复用性和灵活性，在实际应用中，常常用于与核心业务无关但又在多个模块使用的功能，如权限控制、日志记录、数据校验、异常处理、统计上报等

  举个例子，存在一个组件，需要从缓存中获取数据，然后渲染。一般情况，我们会如下编写

  ```ts
  import React, { Component } from 'react'
  
  class MyComponent extends Component {
  
    componentWillMount() {
        let data = localStorage.getItem('data');
        this.setState({data});
    }
    
    render() {
      return <div>{this.state.data}</div>
    }
  }
  ```

  但是如果还有其他组件也有类似功能的时候，每个组件都需要重复写`componentWillMount`中的代码

  下面就可以通过高价组件来进行改写

  ```ts
  import React, { Component } from 'react'
  
  function withPersistentData(WrappedComponent) {
    return class extends Component {
      componentWillMount() {
        let data = localStorage.getItem('data');
          this.setState({data});
      }
      
      render() {
        // 通过{...this.props} 把传递给当前组件的属性继续传递给被包装的组件WrappedComponent
        return <WrappedComponent data={this.state.data} {...this.props} />
      }
    }
  }
  
  class MyComponent2 extends Component {  
    render() {
      return <div>{this.props.data}</div>
    }
  }
  class MyComponent3 extends Component {  
    render() {
      return <button>{this.props.data}</button>
    }
  }
  
  const MyComponentWithPersistentData = withPersistentData(MyComponent2)
  // 公用逻辑
  const MyComponentWithPersistentDataV2 = withPersistentData(MyComponent3)
  ```

  



### 说说对React Hooks的理解？解决了什么问题？

* **是什么**

  `Hook` 是 React 16.8 的新增特性。它可以让你在不编写 `class` 的情况下使用 `state` 以及其他的 `React` 特性

  在以前，函数组件也被称为无状态的组件，只负责渲染的一些工作

  现在的函数组件也可以是有状态的组件，内部也可以维护自身的状态以及做一些逻辑方面的处理

* **为什么**

  官方给出的动机是解决长时间使用和维护`react`过程中常遇到的问题

  1. **难以重用和共享组件中的与状态相关的逻辑**

     > 比如状态只能放在state中且只有一个，setState也只能有一个

  2. **逻辑复杂的组件难以开发与维护，当我们的组件需要处理多个互不相关的 local state 时，每个生命周期函数中可能会包含着各种互不相关的逻辑在里面**

  3. 类组件中的this增加学习成本，类组件在基于现有工具的优化上存在些许问题

  4. 由于业务变动，函数组件不得不改为类组件等等

* **有哪些**

  `Hooks`让我们的函数组件拥有了类组件的特性，例如组件内的状态、生命周期，最常见的有

  - useState
  - useEffect

* **useState**

  与类中的区别

  1. state声明方式：在函数组件中通过 useState 直接获取，类组件通过constructor 构造函数中设置

  2. state读取方式：在函数组件中直接使用变量，类组件通过`this.state.count`的方式获取
  3. state更新方式：在函数组件中通过 setCount 更新，类组件通过this.setState()
  4. 总的来讲，useState 使用起来更为简洁，减少了`this`指向不明确的情况

* **useEffect**

  `useEffect`可以让我们在函数组件中进行一些带有副作用的操作

  如果用类组件，组件加载和更新都执行同样的操作

  ```ts
    componentDidMount() {
      document.title = `You clicked ${this.state.count} times`;
    }
    componentDidUpdate() {
      document.title = `You clicked ${this.state.count} times`;
    }
  ```

  但是使用useEffect，就可以将相同的逻辑抽离出来，这是类组件不具备的方法

  **怎么用**

  * `useEffect`第一个参数接受一个回调函数，默认情况下，`useEffect`会在第一次渲染和更新之后都会执行，相当于在`componentDidMount`和`componentDidUpdate`两个生命周期函数中执行回调
  * 如果某些特定值在两次重渲染之间没有发生变化，你可以跳过对 effect 的调用，这时候只需要传入第二个 参数，一个数组
  * 回调函数中可以返回一个清除函数，这是`effect`可选的清除机制，相当于类组件中`componentwillUnmount`生命周期函数，可做一些清除副作用的操作

* **其他**
  - useReducer
  - useCallback
  - useMemo
  - useRef

* **解决什么**

  `hooks`能够更容易解决状态相关的重用的问题：

  * 每调用useHook一次都会生成一份独立的状态
  * 通过自定义hook能够更好的封装我们的功能

  编写`hooks`为函数式编程，每个功能都包裹在函数中，整体风格更清爽，更优雅

  `hooks`的出现，使函数组件的功能得到了扩充，拥有了类组件相似的功能，在我们日常使用中，使用`hooks`能够解决大多数问题，并且还拥有代码复用机制，因此优先考虑`hooks`



### 说说React render方法的原理？在什么时候会被触发？

* **原理**

  `render`函数在`react`中有两种形式：

  1. 在类组件中，指的是`render`方法：

     ```tsx
     class Foo extends React.Component {
         render() {
             return <h1> Foo </h1>;
         }
     }
     ```

  2. 在函数组件中，指的是函数组件本身：

     ```tsx
     function Foo() {
         return <h1> Foo </h1>;
     }
     ```

  在render中，我们会编写jsx，jsx通过babel编译后转化成js对象

  ```tsx
  return (
    <div className='cn'>
      <Header> hello </Header>
      <div> start </div>
      Right Reserve
    </div>
  )
  
  // 编译后
  return (
    React.createElement(
      'div',
      {
        className : 'cn'
      },
      React.createElement(
        Header,
        null,
        'hello'
      ),
      React.createElement(
        'div',
        null,
        'start'
      ),
      'Right Reserve'
    )
  )
  ```

  在react中，使用createElement来创建虚拟DOM，接收三个参数，虚拟dom最终会渲染成真实DOM

  在`render`过程中，`React` 将新调用的 `render`函数返回的树与旧版本的树进行比较，这一步是决定如何更新 `DOM` 的必要步骤，然后进行 `diff` 比较，更新 `DOM`树



* **触发时机**

  * 类组件只要执行了 `setState` 方法，就一定会触发 `render` 函数执行，函数组件使用`useState`更改状态不一定导致重新`render`

    > 因为useState会判断改了的状态是不是和原来的一样

  * 组件的`props` 改变了，不一定触发 `render` 函数的执行，但是如果 `props` 的值来自于父组件或者祖先组件的 `state`，在这种情况下，父组件或者祖先组件的 `state` 发生了改变，就会导致子组件的重新渲染，因为父组件重新渲染



### 说说你是如何提高组件的渲染效率的？在React中如何避免不必要的render？

* **是什么**

  `react` 基于虚拟 `DOM` 和高效 `Diff`算法的完美配合，实现了对 `DOM`最小粒度的更新，大多数情况下，`React`对 `DOM`的渲染效率足以我们的业务日常。但是在复杂业务场景下，性能问题以然会困扰我们

* **如何做**

  前面说到，类组件通过调用`setState`方法， 就会导致`render`，父组件一旦发生`render`渲染，子组件一定也会执行`render`渲染

  则，若父组件渲染导致子组件渲染，子组件并没有发生任何改变，这时候就可以从避免无谓的渲染，具体实现的方式有如下

  - shouldComponentUpdate
  - PureComponent
  - React.memo

* **shouldComponentUpdate**

  通过`shouldComponentUpdate`生命周期函数来比对 `state`和 `props`，确定是否要重新渲染

  默认情况下返回`true`表示重新渲染，如果不希望组件重新渲染，返回 `false` 即可

* **PureComponent**

  跟`shouldComponentUpdate`原理基本一致，通过对 `props` 和 `state`的浅比较结果来实现 `shouldComponentUpdate`

  > 让自己的组件继承这个Component就行了
  >
  > 非深度，只深一层

* **React.memo**

  `React.memo`用来缓存组件的渲染，避免不必要的更新，其实也是一个高阶组件，与 `PureComponent` 十分类似。但不同的是， `React.memo` 只能用于函数组件

  ```tsx
  import { memo } from 'react';
  
  function Button(props) {
    // Component code
  }
  
  export default memo(Button);
  ```

  memo是浅层的，可以给第二个参数自定比较

  ```tsx
  function arePropsEqual(prevProps, nextProps) {
    // your code
    return prevProps === nextProps;
  }
  
  export default memo(Button, arePropsEqual);
  ```

  



### 说说react中引入css的方式有哪几种？区别？

* **是什么**

  组件式开发选择合适的`css`解决方案尤为重要，通常会遵循以下规则：

  - 可以编写局部css，不会随意污染其他组件内的原生；
  - 可以编写动态的css，可以获取当前组件的一些状态，根据状态的变化生成不同的css样式；
  - 支持所有的css特性：伪类、动画、媒体查询等；
  - 编写起来简洁方便、最好符合一贯的css风格特点

  在这一方面，`vue`使用`css`起来更为简洁：

  - 通过 style 标签编写样式
  - scoped 属性决定编写的样式是否局部有效
  - lang 属性设置预处理器
  - 内联样式风格的方式来根据最新状态设置和改变cs

  而在`react`中，引入`CSS`就不如`Vue`方便简洁，其引入`css`的方式有很多种，各有利弊

  > 其不会在组件内向vue那样直接有style标签

* **方式**

  常见的`CSS`引入方式有以下：

  - **在组件内直接使用**

    直接在组件中书写`css`样式，通过`style`属性直接引入

    ```ts
    const div1 = {
      width: "300px",
      margin: "30px auto",
      backgroundColor: "#44014C",  //驼峰法
      minHeight: "200px",
      boxSizing: "border-box"
    };
    
    <div style={div1}>123</div>
    <div style={{backgroundColor:"red"}}>
    ```

    **优点**

    - 内联样式, 样式之间不会有冲突
    - 可以动态获取当前state中的状态

    **缺点**

    - 写法上都需要使用驼峰标识
    - 某些样式没有提示
    - 大量的样式, 代码混乱
    - 某些样式无法编写(比如伪类/伪元素)

  - **组件中引入 .css 文件**

    将`css`单独写在一个`css`文件中，然后在组件中直接引入

    > 与纯html不同的是这里使用import引入，然后正常用

    **缺点**

    样式是全局生效，样式之间会互相影响

  - **组件中引入 .module.css 文件**

    将`css`文件作为一个模块引入，这个模块中的所有`css`，只作用于当前组件。不会影响当前组件的后代组件

    这种方式是`webpack`特供的方案，只需要配置`webpack`配置文件中`modules:true`即可

    ```ts
    import './App.module.css';  // 引用的是App.css,用module只是为了模块
    ```

    **缺点**

    不方便动态来修改某些样式，依然需要使用内联样式的方式动态修改样式

  - **CSS in JS**

    是指一种模式，其中`CSS`由 `JavaScript`生成而不是在外部文件中定义

    此功能由第三方库提供，如`styled-component`、`semotiong`、`lamorous`

    下面主要看`styled-components`的基本使用**本质是通过函数的调用，最终创建出一个组件：**

    - 这个组件会被自动添加上一个`不重复的class`
    - styled-components会给该class添加相关的样式

    ```ts
    export const SelfLink = styled.div`
      height: 50px;
      border: 1px solid red;
      color: yellow;
    `;
    ```

* **区别**
  * 在组件内直接使用`css`该方式编写方便，容易能够根据状态修改样式属性，但是大量的样式编写容易导致代码混乱
  * 组件中引入 .css 文件符合我们日常的编写习惯，但是作用域是全局的，样式之间会层叠
  * 引入.module.css 文件能够解决局部作用域问题，但是不方便动态修改样式，需要使用内联的方式进行样式的编写
  * 通过css in js 这种方法，可以满足大部分场景的应用，可以类似于预处理器一样样式嵌套、定义、修改状态等
  * 至于使用`react`用哪种方案引入`css`，并没有一个绝对的答案，可以根据各自情况选择合适的方案



 

### 在react中组件间过渡动画如何实现？

在`react`中，`react-transition-group`是一种很好的解决方案，其为元素添加`enter`，`enter-active`，`exit`，`exit-active`这一系列勾子可以帮助我们方便的实现组件的入场和离场动画

其主要提供了三个主要的组件：

- CSSTransition：在前端开发中，结合 CSS 来完成过渡动画效果
- SwitchTransition：两个组件显示和隐藏切换时，使用该组件
- TransitionGroup：将多个动画组件包裹在其中，一般用于列表中元素的动画



**CSSTransition**

* **原理**

  `CSSTransition`的`in`属性置为`true`时，`CSSTransition`首先会给其子组件加上`xxx-enter`、`xxx-enter-active`的`class`执行动画

  当动画执行结束后，会移除两个`class`，并且添加`-enter-done`的`class`

  当`in`属性置为`false`时，`CSSTransition`会给子组件加上`xxx-exit`和`xxx-exit-active`的`class`，然后开始执行动画，当动画结束后，移除两个`class`，然后添加`-enter-done`的`class`

  所以可以利用这一点，通过`css`的`transition`属性，让元素在两个状态之间平滑过渡，从而得到相应的动画效果

  ```tsx
  <CSSTransition
      in={show}
      timeout={500}
      classNames={'fade'}
      unmountOnExit={true}
      >
      <div className={'square'} />
  </CSSTransition>
  ```

  ```ts
  .fade-enter {
    opacity: 0;
    transform: translateX(100%);
  }
  
  .fade-enter-active {
    opacity: 1;
    transform: translateX(0);
    transition: all 500ms;
  }
  ```

### SwitchTransition

`SwitchTransition`可以完成两个组件之间切换的炫酷动画

比如有一个按钮需要在`on`和`off`之间切换，我们希望看到`on`先从左侧退出，`off`再从右侧进入

* **原理**

  `SwitchTransition`中主要有一个属性`mode`，对应两个值：

  - in-out：表示新组件先进入，旧组件再移除；
  - out-in：表示就组件先移除，新组建再进入

  `SwitchTransition`组件里面要有`CSSTransition`，不能直接包裹你想要切换的组件

  里面的`CSSTransition`组件不再像以前那样接受`in`属性来判断元素是何种状态，取而代之的是`key`属性

```tsx
<SwitchTransition mode="out-in">
    <CSSTransition classNames="btn"
        timeout={500}
        key={isOn ? "on" : "off"}>
        {
            <button onClick={this.btnClick.bind(this)}>
                {isOn ? "on": "off"}
            </button>
        }
    </CSSTransition>
</SwitchTransition>
```

> key仍可决定CSSTransition要加的属性

```css
.btn-enter {
  transform: translate(100%, 0);
  opacity: 0;
}

.btn-enter-active {
  transform: translate(0, 0);
  opacity: 1;
  transition: all 500ms;
}

.btn-exit {
  transform: translate(0, 0);
  opacity: 1;
}

.btn-exit-active {
  transform: translate(-100%, 0);
  opacity: 0;
  transition: all 500ms;
}
```

### TransitionGroup

当有一组动画的时候，就可将这些`CSSTransition`放入到一个`TransitionGroup`中来完成动画

同样`CSSTransition`里面没有`in`属性，用到了`key`属性

`TransitionGroup`在感知`children`发生变化的时候，先保存移除的节点，当动画结束后才真正移除

> 原位置先占用一会

* **处理方式**
  - 插入的节点，先渲染dom，然后再做动画
  - 删除的节点，先做动画，然后再删除dom

```tsx
<TransitionGroup>
    {
        this.state.friends.map((item, index) => {
            return (
                <CSSTransition classNames="friend" timeout={300} key={index}>
                    <div>{item}</div>
                </CSSTransition>
            )
        })
    }
</TransitionGroup>
```

> 动画自己写一下

```css
.friend-enter {
    transform: translate(100%, 0);
    opacity: 0;
}

.friend-enter-active {
    transform: translate(0, 0);
    opacity: 1;
    transition: all 500ms;
}

.friend-exit {
    transform: translate(0, 0);
    opacity: 1;
}

.friend-exit-active {
    transform: translate(-100%, 0);
    opacity: 0;
    transition: all 500ms;
}
```



### 说说你对Redux的理解？其工作原理？

* **是什么**

  `React`是用于构建用户界面的，帮助我们解决渲染`DOM`的过程

  而在整个应用中会存在很多个组件，每个组件的`state`是由自身进行管理，包括组件定义自身的`state`，组件之间的通信通过`props`传递，使用`Context`实现数据共享

  如果让每个组件都存储自身相关的状态，理论上来讲不会影响应用的运行，但在开发及后续维护阶段，我们将花费大量精力去查询状态的变化过程

  这种情况下，如果将所有的状态进行集中管理，当需要更新状态的时候，仅需要对这个管理集中处理，而不用去关心状态是如何分发到每一个组件内部的

  `redux`就是一个实现上述集中管理的容器，遵循三大基本原则：

  - 单一数据源
  - state 是只读的
  - 使用纯函数来执行修改

  注意的是，`redux`并不是只应用在`react`中，还与其他界面库一起使用，如`Vue`

* **工作原理**

  `redux`要求我们把数据都放在 `store`公共存储空间

  一个组件改变了 `store` 里的数据内容，其他组件就能感知到 `store`的变化，再来取数据，从而间接的实现了这些数据传递的功能

  工作流程如图

  ![img](https://static.vue-js.com/27b2e930-e56b-11eb-85f6-6fac77c0c9b3.png)

  

* **如何使用**

  创建一个`store`的公共数据区域

  ```tsx
  import { createStore } from 'redux' // 引入一个第三方的方法
  const store = createStore() // 创建数据的公共存储区域
  ```

  需要一个reducer管理数据，本质就是一个函数，接收两个参数`state`，`action`，返回`state`

  ```tsx
  // 设置默认值
  const initialState = {
    counter: 0
  }
  
  const reducer = (state = initialState, action) => {
  }
  ```

  可以将reducer传递给`store`，两者建立连接

  ```tsx
  const store = createStore(reducer)
  ```

  获取的时候使用store.getState()`来获取当前`state

  ```tsx
  console.log(store.getState());
  ```

  修改数据时，通过是通过`dispatch`来派发`action`，通常`action`中都会有`type`属性，也可以携带其他的数据

  ```tsx
  store.dispatch({
    type: "INCREMENT"
  })
  ```

  在redux中，应该有相应的处理逻辑

  > `reducer`是一个纯函数，不需要直接修改`state`

  ```tsx
  const reducer = (state = initialState, action) => {
    switch (action.type) {
      case "INCREMENT":
        return {...state, counter: state.counter + 1};
      default: 
        return state;
    }
  }
  ```

  派发之后，可以通过store.subscribe监听`store`的变化

  ```tsx
  store.subscribe(() => {
    console.log(store.getState());
  })
  ```

* **总结**
  - createStore可以帮助创建 store
  - store.dispatch 帮助派发 action , action 会传递给 store
  - store.getState 这个方法可以帮助获取 store 里边所有的数据内容
  - store.subscrible 方法订阅 store 的改变，只要 store 发生改变， store.subscrible 这个函数接收的这个回调函数就会被执行



### 说说对Redux中间件的理解？常用的中间件有哪些？实现原理？

中间件（Middleware）是介于应用系统和系统软件之间的一类软件，它使用系统软件所提供的基础服务（功能），衔接网络上应用系统的各个部分或不同的应用，能够达到资源共享、功能共享的目的

* **是什么**

  `Redux`整个工作流程，当`action`发出之后，`reducer`立即算出`state`，整个过程是一个同步的操作

  那么如果需要支持异步操作，或者支持错误处理、日志监控，这个过程就可以用中间件

  `Redux`中，中间件就是放在就是在`dispatch`过程，在分发`action`前进行拦截处理

  其本质上一个函数，对`store.dispatch`方法进行了改造，在发出 `Action`和执行 `Reducer`这两步之间，添加了其他功能

  ![img](https://static.vue-js.com/57edf750-e699-11eb-ab90-d9ae814b240d.png)

* **常用的中间件**

  有很多优秀的`redux`中间件，如：

  - redux-thunk：用于异步操作
  - redux-logger：用于日志记录

  上述的中间件都需要通过`applyMiddlewares`进行注册，作用是将所有的中间件组成一个数组，依次执行

  然后作为第二个参数传入到`createStore`中

  ```tsx
  const store = createStore(
    reducer,
    applyMiddleware(thunk, logger)
  );
  ```

* **redux-thunk**

  官网推荐的异步处理中间件

  默认情况下的`dispatch(action)`，`action`需要是一个`JavaScript`的对象

  `redux-thunk`中间件会判断你当前传进来的数据类型，如果是一个函数，将会给函数传入参数值（dispatch，getState）

  - dispatch函数用于我们需要再派发action
  - getState函数考虑到我们之后的一些操作需要依赖原来的状态，用于让我们可以获取之前的一些状态

  ```tsx
  const getHomeMultidataAction = () => {
    return (dispatch) => {
      axios.get("http://xxx.xx.xx.xx/test").then(res => {
        const data = res.data.data;
        dispatch(changeBannersAction(data.banner.list)); 
        dispatch(changeRecommendsAction(data.recommend.list));
      })
    }
  }
  ```

* **redux-logger**

  如果想要实现一个日志功能，则可以使用现成的`redux-logger`

  ```js
  import { applyMiddleware, createStore } from 'redux';
  import createLogger from 'redux-logger';
  const logger = createLogger();
  
  const store = createStore(
    reducer,
    applyMiddleware(logger)
  );
  ```



### 你在React项目中是如何使用Redux的? 项目结构是如何划分的？

* **是什么**

  `redux`是用于数据状态管理，而`react`是一个视图层面的库

  如果将两者连接在一起，可以使用官方推荐`react-redux`库，其具有高效且灵活的特性

  `react-redux`将组件分成：

  - 容器组件：存在逻辑处理
  - UI 组件：只负责现显示和交互，内部不处理逻辑，状态由外部控制

  通过`redux`将整个应用状态存储到`store`中，组件可以派发`dispatch`行为`action`给`store`

  其他组件通过订阅`store`中的状态`state`来更新自身的视图

* **怎么做**

  使用`react-redux`分成了两大核心：

  - Provider
  - connection

* **Provider**

  在`redux`中存在一个`store`用于存储`state`，如果将这个`store`存放在顶层元素中，其他组件都被包裹在顶层元素之上，那么所有的组件都能够受到`redux`的控制，都能够获取到`redux`中的数据

  ```tsx
  <Provider store = {store}>
      <App />
  <Provider>
  ```

![img](https://static.vue-js.com/3e47db10-e7dc-11eb-85f6-6fac77c0c9b3.png)

* **项目结构**

  1. **按角色组织**

     ```tsx
     reducers/
       todoReducer.js
       filterReducer.js
     actions/
       todoAction.js
       filterActions.js
     components/
       todoList.js
       todoItem.js
       filter.js
     containers/
       todoListContainer.js
       todoItemContainer.js
       filterContainer.js
     ```

  2. **按功能组织**

     使用`redux`使用功能组织项目，也就是把完成同一应用功能的代码放在一个目录下，一个应用功能包含多个角色的代码

     > - actionTypes.js 定义action类型
     > - actions.js 定义action构造函数
     > - reducer.js 定义这个功能模块如果响应actions.js定义的动作
     > - views 包含功能模块中所有的React组件，包括展示组件和容器组件
     > - index.js 把所有的角色导入，统一导出

     ```tsx
     todoList/
       actions.js
       actionTypes.js
       index.js
       reducer.js
       views/
         components.js
         containers.js
     filter/
       actions.js
       actionTypes.js
       index.js
       reducer.js
       views/
         components.js
         container.js
     ```









### 说说你对React Router的理解？常用的Router组件有哪些？

* **是什么**

  `react-router`等前端路由的原理大致相同，可以实现无刷新的条件下切换显示不同的页面

  路由的本质就是页面的`URL`发生改变时，页面的显示结果可以根据`URL`的变化而变化，但是页面不会刷新

  `eact-router`主要分成了几个不同的包：

  - react-router: 实现了路由的核心功能
  - react-router-dom： 基于 react-router，加入了在浏览器运行环境下的一些功能
  - react-router-native：基于 react-router，加入了 react-native 运行环境下的一些功能
  - react-router-config: 用于配置静态路由的工具库

* **有哪些**

  常见的是react-router-dom提供的一些常用的组件 

  - BrowserRouter、HashRouter
  - Route
  - Link、NavLink
  - switch
  - redirect

* **BrowserRouter、HashRouter**

  Router中包含了对路径改变的监听，并且会将相应的路径传递给子组件

  `BrowserRouter`是`history`模式，`HashRouter`是`hash`模式

  两者作为最顶层组件包裹其他组件,字组件能通过props接收到history对象

  ```tsx
  import { BrowserRouter as Router } from "react-router-dom";
  
  export default function App() {
    return (
      <Router>
        <main>
          <nav>
            <ul>
              <li>
                < a href=" ">Home</ a>
              </li>
              <li>
                < a href="/about">About</ a>
              </li>
              <li>
                < a href="/contact">Contact</ a>
              </li>
            </ul>
          </nav>
        </main>
      </Router>
    );
  }
  ```

* **Route**

  `Route`用于路径的匹配，然后进行组件的渲染，对应的属性如下：

  - path 属性：用于设置匹配到的路径
  - component 属性：设置匹配到路径后，渲染的组件
  - render 属性：设置匹配到路径后，渲染的内容
  - exact 属性：开启精准匹配，只有精准匹配到完全一致的路径，才会渲染对应的组件

  ```tsx
  import { BrowserRouter as Router, Route } from "react-router-dom";
  
  export default function App() {
    return (
      <Router>
        <main>
          <nav>
            <ul>
              <li>
                < a href="/">Home</ a>
              </li>
              <li>
                < a href="/about">About</ a>
              </li>
              <li>
                < a href="/contact">Contact</ a>
              </li>
            </ul>
          </nav>
          <Route path="/" render={() => <h1>Welcome!</h1>} />
        </main>
      </Router>
    );
  }
  ```

* **Link、NavLink**

  通常路径的跳转是使用`Link`组件，最终会被渲染成`a`元素，其中属性`to`代替`a`标题的`href`属性

  `NavLink`是在`Link`基础之上增加了一些样式属性，例如组件被选中时，发生样式变化，则可以设置`NavLink`的一下属性：

  - activeStyle：活跃时（匹配时）的样式
  - activeClassName：活跃时添加的class

  ```tsx
  <NavLink to="/" exact activeStyle={{color: "red"}}>首页</NavLink>
  <NavLink to="/about" activeStyle={{color: "red"}}>关于</NavLink>
  <NavLink to="/profile" activeStyle={{color: "red"}}>我的</NavLink>
  ```

* **switch**

  用于路由的重定向，当这个组件出现时，就会执行跳转到对应的`to`路径中，如下例子：

  > Route会在props中提供match

  ```tsx
  const About = ({
    match: {
      params: { name },
    },
  }) => (
    // props.match.params.name
    <Fragment>
      {name !== "tom" ? <Redirect to="/" /> : null}
      <h1>About {name}</h1>
      <FakeText />
    </Fragment>
  )
  ```

* **switch**

  `switch`组件的作用适用于当匹配到第一个组件的时候，后面的组件就不应该继续匹配

  ```tsx
  <Switch>
    <Route exact path="/" component={Home} />
    <Route path="/about" component={About} />
    <Route path="/profile" component={Profile} />
    <Route path="/:userid" component={User} />
    <Route component={NoMatch} />
  </Switch>
  ```



> 除了一些路由相关的组件之外，`react-router`还提供一些`hooks`，如下：
>
> - useHistory
> - useParams
> - useLocation

* **useHistory**

  `useHistory`可以让组件内部直接访问`history`，无须通过`props`获取

* **useParams**

  useParams可以直接访问`params`，无需通过`props`获取

* **useLocation**

  `useLocation` 会返回当前 `URL`的 `location`对象





### 说说react-router传参方式

路由传递参数主要分成了三种形式：

- **动态路由的方式**

  路由中的路径并不会固定，`path`在`Route`匹配时写成`/detail/:id`，那么 `/detail/abc`、`/detail/123`都可以匹配到该

  ```tsx
  <NavLink to="/detail/abc123">详情</NavLink>
  
  <Switch>
      ... 其他Route
      <Route path="/detail/:id" component={Detail}/>
      <Route component={NoMatch} />
  </Switch>
  ```

  ```tsx
  console.log(props.match.params.xxx) //获取方式
  ```

- **search传递参数**

  ```tsx
  <NavLink to="/detail2?name=why&age=18">详情2</NavLink>
  
  <Switch>
    <Route path="/detail2" component={Detail2}/>
  </Switch>
  ```

  ```tsx
  console.log(props.location.search)
  ```

- **to传入对象**

  ```tsx
  <NavLink to={{
      pathname: "/detail2", 
      query: {name: "kobe", age: 30},
      state: {height: 1.98, address: "洛杉矶"},
      search: "?apikey=123"
    }}>
    详情2
  </NavLink>
  ```

  ```tsx
  console.log(props.location)
  ```









### 说说React Router有几种模式？实现原理？

* **是什么**

  在单页应用中，一个`web`项目只有一个`html`页面，一旦页面加载完成之后，就不用因为用户的操作而进行页面的重新加载或者跳转，其特性如下：

  - 改变 url 且不让浏览器像服务器发送请求
  - 在不刷新页面的前提下动态改变浏览器地址栏中的URL地址

  其中主要分成了两种模式：

  - hash 模式：在url后面加上#，如http://127.0.0.1:5500/home/#/page1
  - history 模式：允许操作浏览器的曾经在标签页或者框架里访问的会话历史记录

* **使用**

  `React Router`对应的`hash`模式和`history`模式对应的组件为：

  - HashRouter
  - BrowserRouter

  这两个组件的使用都十分的简单，作为最顶层组件包裹其他组件，如下所示

  ```tsx
  // 1.import { BrowserRouter as Router } from "react-router-dom";
  // 2.import { HashRouter as Router } from "react-router-dom";
  <Router>
      <Route path="/login" component={Login}/>
      <Route path="/backend" component={Backend}/>
      <Route path="/admin" component={Admin}/>
      <Route path="/" component={Home}/>
  </Router>
  ```

* **原理**

  路由描述了 `URL` 与 `UI`之间的映射关系，这种映射是单向的，即 URL 变化引起 UI 更新（无需刷新页面）

  下面以`hash`模式为例子，改变`hash`值并不会导致浏览器向服务器发送请求，浏览器不发出请求，也就不会刷新页面

  `hash` 值改变，触发全局 `window` 对象上的 `hashchange` 事件。所以 `hash` 模式路由就是利用`hashchange` 事件监听 `URL` 的变化，从而进行 `DOM` 操作来模拟页面跳转

* **HashRouter**

  `HashRouter`包裹了整应用，

  通过`window.addEventListener('hashChange',callback)`监听`hash`值的变化，并传递给其嵌套的组件

  然后通过`context`将`location`数据往后代组件传递，

  ```tsx
  import React, { Component } from 'react';
  import { Provider } from './context'
  // 该组件下Api提供给子组件使用
  class HashRouter extends Component {
    constructor() {
      super()
      this.state = {
        location: {
          pathname: window.location.hash.slice(1) || '/'
        }
      }
    }
    // url路径变化 改变location
    componentDidMount() {
      window.location.hash = window.location.hash || '/'
      window.addEventListener('hashchange', () => {
        this.setState({
          location: {
            ...this.state.location,
            pathname: window.location.hash.slice(1) || '/'
          }
        }, () => console.log(this.state.location))
      })
    }
    render() {
      let value = {
        location: this.state.location
      }
      return (
        <Provider value={value}>
          {
            this.props.children
          }
        </Provider>
      );
    }
  }
  
  export default HashRouter;
  
  ```

  `Route`组件主要做的是通过`BrowserRouter`传过来的当前值，通过`props`传进来的`path`与`context`传进来的`pathname`进行匹配，然后决定是否执行渲染组件

  ```tsx
  import React, { Component } from 'react';
  import { Consumer } from './context'
  const { pathToRegexp } = require("path-to-regexp");
  class Route extends Component {
    render() {
      return (
        <Consumer>
          {
            state => {
              console.log(state)
              let {path, component: Component} = this.props
              let pathname = state.location.pathname
              let reg = pathToRegexp(path, [], {end: false})
              // 判断当前path是否`包含`pathname
              if(pathname.match(reg)) {
                return <Component></Component>
              }
              return null
            }
          }
        </Consumer>
      );
    }
  }
  export default Route;
  
  ```

  

### 说说React diff的原理是什么？

* **是什么**

  跟`Vue`一致，`React`通过引入`Virtual DOM`的概念，极大地避免无效的`Dom`操作，使我们的页面的构建效率提到了极大的提升

  而`diff`算法就是更高效地通过对比新旧`Virtual DOM`来找出真正的`Dom`变化之处

  > 只是找出变化之处，具体后面怎么操作DOM diff算法不管

  传统diff算法通过循环递归对节点进行依次对比，效率低下，算法复杂度达到 O(n^3)，`react`将算法进行一个优化，复杂度姜维`O(n)`

  > O(n^3)是因为传统二叉树节点两两比较是n^2,每次比较里面还有一些操作O(n),所以就3了

* **原理**

  `react`中`diff`算法主要遵循三个层级的策略：

  * tree层级
  * conponent 层级
  * element 层级

* **tree层级**

  > 策略原因
  >
  > Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计

  `DOM`节点只会对相同层级的节点进行比较,如下面相同颜色的是相同层级

  如果跨层级移动，那个移动的根会重新创建，不会简单移动

  ![img](https://static.vue-js.com/ae71d1c0-ec91-11eb-85f6-6fac77c0c9b3.png)

* **conponent 层级**

  > 策略：拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构。

  如果是同一个类的组件，则会继续往下`diff`运算，如果不是一个类的组件，那么直接删除这个组件下的所有子节点，创建新的(不同类型的 component 是很少存在相似 DOM tree 的机会)

  下面虽然只是D换成了G且两者结构一致，但是也会删除左边红框一整个，换成右边的

  ![img](https://static.vue-js.com/c1fcdf00-ec91-11eb-ab90-d9ae814b240d.png)

* **element层级**

  > 策略：对于比较同一层级的节点们，每个节点在对应的层级用唯一的`key`作为标识

  提供了 3 种节点操作，分别为 `INSERT_MARKUP`(插入)、`MOVE_EXISTING` (移动)和 `REMOVE_NODE` (删除)

  ![img](https://static.vue-js.com/cae1c9a0-ec91-11eb-ab90-d9ae814b240d.png)

  

  通过`key`可以准确地发现新旧集合中的节点都是相同的节点，因此无需进行节点删除和创建，只需要将旧集合中节点的位置进行移动，更新为新集合中节点的位置，下面讲具体如何移动：

  **算法描述**

  react的diff算法的主要思想就是将原来的节点数组中与新的对比，将在原数组中靠左但是在新数组中靠右的节点移到右边。因为新的节点遍历过程中，新节点的位置是越来越靠右的，所以只需要保证当前遍历到的节点在旧数组移动到已经遍历到的节点靠右的位置即可。

  我们需要维护新老数组，然后**遍历新数组**，同时维护以下信息

  - index： 新集合的遍历下标。
  - oldIndex：当前节点在老集合中的下标
  - maxIndex：在新集合访问过的节点中，其在老集合的最大下标

  遍历过程中，对比oldIndex和maxIndex

  1. 如果`oldIndex < maxIndex`

     首先，当前节点应该保证在所有以访问的节点最右边，但是`oldIndex < maxIndex`说明在老数组中，当前节点没有维护在已经遍历的节点最右边，所以要将节点从oldIndex位置移动到maxIndex，其他节点顺位往前退

     > 如果oldIndex=-1，则创建一个，放到maxIndex

  2. `oldIndex = maxIndex`

     不操作

  3. `oldIndex>maxIndex`

     此时老数组中当前遍历到的节点对比已经遍历过的节点靠右，不用移动，将oldIndex的值赋值给maxIndex即可。

  当比较完成后，`diff`过程还没完，还会整体遍历老集合中节点，看有没有没用到的节点，有的话，就删除

  

  流程表：

  ![img](https://static.vue-js.com/d34c5420-ec91-11eb-85f6-6fac77c0c9b3.png)

​	

> 但是会有缺陷，有时候其实只需要移动一个元素，但是却三个都移动了比如
>
> 旧: A B C D
>
> 新: D A B C
>
> 此时比较的过程中，A，B，C都依次要放到D的右边，移动了三次
>
> 所以尽量减少类似将最后一个节点移动到列表首部的操作

> 上面只是得出了差异队列，至于怎么patch的，还得深究

### 注意事项

对于简单列表渲染而言，不使用`key`比使用`key`的性能，由于`dom`节点的移动操作开销是比较昂贵的，没有`key`的情况下要比有`key`的性能更好

```tsx
1.加key
<div key='1'>1</div>             <div key='1'>1</div>     
<div key='2'>2</div>             <div key='3'>3</div>  
<div key='3'>3</div>  ========>  <div key='2'>2</div>  
<div key='4'>4</div>             <div key='5'>5</div>  
<div key='5'>5</div>             <div key='4'>4</div>  
操作：节点2移动至下标为2的位置，节点4移动至下标为4的位置。

2.不加key
<div>1</div>             <div>1</div>     
<div>2</div>             <div>3</div>  
<div>3</div>  ========>  <div>2</div>  
<div>4</div>             <div>5</div>  
<div>5</div>             <div>4</div>  
操作：修改第1个到第5个节点的innerText，因为内部判断改动的时候，只判断text修改的化话，不会改这个DOM，只换text，因为有静态节点的机制
```





### 说说对Fiber架构的理解？解决了什么问题？

* **问题**

  `JavaScript`引擎和页面渲染引擎两个线程是互斥的，当其中一个线程执行时，另一个线程只能挂起等待

  如果 `JavaScript` 线程长时间地占用了主线程，那么渲染层面的更新就不得不长时间地等待，界面长时间不更新，会导致页面响应度变差，用户可能会感觉到卡顿

  而这也正是 `React 15` 的 `Stack Reconciler`所面临的问题，当 `React`在渲染组件时，从开始到渲染完成整个过程是一气呵成的，无法中断

  如果组件较大，那么`js`线程会一直执行，然后等到整棵`VDOM`树计算完成后，才会交给渲染的线程

  这就会导致一些用户交互、动画等任务无法立即得到处理，导致卡顿的情况

* **是什么**

  React Fiber 是 Facebook 花费两年余时间对 React 做出的一个重大改变与优化，是对 React 核心算法的一次重新实现

  在`react`中，主要做了以下的操作：

  * 为每个增加了优先级，优先级高的任务可以中断低优先级的任务。然后再重新，注意是重新执行优先级低的任务
  * 增加了异步任务，调用requestIdleCallback api，浏览器空闲的时候执行
  * dom diff树变成了链表，一个dom对应两个fiber（一个链表），对应两个队列，这都是为找到被中断的任务，重新执行

  从架构角度来看，`Fiber` 是对 `React`核心算法（即调和过程）的重写

  从编码角度来看，`Fiber`是 `React`内部所定义的一种数据结构，它是 `Fiber`树结构的节点单位，也就是 `React 16` 新架构下的虚拟`DOM`

  一个 `fiber`就是一个 `JavaScript`对象，包含了元素的信息、该元素的更新操作队列、类型

* 怎么解决

  * `Fiber`把渲染更新过程拆分成多个子任务，每次只做一小部分，做完看是否还有剩余时间，如果有继续下一个任务；如果没有，挂起当前任务，将时间控制权交给主线程，等主线程不忙的时候在继续执行

  * 即可以中断与恢复，恢复后也可以复用之前的中间状态，并给不同的任务赋予不同的优先级，其中每个任务更新单元为 `React Element` 对应的 `Fiber`节点，保存了该组件的类型（函数组件/类组件/原生组件等等）、对应的 DOM 节点等信息。

  * 作为动态的工作单元来说，每个 `Fiber` 节点保存了本次更新中该组件改变的状态、要执行的工作。

  * 每个 Fiber 节点有个对应的 `React element`，多个 `Fiber`节点根据如下三个属性构

    ```tsx
    // 指向父级Fiber节点
    this.return = null
    // 指向子Fiber节点
    this.child = null
    // 指向右边第一个兄弟Fiber节点
    this.sibling = null
    ```

  * 实现的上述方式的是`requestIdleCallback`方法

    `window.requestIdleCallback()`方法将在浏览器的空闲时段内调用的函数排队。这使开发者能够在主事件循环上执行后台和低优先级工作，而不会影响延迟关键事件，如动画和输入响应

    

### 说说React Jsx转换成真实DOM过程？

* **是什么**

  `react`通过将组件编写的`JSX`映射到屏幕，以及组件中的状态发生了变化之后 `React`会将这些「变化」更新到屏幕上

  ```tsx
  <div>
    < img src="avatar.png" className="profile" />
    <Hello />
  </div>
  ```

  在前面文章了解中，`JSX`通过`babel`最终转化成`React.createElement`这种形式

  ```tsx
  React.createElement(
    "div",
    null,
    React.createElement("img", {
      src: "avatar.png",
      className: "profile"
    }),
    React.createElement(Hello, null)
  );
  ```

  

  最终都会通过`RenderDOM.render(...)`方法进行挂载，如下：

  ```tsx
  ReactDOM.render(<App />,  document.getElementById("root"));
  ```

* **过程**

  在`react`中，节点大致可以分成四个类别

  - 原生标签节点
  - 文本节点
  - 函数组件
  - 类组件
  
  ```tsx
  < a href=" ">xxx</ a>
  <p>xx</p >
  <FunctionComponent name="函数组件" />
  <ClassComponent name="类组件" color="red" />
  ```
  
  这些类别最终都会被转化成`React.createElement`这种形式
  
  `React.createElement`其被调用时会传⼊标签类型`type`，标签属性`props`及若干子元素`children`，作用是生成一个虚拟`Dom`对象，如下所示：
  
  ```tsx
  function createElement(type, config, ...children) {
      if (config) {
          delete config.__self;
          delete config.__source;
      }
      // ! 源码中做了详细处理，⽐如过滤掉key、ref等
      const props = {
          ...config,
          children: children.map(child =>
              typeof child === "object" ? child : createTextNode(child)
          )
      };
      return {
          type,
          props
      };
  }
  // 生成一个文本节点
  function createTextNode(text) {
      return {
          type: TEXT,
          props: {
              children: [],
              nodeValue: text
          }
      };
  }
  
  ```
  
  `createElement`会根据传入的节点信息进行一个判断：
  
  - 如果是原生标签节点， type 是字符串，如div、span
  - 如果是文本节点， type就没有，这里是 TEXT
  - 如果是函数组件，type 是函数名
  - 如果是类组件，type 是类名
  
  虚拟`DOM`会通过`ReactDOM.render`进行渲染成真实`DOM`，使用方法如下：
  
  ```tsx
  ReactDOM.render(element, container[, callback])
  ```
  
  当首次调用时，容器节点里的所有 `DOM` 元素都会被替换，后续的调用则会使用 `React` 的 `diff`算法进行高效的更新
  
  如果提供了可选的回调函数`callback`，该回调将在组件被渲染或更新之后被执行
  
  `render`大致实现方法如下：
  
  ```tsx
  function render(vnode, container) {
      console.log("vnode", vnode); // 虚拟DOM对象
      // vnode _> node
      const node = createNode(vnode, container);
      container.appendChild(node);
  }
  
  // 创建真实DOM节点
  function createNode(vnode, parentNode) {
      let node = null;
      const {type, props} = vnode;
      if (type === TEXT) {
          node = document.createTextNode("");
      } else if (typeof type === "string") {
          node = document.createElement(type); // 原生标签
      } else if (typeof type === "function") { // 函数和类的type都是function
          node = type.isReactComponent
              ? updateClassComponent(vnode, parentNode)
          : updateFunctionComponent(vnode, parentNode);
      } else {
          node = document.createDocumentFragment(); // 创建一个空的
      }
      reconcileChildren(props.children, node);
      updateNode(node, props);
      return node;
  }
  
  // 遍历下子vnode，然后把子vnode->真实DOM节点，再插入父node中
  function reconcileChildren(children, node) {
      for (let i = 0; i < children.length; i++) {
          let child = children[i];
          if (Array.isArray(child)) {
              for (let j = 0; j < child.length; j++) {
                  render(child[j], node);
              }
          } else {
              render(child, node);
          }
      }
  }
  function updateNode(node, nextVal) {
      Object.keys(nextVal)
          .filter(k => k !== "children")
          .forEach(k => {
          if (k.slice(0, 2) === "on") {
              let eventName = k.slice(2).toLocaleLowerCase();
              node.addEventListener(eventName, nextVal[k]);
          } else {
              node[k] = nextVal[k];
          }
      });
  }
  
  // 返回真实dom节点
  // 执行函数
  function updateFunctionComponent(vnode, parentNode) {
      const {type, props} = vnode;
      let vvnode = type(props); // 执行函数返回真实的节点
      const node = createNode(vvnode, parentNode);
      return node;
  }
  
  // 返回真实dom节点
  // 先实例化，再执行render函数
  function updateClassComponent(vnode, parentNode) {
      const {type, props} = vnode;
      let cmp = new type(props);
      const vvnode = cmp.render();
      const node = createNode(vvnode, parentNode);
      return node;
  }
  export default {
      render
  };
  ```

* **总结**

  ![img](https://static.vue-js.com/28824fa0-f00a-11eb-ab90-d9ae814b240d.png)

  * 使用React.createElement或JSX编写React组件，实际上所有的 JSX 代码最后都会转换成React.createElement(...) ，Babel帮助我们完成了这个转换的过程。
  * createElement函数对key和ref等特殊的props进行处理，并获取defaultProps对默认props进行赋值，并且对传入的孩子节点进行处理，最终构造成一个虚拟DOM对象
  * ReactDOM.render将生成好的虚拟DOM渲染到指定容器上，其中采用了批处理、事务等机制并且对特定浏览器进行了性能优化，最终转换为真实DOM





### 说说 React 性能优化的手段有哪些？

* **是什么**

  `React`凭借`virtual DOM`和`diff`算法拥有高效的性能，但是某些情况下，性能明显可以进一步提高

  在前面文章中，我们了解到类组件通过调用`setState`方法， 就会导致`render`，父组件一旦发生`render`渲染，子组件一定也会执行`render`渲染

  当我们想要更新一个子组件的时候，如下图绿色部分

  ![img](https://static.vue-js.com/b41f6f30-f270-11eb-ab90-d9ae814b240d.png)

​	理想状态只调用该路径下的组件`render`，生成这几个组件的新虚拟DOM

​	![img](https://static.vue-js.com/bc0f2460-f270-11eb-85f6-6fac77c0c9b3.png)

但是`react`的默认做法是调用所有组件的`render`，再对生成的虚拟`DOM`进行对比（黄色部分），如不变则不进行更新

![img](https://static.vue-js.com/c2f0c4f0-f270-11eb-85f6-6fac77c0c9b3.png)

从上图可见，黄色部分`diff`算法对比是明显的性能浪费的情况

* **怎么做**

  避免不必要的`render`来应付上面的问题，主要手段是通过`shouldComponentUpdate`、`PureComponent`、`React.memo`，这三种形式这里就不再复述

  除此之外， 常见性能优化常见的手段有如下

  - **避免使用内联函数**

    如果我们使用内联函数，则每次调用`render`函数时都会创建一个新的函数实例

    ```tsx
    <input type="button" onClick={(e) => { this.setState({inputValue: e.target.value}) }} value="Click For Inline Function" />
    ```

    我们应该在组件内部创建一个函数，并将事件绑定到该函数本身。这样每次调用 `render` 时就不会创建单独的函数实例

    > 是类组件，函数组件这样也会重新生成，除非使用useCallback

    ```tsx
     <input type="button" onClick={this.setNewStateData} value="Click For Inline Function" />
    ```

  - **使用 React Fragments 避免额外标记**

    用户创建新组件时，每个组件应具有单个父标签。父级不能有两个标签，所以顶部要有一个公共标签，所以我们经常在组件顶部添加额外标签`div`

    这个额外标签除了充当父标签之外，并没有其他作用，这时候则可以使用`fragement`

  - **懒加载组件**

    从工程方面考虑，`webpack`存在代码拆分能力，可以为应用创建多个包，并在运行时动态加载，减少初始包的大小

    而在`react`中使用到了`Suspense`和 `lazy`组件实现代码拆分功能，基本使用如下

    ```ts
    const johanComponent = React.lazy(() => import(/* webpackChunkName: "johanComponent" */ './myAwesome.component'));
     
    export const johanAsyncComponent = props => (
      <React.Suspense fallback={<Spinner />}>
        <johanComponent {...props} />
      </React.Suspense>
    );
    ```

  - **事件绑定方式**

    从性能方面考虑，在`render`方法中使用`bind`和`render`方法中使用箭头函数这两种形式在每次组件`render`的时候都会生成新的方法实例，性能欠缺

    而`constructor`中`bind`事件与定义阶段使用箭头函数绑定这两种形式只会生成一个方法实例，性能方面会有所改善

  - **服务端渲染**

  

### 说说你在React项目是如何捕获错误的？

* **是什么**

  在`react`项目中去编写组件内`JavaScript`代码错误会导致 `React` 的内部状态被破坏，导致整个应用崩溃，这是不应该出现的现象。作为一个框架，`react`也有自身对于错误的处理的解决方案

* **怎么做**

  为了解决出现的错误导致整个应用崩溃的问题，`react16`引用了**错误边界**新的概念

  错误边界是一种 `React` 组件，这种组件可以捕获发生在其子组件树任何位置的 `JavaScript` 错误，并打印这些错误，同时展示降级 `UI`，而并不会渲染那些发生崩溃的子组件树

  错误边界在渲染期间、生命周期方法和整个组件树的构造函数中捕获错误

  形成错误边界组件的两个条件：

  - 使用了 static getDerivedStateFromError()
  - 使用了 componentDidCatch()

  抛出错误后，请使用 `static getDerivedStateFromError()` 渲染备用 UI ，使用 `componentDidCatch()` 打印错误信息

  ```tsx
  class ErrorBoundary extends React.Component {
    constructor(props) {
      super(props);
      this.state = { hasError: false };
    }
  
    static getDerivedStateFromError(error) {
      // 更新 state 使下一次渲染能够显示降级后的 UI
      return { hasError: true };
    }
  
    componentDidCatch(error, errorInfo) {
      // 你同样可以将错误日志上报给服务器
      logErrorToMyService(error, errorInfo);
    }
  
    render() {
      if (this.state.hasError) {
        // 你可以自定义降级后的 UI 并渲染
        return <h1>Something went wrong.</h1>;
      }
  
      return this.props.children; 
    }
  }
  ```

  然后就可以把自身组件的作为错误边界的子组件，如下：

  ```tsx
  <ErrorBoundary>
    <MyWidget />
  </ErrorBoundary>
  ```

  下面这些情况无法捕获到异常：

  - 事件处理
  - 异步代码
  - 服务端渲染
  - 自身抛出来的错误

在`react 16`版本之后，会把渲染期间发生的所有错误打印到控制台

除了错误信息和 JavaScript 栈外，React 16 还提供了组件栈追踪。现在你可以准确地查看发生在组件树内的错误信息：

![img](https://static.vue-js.com/7b2b51d0-f289-11eb-ab90-d9ae814b240d.png)

对于错误边界无法捕获的异常，如事件处理过程中发生问题并不会捕获到，是因为其不会在渲染期间触发，并不会导致渲染时候问题,这时候可以自己在事件处理的时候加catch

除此之外还可以通过监听`onerror`事件

```tsx
window.addEventListener('error', function(event) { ... })
```

