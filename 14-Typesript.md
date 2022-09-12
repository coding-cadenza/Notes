### 说说你对 TypeScript 的理解？与 JavaScript 的区别？

* **是什么**
  * `TypeScript` 是 `JavaScript` 的类型的超集(子集得反义词)，支持`ES6`语法，支持面向对象编程的概念，如类、接口、继承、泛型等
  * 其是一种静态类型检查的语言，提供了类型注解，在代码编译阶段就可以检查出数据类型的错误
* **特性**
  * **类型批注和编译时类型检查** ：在编译时批注变量类型
  * **类型推断**：ts 中没有批注变量类型会自动推断变量的类型
  * **类型擦除**：在编译过程中批注的内容和接口会在运行时利用工具擦除、
  * **接口**：ts 中用接口来定义对象类型
  * **枚举**：用于取值被限定在一定范围内的场景
  * **泛型编程**：写代码时使用一些以后才指定的类型
  * **名字空间**：名字只在该区域内有效，其他区域可重复使用该名字而不冲突
  * **元组**：元组合并了不同类型的对象，相当于一个可以装不同类型数据的数组

* **区别**
  * TypeScript 是 JavaScript 的超集，扩展了 JavaScript 的语法
  * TypeScript 可处理已有的 JavaScript 代码，并只对其中的 TypeScript 代码进行编译
  * 在编写 TypeScript 的文件的时候就会自动编译成 js 文件
  * 扩展名不同
  * 支持静态类型检查，JS没有静态类型得概念
  * 支持可选参数方法



### typescript 的数据类型有哪些？

* **列举**

  - boolean（布尔类型）
  - number（数字类型）
  - string（字符串类型）
  - array（数组类型）

  - object 对象类型
  - null 和 undefined 类型
  - tuple（元组类型）
  - enum（枚举类型）
  - any（任意类型）
  - void 类型
  - never 类型

* **具体**

  * **array**

    两种写法

    1. ```ts
       let arr:string[] = ['12', '23'];
       ```

    2. ```ts
       // 使用数组泛型
       let arr:Array<number> = [1, 2];
       ```

  * **tuple**

    允许表示一个已知元素数量和类型的数组，各元素的类型不必相同

    赋值的类型、位置、个数需要和定义（生明）的类型、位置、个数一致

    ```ts
    let tupleArr:[number, string, boolean];
    tupleArr = [12, '34', true]; //ok
    typleArr = [12, '34'] // no ok
    ```

  * **null 和 undefined**

    默认情况下`null`和`undefined`是所有类型的子类型， 就是说你可以把 `null`和 `undefined`赋值给 `number`类型的变量

    但是如果`ts`配置了`--strictNullChecks`标记，`null`和`undefined`只能赋值给`void`和它们各自

  * **void**

    用于标识方法返回值的类型，表示该方法没有返回值。

  * **never**

    `never`是其他类型 （包括`null`和 `undefined`）的子类型，可以赋值给任何类型，代表从不会出现的值

    `never` 类型一般用来指定那些总是会抛出异常、无限循环

    ```ts
    // 返回never的函数必须存在无法达到的终点
    function error(message: string): never {
        throw new Error(message);
    }
    ```

    



### 说说你对 TypeScript 中枚举类型的理解？应用场景？

* **是什么**

  枚举是一个被命名的整型常数的集合，用于声明一组命名的常数,当一个变量有几种可能的取值时,可以将它定义为枚举类型**，通俗来说，枚举就是一个变量的所有可能取值的集合**

* **使用**

  * 通过`enum`关键字进行定义

    ```ts
    enum xxx { ... }
    ```

  * 声明方法

    ```ts
    let d: xxx;
    ```

* **分类**

  1. **数字枚举**

     当我们声明一个枚举类型是,虽然没有给它们赋值,但是它们的值其实是默认的数字类型,而且默认从0开始依次累加,如果将某个值赋值，后面的值惠根据前一个值累加1

     ```ts
     enum Direction {
         Up,   // 值默认为 0
         Down, // 值默认为 1
         Left, // 值默认为 2
         Right // 值默认为 3
     }
     ```

  2. **字符串枚举**

     如果设定了一个变量为字符串之后，后续的字段也需要赋值字符串，否则报错：

     ```ts
     enum Direction {
         Up = 'Up',
         Down = 'Down',
         Left = 'Left',
         Right = 'Right'
     }
     ```

  3. **异构枚举**

     上述联合

* **本质**

  本质上是进行了键值的双向映射

  > 枚举可合并

  ```ts
  enum Direction {
      Up,
      Down,
      Left,
      Right
  }
  
  // 编译后
  var Direction;
  (function (Direction) {
      Direction[Direction["Up"] = 0] = "Up";
      Direction[Direction["Down"] = 1] = "Down";
      Direction[Direction["Left"] = 2] = "Left";
      Direction[Direction["Right"] = 3] = "Right";
  })(Direction || (Direction = {}));
  ```

* **场景**

  就拿回生活的例子，后端返回的字段使用 0 - 6 标记对应的日期，这时候就可以使用枚举可提高代码可读性





### 说说你对 TypeScript 中接口的理解？应用场景？

* **是什么**

  **接口**是一系列抽象方法的声明，一个接口所描述的是一个对象相关的属性和方法，但并不提供具体创建此对象实例的方法，能利用这些声明为你的代码或者第三方的代码定义约束

* **使用**

  ```ts
  interface User {
      name: string
      age: number
  }
  
  const getUserName = (user: User) => user.name
  ```

* **特征**

  1. 可选属性

  2. 只读属性

  3. 索引签名

     ```ts
     interface User {
         name: string
         age: number
         [propName: string]: any;
     }
     ```

  4. 能够继承

* **应用场景**

  例如在`javascript`中定义一个函数，用来获取用户的姓名和年龄，如果多人开发的都需要用到这个函数的时候，如果没有注释，则可能出现各种**运行时的错误**，这时候就可以使用接口定义参数变量：

  ```js
  // 先定义一个接口
  interface IUser {
    name: string;
    age: number;
  }
  
  const getUserInfo = (user: IUser): string => {
    return `name: ${user.name}, age: ${user.age}`;
  };
  
  // 只能正确的调用
  getUserInfo({name: "koala", age: 18});
  ```

  

### 说说你对 TypeScript 中类的理解？

* **是什么**

  在 `ES6` 之后，`JavaScript` 拥有了 `class` 关键字，虽然本质依然是构造函数，但是使用起来已经方便了许多，但是`JavaScript` 的`class`依然有一些特性还没有加入，比如修饰符和抽象类；`TypeScript` 的 `class` 支持面向对象的所有特性，比如 类、接口等

* **使用**

  * **类包含的模块**

    字段、构造函数、方法

    ```ts
    class Car {
        // 字段
        engine:string;
    
        // 构造函数
        constructor(engine:string) {
            this.engine = engine
        }
    
        // 方法
        disp():void {
            console.log("发动机为 :   "+this.engine)
        }
    }
    ```

  * **继承**

    类的继承使用过`extends`的关键字,类继承后，子类可以对父类的方法重新定义

  * **修饰符**

    1. **私有修饰符**

       只能够在该类的内部进行访问，实例对象并不能够访问;并且继承该类的子类并不能访问

       ```ts
       class Father{
           privaate name:String
           constructor(name:String){
               this.name = name; // 这里this.name是上面那个name
           }
       }
       class Son extends Father{
           say(){
               console.log(this.name) // 错误
           }
       }
       const father = new Father("huhu")
       father.name  // 报错
       ```

    2. **受保护修饰符**

       实例对象并不能够访问，但是子类可以

    3. **只读修饰符**

       只读属性必须在声明时或构造函数里被初始化，并且不可被修改

  * **静态属性**

    通过`static`进行定义，访问这些属性需要通过 类型.静态属性

  * **抽象类**

    抽象类做为其它派生类的基类使用，它们一般不会直接被实例化，不同于接口，抽象类可以包含成员的实现细节

    ```ts
    // 这个不能直接被实例化
    abstract class Animal {
        abstract makeSound(): void;
        move(): void {
            console.log('roaming the earch...');
        }
    }
    ```





### 说说你对 TypeScript 中函数的理解？与 JavaScript 函数的区别？

* **是什么**

  `TypeScript` 为 `JavaScript` 函数添加了额外的功能，丰富了更多的应用场景

* **使用方法**

  1. **定义参数类型或返回值类型**

  2. **可选参数**

  3. **剩余类型**

  4. **函数重载**

     * 允许创建数个名称相同但输入输出类型或个数不同的子程序，它可以简单地称为一个单独功能可以执行多项任务的能力
     * 关于`typescript`函数重载，必须要把精确的定义放在前面，最后函数实现时，需要使用 `|`操作符或者`?`操作符，把所有可能的输入类型全部包含进去，用于具体实现

     ```ts
     // 上边是声明
     function add (arg1: string, arg2: string): string
     function add (arg1: number, arg2: number): number
     // 因为我们在下边有具体函数的实现，所以这里并不需要添加 declare 关键字
     
     // 下边是实现
     function add (arg1: string | number, arg2: string | number) {
       // 在实现上我们要注意严格判断两个参数的类型是否相等，而不能简单的写一个 arg1 + arg2
       if (typeof arg1 === 'string' && typeof arg2 === 'string') {
         return arg1 + arg2
       } else if (typeof arg1 === 'number' && typeof arg2 === 'number') {
         return arg1 + arg2
       }
     }
     ```

* **区别**
  1. typescript 声明函数需要定义参数类型或者声明返回值类型
  2. typescript 在参数中，添加可选参数供使用者选择
  3. typescript 增添函数重载功能





### 说说你对 TypeScript 中泛型的理解？

* **是什么**

  泛型允许我们在强类型程序设计语言中编写代码时使用一些以后才指定的类型，在实例化时作为参数指明这些类型

  ```ts
  function returnItem<T>(para: T): T {
      return para
  }
  ```

* **基本使用**

  可以声明：

  - **函数**

    ```ts
    function returnItem<T>(para: T): T {
        return para
    }
    
    // 可以一次定义多个类型参数
    function swap<T, U>(tuple: [T, U]): [U, T] {
        return [tuple[1], tuple[0]];
    }
    
    swap([7, 'seven']); // ['seven', 7]
    ```

  - **接口**

    ```ts
    interface ReturnItemFn<T> {
        (para: T): T
    }
    ```

  - **类**

    ```ts
    class Stack<T> {
        private arr: T[] = []
    
        public push(item: T) {
            this.arr.push(item)
        }
    
        public pop() {
            this.arr.pop()
        }
    }
    ```

* **多类型约束**

  需要实现两个接口的类型约束,可以先创建一个接口继承这两个接口，再用继承地这个约束泛型

  ```ts
  interface ChildInterface extends FirstInterface, SecondInterface {
  }
  
  class Demo<T extends ChildInterface> {
  }
  ```

  



### 说说你对 TypeScript 中高级类型的理解？有哪些？

* **是什么**

  高级类型，是`typescript`为了保证语言的灵活性，所使用的一些语言特性。这些特性有助于我们应对复杂多变的开发场景

* **有哪些**

  - 交叉类型
  - 联合类型
  - 类型别名
  - 类型索引
  - 类型约束
  - 映射类型
  - 条件类型

* **解释**

  1. **交叉类型**

     通过 `&` 将多个类型合并为一个类型，包含了所需的所有类型的特性，适用于对象合并场景

     ```ts
     T & U
     ```

  2. **联合类型**

     表示其类型为连接的多个类型中的任意一个，且只能是一个,注意如果是接口联合，那么对象的属性必须是多个接口的共同属性

  3. **类型别名**

     会给一个类型起个新名字，类型别名有时和接口很像，**但是可以作用于原始值、联合类型、元组以及其它任何你需要手写的类型**

     ```ts
     type some = boolean | string
     const b: some = true // ok
     ```

     类型别名可以是泛型

     ```ts
     type Container<T> = { value: T };
     ```

  4. **类型索引**

     用于获取一个接口中 Key 的联合类型

     ```ts
     interface Button {
         type: string
         text: string
     }
     type ButtonKeys = keyof Button
     // 等效于
     type ButtonKeys = "type" | "text"
     ```

  5. **类型约束**

     通过关键字 `extend` 进行约束，不同于在 `class` 后使用 `extends` 的继承作用，泛型内使用的主要作用是对泛型加以约束，类型约束通常和类型索引一起使用。

     > 下面直接用BaseType是因为我们需要知道参数的类型并且使用类型

     ```ts
     type BaseType = string | number | boolean
     // 这里表示 copy 的参数只能是字符串、数字、布尔这几种基础类型
     function copy<T extends BaseType>(arg: T): T {
       return arg
     }
     ```

  6. **映射类型**

     通过 `in` 关键字做类型的映射，遍历已有接口的 `key` 或者是遍历联合类型

     ```ts
     type Readonly<T> = {
         readonly [P in keyof T]: T[P];
     };
     ```

  7. **条件类型**

     语法规则和三元表达式一致，经常用于一些类型不确定的情况。

     ```ts
     // 如果 T 是 U 的子集，就是类型 X，否则为类型 Y
     T extends U ? X : Y
     ```

     

  



### 说说你对 TypeScript 装饰器的理解？应用场景？

* **是什么**

  装饰器是一种特殊类型的声明，它能够被附加到类声明，方法， 访问符，属性或参数上，是一种在不改变原类和使用继承的情况下，动态地扩展对象功能

* **使用**

  需要在tsconfig.json种配置

  ```ts
  {
      "compilerOptions": {
          "target": "ES5",
          "experimentalDecorators": true
      }
  }
  ```

* **装饰类**

  当装饰器作为修饰类的时候，会把构造器传递进去。

  ```ts
  function addAge(constructor: Function) {
    constructor.prototype.age = 18;
  }
  
  @addAge
  class Person{
    name: string;
    age!: number;
    constructor() {
      this.name = 'huihui';
    }
  }
  ```

* **方法/属性装饰**

  装饰器可以用于修饰类的方法，这时候装饰器函数接收的参数变成了

  - target：对象的原型
  - propertyKey：方法的名称
  - descriptor：方法的属性描述符

* **装饰参数**

  接收3个参数，分别是：

  - target ：当前对象的原型
  - propertyKey ：参数的名称
  - index：参数数组中的位置



### 说说对 TypeScript 中命名空间与模块的理解？区别

* **模块**

  `TypeScript` 与`ECMAScript` 2015 一样，任何包含顶级 `import` 或者 `export` 的文件都被当成一个模块，相反地，如果一个文件不带有顶级的`import`或者`export`声明，那么它的内容被视为全局可见的！

  > 所以在一个文件声明一个const在另一个文件再声明一个就会出错，可以通过`import`或者`export`引入模块系统解决这个问题
  >
  > ```ts
  > const a = 10;
  > 
  > export default a
  > ```

​	在`typescript`中，`export`关键字可以导出变量或者类型

* **命名空间**

  命名空间一个最明确的目的就是解决重名问题，命名空间定义了标识符的可见范围，一个标识符可在多个名字空间中定义，它在不同名字空间中的含义是互不相干的

  * 用namespace定义一个命名空间

    ```ts
    namespace SomeNameSpaceName {
       export interface ISomeInterfaceName {      }
       export class SomeClassName {      }
    }
    ```

  * 外部使用

    ```ts
    SomeNameSpaceName.SomeClassName
    ```

  * 本质

    命名空间本质上是一个对象，作用是将一系列相关的全局变量组织到一个对象的属性，如下：

    ```ts
    namespace Letter {
      export let a = 1;
      export let b = 2;
      export let c = 3;
      // ...
      export let z = 26;
    }
    
    var Letter;
    (function (Letter) {
        Letter.a = 1;
        Letter.b = 2;
        Letter.c = 3;
        // ...
        Letter.z = 26;
    })(Letter || (Letter = {}));
    
    ```

* **区别**

  * 命名空间很难去识别组件之间的依赖关系，尤其是在大型的应用中，但是模块可以通过声明依赖识别组件间的依赖关系

  

