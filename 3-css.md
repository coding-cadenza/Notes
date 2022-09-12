### 伪类和伪元素以及异同

* **伪类**
  * 核心是在元素处于某种状态时为其添加对应的样式，选择DOM树之外的信息
  * 由于状态的变化是⾮静态的，所以元素达到⼀个特定状态时，它可能得到⼀个伪类的样式；当状态改变时，它⼜会失去这个样式。
  * 它的功能和class有些类似，但它是基于⽂档之外的抽象，所以叫 伪类
* **伪元素**
  * 是DOM树没有定义的元素
  * 伪元素控制的内容和元素是没有差别的，但是它本身只是基于元素的抽象，并不存在于⽂档中，所以称为伪元素。

* **区别**

  * 表示方法

    伪类用单冒号表示，但是伪元素大多数使用双冒号表示

  * 定义不同

    * 伪类即假的类，可以添加类来达到效果
    * 伪元素即假元素，需要通过添加元素才能达到效果

* **相同点**

  * 伪类和伪元素都不出现在源⽂件和DOM树中。也就是说在html源⽂件中是看不到伪类和伪元素的。

### 继承

继承是一种规则，它允许样式不仅应用于特定的html标签元素，而且应用于其后代元素

下面的可继承属性是分元素类型的，有的类型的元素有的属性不能继承

**可继承的属性有：**

* **字体系列属性**

  > font开头那堆

* **文本系列属性**

  > text-indent：文本缩进
  >
  > text-align：文本水平对齐
  >
  > line-height：行高
  >
  > word-spacing：增加或减少单词间的空白（即字间隔）
  >
  > letter-spacing：增加或减少字符间的空白（字符间距）
  >
  > text-transform：控制文本大小写
  >
  > direction：规定文本的书写方向
  >
  > color：文本颜色 a元素除外

* **元素可见性**

  visibility

* **表格布局属性**

* **列表布局属性**

  > list-style-type、list-style-image、list-style-position、list-style

* **生成内容属性**

* **光标属性**

  > cursor

* **页面样式属性**

* **声音样式属性**





### css预处理工具

**CSS 预处理器**是一个能让你通过预处理器自己独有的语法来生成CSS的程序

css预处理器种类繁多，三种主流css预处理器是Less、Sass（Scss）及Stylus



### 行内元素和块级元素和行内块元素的区别，如何互换

* **块级元素**
  1. 独占一行
  2. 自动填充父元素
  3. 可以设置margin、padding以及高度和宽度
* **行内元素**
  1. 不会独占一行
  2. 不能设置宽高
  3. 在垂直方向margin和padding失效
  4. 宽度随着元素的内容而变化

* **行内块元素**
  1. 不独占一行
  2. 可以设置宽高
  3. margin、padding水平垂直方向都有效

* **转换**

  ```js
  display: inline // 转成行内元素
  display: block  // 转成块级元素
  dispaly: inline-block; //转化成行内块元素
  ```



### 块级元素可以继承哪些属性

* btext-align
* text-indent
* visibility
* cursor





### 盒模型

盒子模型就是用来装页面上的元素的矩形区域，包括外边距（margin）、边框（border）、内边距（padding）、实际内容（content）四个属性

* **W3C盒子模型**

  `with = content`

* **IE盒模型**

  `with = content + padding +margin`

* **如何设置**

  ```js
  box-sizing:content-box
  box-sizing:border-box
  ```



### js如何获取元素的宽高

* **方法一**

  只能获取行内样式的宽和高，style 标签中和 link 外链的样式取不到

  ```js
  dom.style.width/height
  ```

* **方法二**

  （只有IE兼容）取到的是最终渲染后的宽和高

  ```js
  dom.currentStyle.width/height
  ```

* **方法三**

  包括高度（宽度）、内边距和边框，不包括外边距。最常用，兼容性最好。

  ```js
  dom.offsetWidth/offsetHeight
  ```

  

### 块级格式上下文BFC

* **定义**

  BFC是CSS布局的一个概念，是一块独立的渲染区域，是一个环境，里面的元素不会影响到外部的元素。决定了其子元素如何布局，以及和其他元素之间的关系和作用

* **BFC规则**
  * 内部的Box会在垂直方向，从顶部一个接一个地放置
  * Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生合并。（水平不会）(取大的)
  * BFC的区域不会与`float box`重叠（文字环绕的时候）
  * 计算BFC的高度时，浮动元素也参与计算。(清除浮动)

* **如何生成**
  * 根元素，即HTML元素
  * 浮动的元素
  * display为line-block,table-cell,line-flex,flex之一
  * overflow不为visible
  * position不为static,relative

* **应用场景**

  * **避免外边距重叠**

    两个相邻元素放到不同的BFC就不会发生外边距重贴了

  * **自适应两栏布局 | 阻止元素被浮动元素覆盖**

    左边创建一个float盒子，右边盒子单独生成BFC,便可自适应宽度,因为不会重叠

  * **清除浮动**

  

### 行内格式化上下文IFC

* 内部的Box会在水平方向，从含块的顶部开始一个接着一个地放置；
* 这些Box之间的水平方向的margin，border和padding都有效；
* Box垂直对齐方式：以它们的底部、顶部对齐，或以它们里面的文本的基线（baseline）对齐（默认， 文本与图片对其）



### 样式优先级

* **样式分类**

  1. 行内

  2. 内联

     > 就是style标签

  3. 外部

     > link

* **选择器分类**
  * id选择器
  * class选择器
  * 标签选择器
  * 通用选择器: `*`
  * 属性选择器: `[type="text"]`
  * 伪类选择器: `:hover`
  * 伪元素选择器： `::after`
  * 子选择器、相邻选择器
  
* **权重计算规则**
  
  1. **内联样式**: 1000
  
  2. **ID选择器**: 0100
  
  3. **类、伪类和属性:** 0010

     > 类和属性竟然是一样的
  
  4. **标签选择器和伪元素选择器**：0001
  
  5. **子选择器、相邻元素选择器等**: 0000
  
  6. **继承的**：无
  
* **比较法则**

  * 选择器都有一个权值，权值大者优先

  * 权值相等时，后出现优先级大

    > 注意，权值可能会叠加，计算的时候不进位

  * 网页编写者设置的 CSS 样式的优先权高于浏览器所设置的样式

  * 继承的 CSS 样式不如后来指定的 CSS 样式；

  * 在同一组属性设置中标有!important规则的优先级最大

  * 通配符、子选择器、相邻选择器等的。虽然权值为0000，但是也比继承的样式优先。





### 盒子塌陷是什么

* **定义**

  本应该在父盒子内部的元素跑到了外部

* **原因**

  父元素没有设置高度，子元素全部浮动，没有其他非浮动的可见元素，父元素的高度塌陷为0

* **解决方法**

  1. 定盒子的宽高

  2. 父盒子浮动BFC，不友好，会影响布局

  3. 给父元素增加Overflow生成BFC

     > auto会出现滚动条
     >
     > hidden会导致内容不可见

  4. 引入清除浮动块

     也就是引入一个块元素然后设置clear，这个会引入多余的元素，不推荐

  5. 使用after伪元素清除浮动：推荐

     ```css
     .clearfix {*zoom: 1;}
     
     .clearfix:before,.clearfix:after {
     
     display: table;
     
     line-height: 0;
     
     content: "";
     
     }
     
     .clearfix:after {clear: both;}
     
     ```

  6. 父盒子设置border或者padding-top

  

### min-width/max-width 和属性间的覆盖规则？

* 当min-width和max-width发生冲突时，min-width是会覆盖max-width的

  > 就是min-width比max-width大的时候

* max-width和width冲突的时候，即使width设置了important，max-width也会覆盖width



### 浏览器是怎样解析CSS选择器的？

CSS选择器的解析是从右向左解析的。

若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能

两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点(叶子节点)，而从左向右的匹配规则的性能都浪费在了失败的查找上面





### 垂直水平居中

1. **绝对定位 + margin:auto**

```css
 div{
     position: absolute;
     margin: auto;
     left: 0;
     right: 0;
     bottom: 0;
     top: 0;
}
```

2. **绝对定位 + translate**

```css
div{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%);
    transform: translateY(-50%);
}
```

3. **flex布局**

```css
.father{
     display: flex;
     display: -webkit-flex;
     -webkit-justify-content:center;
     justify-content: center;
     -webkit-align-items:center;
     align-items: center;
}
```

4. **table布局**

> 设置父元素的display:table-cell,并且vertical-align:middle，text-align:center这样子元素可以实现垂直居中。

5. **视窗+translate**

```css
 div{
     width: 200px;
     height: 200px;
     margin: 50vh auto 0;
     transform: translate(0,-50%);
     background-color: pink;
}
```





### 文本元素如何居中

* **水平**

  * text-align

* **垂直**

  * 单行文本

    调整line-height和区域高度一致即可

  * 多行文本

    * 父级元素高度没定

      父级高度不固定的时，高度只能通过内部文本来撑开。所以，我们可以通过设置内填充（padding）的值来使文本看起来垂直居中，只需设置padding-top和padding-bottom的值相等

    * 父级元素高度固定

      vertical-align:middle +display:table-cell 使文字垂直居中

      > vertical-align:middle +display:table-cell能够使单行文字、多行文字都居中。但是因为 table-cell 是 inline 类型，所以会导致原来的块级元素每个 div 一行移动到了同一行。如果需要分列两行，需要在外面额外添加容器对位置进行控制。



### 用flex实现九宫格

html层面就是一个container里面有9个块元素

css层面

* 父元素flex布局设置自动换行，在排列方向每项间隔留白
* 子元素

```css
.container{
    display: flex;
    flex-wrap: wrap; /*需要时换行*/
    justify-content: space-around; /*各项周围留白*/
}
.block {
    padding-top: 30%; /*相对父元素宽度，使block有高度*/
    width: 30%; /*宽度和高度一致，则正方形出来了*/ 
    margin-top: 3%; /*上面的留白在水平方向不影响的，所以要margin，相对父元素宽度的*/
    border-radius: 10%; /*这个使相对自己的*/
    background-color: orange;
}
```



### CSS实现等腰三角形

等腰三角形简单，正方形切三边就是了

```js
div{
    width: 0;
    height: 0;
    border: 20px solid transparent;
    border-bottom: 20px solid pink;
}
```

> 如果使等边三角形，就要算一下了，面试官问了就是sb哈哈哈



### 实现一个直角扇形

让一个角有randius并且其半径等于宽高即可

```css
div {
      border-radius: 80px 0 0;
      width: 80px;
      height: 80px;
      background: #666;
    }
```



### 旋转45°角

rotate中加入角度值,旋转方式为顺时针的

```css
div{
    -webkit-transform: rotate(45deg); 
}
```



### 画一条0.5px的线

1. **使用scale缩放**

   要将基准点移到中下的位置，则缩放的时候就是向下折叠，能抗模糊

   ```css
   div{
       height: 1px;
       transform: scaleY(0.5);
       transform-origin: 50% 100%;
   }
   ```

2. **boxshadow**

   ```css
   div{
       height: 1px;
       background: none;
       box-shadow: 0 0.5px 0 #000;
   }
   ```

3. **viewport**

   ```html
   <meta name="viewport" content="width=device-width,initial-sacle=0.5">
   
   ```



### 三栏布局

1. **flex**

   父亲弹性布局，孩子各占一份

   ```css
   .fa {
     display: flex;
   }
    
   .child {
     flex: 1; /*各自占一份剩余空间*/
     background: #eee;
     margin: 10px;
   }
   ```

2. **流式布局**

   ```js
   .child{
       width:33.33%
   }
   ```

3. **float + BFC**

   * 两个div分别左右浮动
   * 中间BFC

4. **绝对定位**

   三个孩子一个left:0,一个right:0，中间那个left和right算一下

5. **table布局**

   * 父元素 display:table
   * 子元素 display:table-cell
   * left和right给宽度，中间不给

6. **圣杯布局**

   * 圣杯布局要求先渲染中间的内容，所以中间的内容要放最前面
   * 父亲左右padding留出左右孩子的宽度
   * 中间孩子宽度设置为100%(相对于content)
   * left设置`margin-left:-100%;(相对content)`走到content的最左边，再设置`left:宽度`走到空白区(此时position是relative)
   * right设置`margin-left`和`right`找到对应位置

   ```css
   .left,.center,.right{
        float: left;
        position: relative;
        height: 200px
   }
   html,body{
       height: 100%;
   }
   .container{
       height: 100%;
       position: relative;
       padding: 0 100px;
   }
   .left{
       width: 100px;
       margin-left: -100%;
       left: -100px;
       background-color: skyblue;
   }
   .right{
       width: 100px;
       right: -100px;
       margin-left: -100px;
       background-color: pink;
   }
   .center{
       width: 100%;
       background-color: greenyellow;
   }
   ```

   





### 移动端1px的问题

* **问题**

  1px的边框，再高清屏下，移动端的1px会很粗

* **归因**
  * DPR设备像素比，它是默认缩放为100%的情况下，设备像素和CSS像素的比值
  * 目前主流的屏幕DPR=2，所以1px的边框实际上高清屏下渲染成了2px，这样是有原因的，为了更清晰

* **方案**

  1. **改变css的值**

     ```css
     border:0.5px solid #E5E5E5
     ```

  2. **设置viewport的scale值**

     > 上面这俩结合起来就可以画1px的线那个了

  3. **使用边框图片**

     替代直接的边框

     ```js
      border: 1px solid transparent;
      border-image: url('./../../image/96.jpg') 2 repeat;
     ```

  3. **使用box-shadow实现**

     ```css
     box-shadow: 0  -1px 1px -1px #e5e5e5,   //上边线
     ```

  4. **使用伪元素**

  





### **三种文档流的定位方案**

* **常规流(Normal flow)**
  - 在常规流中，盒一个接着一个排列;
  - 在块级格式化上下文里面， 它们竖着排列；
  - 在行内格式化上下文里面， 它们横着排列;
  - 当position为static或relative，并且float为none时会触发常规流；
  - 对于静态定位，position: static，盒的位置是常规流布局里的位置；
  - 对于相对定位，position: relative，盒偏移位置由top、bottom、left、right属性定义。即使有偏移，仍然保留原有的位置，其它常规流不能占用这个位置。

* **浮动(Floats)**
  - 左浮动元素尽量靠左、靠上，右浮动同理
  - 这导致常规流环绕在它的周边，除非设置 clear 属性
  - 浮动元素不会影响块级元素的布局
  - 但浮动元素会影响行内元素的布局，让其围绕在自己周围，撑大父级元素，从而间接影响块级元素布局
  - 最高点不会超过当前行的最高点、它前面的浮动元素的最高点
  - 不超过它的包含块，除非元素本身已经比包含块更宽
  - 行内元素出现在左浮动元素的右边和右浮动元素的左边，左浮动元素的左边和右浮动元素的右边是不会摆放浮动元素的

* **绝对定位(Absolute positioning)**
  - 绝对定位方案，盒从常规流中被移除，不影响常规流的布局；
  - 它的定位相对于它的包含块，相关CSS属性：top、bottom、left、right；
  - 如果元素的属性position为absolute或fixed，它是绝对定位元素；
  - 对于position: absolute，元素定位将相对于上级元素中最近的一个relative、fixed、absolute，如果没有则相对于body；



### padding和margin百分比单位依据

margin与padding的百分比指定值时，一律参考**包含盒的宽度**。





### 什么是margin合并，合并的场景是什么，有什么意义

* **是什么**

  块级元素的上外边距（margin-top）与下外边距（margin-bottom）有时会合并为单个外边距，这样的现象称为“margin 合并”

* **场景有三种**

  1. **父级和第一个/最后一个子元素**

     > 这个比较难理解，为什么父亲和子元素的margin会合并，理解为父亲把孩子多余的margin截了吧

     * 父元素设置为块状格式化上下文元素（设置border/padding/overflow）
     * 父亲和第一个子元素之间添加内联元素分割

  2. **相邻兄弟margin合并**

     > 上面的bottom和下面的top

  3. **空块级元素的 margin 合并**

     ```css
     .father { overflow: hidden; } 
     .son { margin: 1em 0; }   // 这里上下应该有1em，所以son本来应该撑开2em，但是合并了，所以只撑开了1em
     
     <div class="father"> 
     	<div class="son"></div> 
     </div>
     ```

* **意义**

  * 兄弟的margin合并，能让连续段落首位的`margin`和中间的`margin`一致，而不会出现`1：2`的场景

  * 父子的`margin`合并，能让我们再向页面中插入`<div>`标签的时候不影响原来的块状布局

    ```css
    /*如若要在下面`div`外面嵌套`div`，如果父子外边距不合并，那么就阻断了原来的兄弟合并*/
    <div style="margin: 20px 0;"></div> 
    <div style="margin: 20px 0;"></div> 
    <div style="margin: 20px 0;"></div> 
    ```

  * 自身 margin 合并的意义在于可以避免不小心遗落或者生成的空标签影响排版和布局

    ```css
    /*这里自身合并加上兄弟合并，最后p对两行的间距基本没影响*/
    p{margin:10px;}
    <p>第一行</p>
    <p></p>
    <p></p>
    <p></p>
    <p></p>
    <p>第二行</p>
    ```

    



### css字体大小设置（三种）.em rem px

* **px(绝对长度单位)**

* **em(相对长度单位)**

  * 浏览器的默认字体都是16px，那么1em=16px，以此类推计算12px=0.75em

  * 为了简化font-size的换算，我们在body中写入一下代码,这样就好算多了，因为字体是整10

    ```css
    body {font-size: 62.5%;  } /*  公式16px*62.5%=10px  */ 
    ```

  * em会继承父级元素的字体大小，所以如果一个设置了font-size:1.2em的元素在另一个设置了font-size:1.2em的元素里，而这个元素又在另一个设置了font-size:1.2em的元素里，那么最后计算的结果是1.2X1.2X1.2=1.728em

* **rem(相对长度单位)**
  * 和em不同的是rem总是相对于根元素(如:root{})，而不像em一样使用级联的方式来计算尺寸。这种相对单位使用起来更简单。



### CSS3新特性

| 特性           | 属性                                                         |
| -------------- | ------------------------------------------------------------ |
| **边框**       | **圆角、阴影、边框图片`border-image`**                       |
| **背景**       | **background-size**、**background-origin**、**background-clip** |
| **2D、3D转换** | **translate() **、**rotate()** 、**scale()**、**skew()**、**matrix()** 、**rotateX()**、**rotateY()** |
| **过渡、动画** | **transition、animation**                                    |
| **布局**       | **flex**                                                     |
| **选择器**     | **first-of-type,nth-child**                                  |
| **颜色**       | **透明、rbga**                                               |
| **文本效果**   | **text-shadow**、**text-wrap**                               |
| **用户界面**   | **resize、box-sizing、outline-offset**                       |
| **媒体查询**   |                                                              |
| **自定义字体** |                                                              |
| **多列**       |                                                              |

### inline-block 的 div 之间的空隙，原因及解决

* **描述**

  几个inline-block之间会有一个小间隙

* **原因**

  我们在写代码的时候，会把标签写在不同的行，所以会存在换行符，换行符会被转成空格。

* **解决方法**

  1. 父元素中设置font-size:0,但是子元素要设置自己的font-size不然会被继承

  2. 将元素写在一行上

  3. inline-block元素添加float:left

  4. 子元素margin负值，但是要根据实际算出，不推荐

  5. 最优解

     设置父元素，display:table和word-spacing

     

### transition和animation的区别

* transition需要触发一个事件才能改变属性
* 而 animation 配合 @keyframe 可以不触发事件就触发这个动画
* 并且transition为2帧，从from .... to
* 
* 而animation可以一帧一帧的



### flex布局

* **容器属性**

  1. **flex-direction**

     决定主轴的方向（即子item的排列方法）

  2. **flex-wrap**

     决定换行规则

  3. **flex-flow**

     前面两个的合体

  4. **justify-content**

     主轴对齐方式

  5. **align-items**

     侧轴对齐方式(默认Y)

* **项目属性**

  1. **order属性**

     定义项目的排列顺序，**顺序越小，排列越靠前**，默认为0

  2. **flex-grow属性**

     * 决定了父元素在空间分配方向上**还有剩余空间时**，如何分配这些剩余空间
     * 其值为一个权重（也称扩张因子），默认为0
     * 权重总和小于1使，权重总和默认为1

  3. **flex-shrink**

     * 定义空间不够时各个元素如何收缩。其值默认为 1

     > 父元素 500px。三个子元素分别设置为 150px，200px，300px。
     >
     > 三个子元素的 flex-shrink 的值分别为 1，2，3
     >
     > 首先，计算子元素溢出多少：150 + 200 + 300 - 500 = -150px
     >
     > 每个元素收缩的权重为其 flex-shrink 乘以其宽度,所以总权重为 1 * 150 + 2 * 200 + 3 * 300 = 1450
     >
     > 三个元素分别收缩：
     >
     > - 150 * 1(flex-shrink) * 150(width) / 1450 = -15.5
     > - 150 * 2(flex-shrink) * 200(width) / 1450 = -41.4
     > - 150 * 3(flex-shrink) * 300(width) / 1450 = -93.1
     >
     > 如果权重总合小于1的时候那么`收缩的总空间`==`要收缩的空间*权重总和`

  4. **flex-basis**

     定义了在分配多余的空间，项目占据的空间,这个就比较直接

  5. **flex**

     前面三个的整合





### css动画如何实现

1. **创建动画序列**
   * 需要使用animation属性或其子属性，该属性允许配置动画时间、时长以及其他动画细节，但该属性不能配置动画的实际表现
   * 动画的实际表现是由 @keyframes规则实现
2. **transition也可实现动画**
   * transition强调过渡，是元素的一个或多个属性发生变化时产生的过渡效果
   * 同一个元素通过两个不同的途径获取样式，而第二个途径当某种改变发生（例如hover）时才能获取样式，这样就会产生过渡动画



### js动画和css3画的差异性

* **js动画**
  * JavaScript在浏览器的主线程中运行，而主线程中还有其它需要运行的JavaScript脚本：样式计算、布局、绘制任务等,对其干扰导致线程可能出现阻塞，从而造成丢帧的情况。
  * 代码的复杂度高于CSS动画
  * JavaScript动画控制能力很强, 可以在动画播放过程中对动画进行控制
  * js动画效果比css3动画丰富,有些动画效果，比如曲线运动,冲击闪烁,视差滚动效果
  * JS大多时候没有兼容性问题

* **css动画**
  * 代码相对简单，但是冗长
  * 对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码
  * CSS动画运行过程控制较弱,无法附加事件绑定回调函数，只能暂停
  * 如果CSS动画只是改变`transform`和`opacity`，这时整个CSS动画得以在`compositor thread`完成（而JS动画则会在`main thread`执行，然后触发`compositor`进行下一步操作）

* **结论**

  简单动画用CSS，复杂动画用js





### 用css实现一个硬币旋转的效果

```css
div {
     width: 200px;
     height: 200px;
     border-radius: 50%;
}
#coin {
    transform-style: preserve-3d;
    animation: spin 3s linear infinite;
}

.front {
    position: absolute;
    top: 0;
    background-color: yellow;
    transform: translateZ(10px);
}

.middle{
    position: absolute;
    top: 0;
    background-color: red;
    transform:translateZ(1px);
}
.back{
    background-color: blue;
}

@keyframes spin{
    0%{
        transform: rotateY(0);
    }
    100%{
        transform: rotateY(360deg);
    }
}
```





### 单行文本省略

```css
p{
    overflow:hidden;
    text-overflow:ellipsis; /*如果值是一个串，那么用这个串来修饰溢出文本*/ 
    white-space:nowrap;  // 不换行
}
```



### calc属性

* Calc用户动态计算长度值，任何长度值都可以使用calc()函数计算
* 要注意的是，运算符前后都需要保留一个空格

```css
width: calc(100% - 10px)；
```



### 改变一个DOM元素的字体颜色，不在它本身上进行操作

可以更改父元素的color,用遗传实现



### 说一下浏览器私有前缀

* 在CSS属性中，我们常常能看到-webkit-，-moz-之类的前缀，这种就叫做浏览器私有前缀，是浏览器对于新CSS属性的一个提前支持。-webkit-是webkit内核的，-moz-是Firefox Gecko内核，moz代表的是Firefox的开发商Mozilla。
* 为什么要有私有前缀呢？因为制定HTML和CSS标准的组织W3C动作是很慢的。通常，有w3c组织成员提出一个新属性，比如说圆角border-radius，大家都觉得好，但是w3c不会为这个属性制定标准，而是要走很复杂的程序，经过很多审查。而浏览器商不愿意等那么久，他们觉得一个属性已经够成熟了，就会在浏览器中加入支持。但是避免日后w3c公布标准时有所变更，就会加入一个私有前缀，比如-webkit-border-radius，通过这种方式来提前支持新属性，等到日后w3c公布了标准，border-radius的标准写法确立之后，再让新版的浏览器支持border-radius这种写法。
* 比方说，Chrome 10是不认border-radius这种写法的，只能用webkit-border-radius。而Chrome12就能认了。于是在写CSS的时候，这样写就能确保Chrome10和Chrome12浏览网页的时候都能够正确显示。







### position属性 比较

* **固定定位fixed**
  1. 元素的位置相对于浏览器窗口是固定位置，即使窗口是滚动的它也不会移动
  2. ixed定位使元素的位置与文档流无关，因此不占据空间
  3. Fixed定位的元素和其他元素重叠
* **相对定位relative**
  1. 如果对一个元素进行相对定位，它将出现在它所在的位置上
  2. 可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动
  3. 在使用相对定位时，无论是否进行移动，元素仍然占据**原来**的空间
  4. 移动元素会导致它覆盖其它框
* **绝对定位absolute**
  1. 绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于\<html>
  2. absolute 定位使元素的位置**与文档流无关**，因此不占据空间
  3. absolute 定位的元素和其他元素重叠
* **粘性定位sticky**
  1. 元素先按照普通文档流定位
  2. 然后相对于该元素在流中的BFC和最近的块级祖先元素定位
  3. 而后，元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位

* **默认定位Static**

  1. 默认值,没有定位
  2. 元素出现在正常的流中
  3. left等没用

* **inherit**

  规定应该从父元素继承position 属性的值





### 如何实现文字少的时候居中显示，文字多的时候居左

文字超过了之后，就全占满了，所以只要内层居中，外层居左即可

```css
.box{
    text-align:center;
}
.content{
    display:inline-block;
    text-align:left;
}
```

### 画一个横着的凹

利用父容器宽度为0时内容的首选最小宽度，也就是(英文字母最小宽度默认是连续的字母长度，中文的最小宽度是一个字)

这样使用外边框勾勒一下就出来了

```css
.ao { 
 display: inline-block; 
 width: 0; 
} 
.ao:before { 
 content: "love 你 love"; 
 outline: 2px solid #cd0000; 
 color: #fff; 
}
```

![OpAGSs.png](https://s1.ax1x.com/2022/04/30/OpAGSs.png)





### 什么是宽度分离原则

宽度分离原则就是CSS中的width属性不与影响宽度的padding/border一起出现

可以在父元素设置宽度，子元素不设置宽度而设置其他

> 针对content-box

```css
.father { 
 width: 180px; 
} 
.son { 
 margin: 0 20px; 
 padding: 20px; 
 border: 1px solid; 
}
```



### 为何父元素没有设置高度的时候，子元素高度100%失效

* **原因**

  * 因为在规范中，如果包含块的高度没有显式指定（即高度由内容决定），并且该元素不是绝对定位，则计算值为 `auto`

  * 那么子元素高度为`'auto' * 100/100 = NaN`

  * `宽度不一样`，在规范中，如果包含块的宽度取决于该元素的宽度，那么产生的布局在CSS 2.1 中是未定义的，所以可以由浏览器自由发挥，根据测试，此时子元素根据父元素的真实的计算值作为百分比计算的基数，而不是以`auto`为基数

* **解决方法**

  1. 父亲设置可生效的高度

  2. 使用绝对定位,相对于第一个定位的父亲，不管其有无设置有效高度

     > 绝对定位的宽高百分比计算是相对于 `padding box` 的
     >
     > 非绝对定位元素则是相对于 `content box` 计算的



### 下拉加载图片前占位

```css
img { visibility: hidden; } 
img[src] { visibility: visible; }
```

### 实现两栏等高

有如下效果图，css代码如所示。问如何实现两列`看起来`等高，而不管内容如何？

![O15jiV.png](https://s1.ax1x.com/2022/05/08/O15jiV.png)

**首先我们要清楚一个点--外部尺寸**

* 外部尺寸就是`padding+content+margin`
* 并且父容器的`overflow`计算子元素的尺寸是根据外部尺寸计算的

**对于两列的背景等高**

* 我们可以设置`padding-bottom ：9999px`，因为`bgc`是涵盖padding的，所以这样使两列在相对较小的高度上看上去是一样高的

* 但是这会导致两列变得很长

**解决两列很长的问题**

* 因为我们加了`padding-bottom ：9999px`,所以外部尺寸变大了

* 我们可以添加`margin-bottom : -9999px`,让外部尺寸抵消，因为margin不影响背景，所以不会抵消背景颜色

* 父元素再设置`overflow：hidden`,以较长的子元素外部尺寸计算父元素的高度，那么较短那部分超出的`padding`也能被保留下来





### margin：auto的填充规则是什么

* 如果一侧定值，一侧 auto，则 auto 为剩余空间大小

* 如果两侧均是 auto，则平分剩余空间

  > 触发 margin:auto 计算有一个前提条件，就是 width 或 height 为 auto 时
  >
  > 元素是具有对应方向的`自动填充特性`的，所以我们不能直接垂直方向居中，因为垂直方向不是自动填充的

  > 可以利用绝对定位元素`margin:auto`居中
  >
  > 当使用`绝对定位`并设置了`top: 0; right: 0; bottom: 0; left: 0; `后，改元素的尺寸就表现为“格式化宽度和格式化高度”，尺寸自动填充父级元素的可用尺寸，此时再设置`margin:auto`即可



### border没有设置颜色的时候，颜色默认是什么

* 默认是其元素的颜色，也就是color
* 当我们hover要改变边框颜色，并且边框颜色和元素的一样的时候，那么我们每次hover后就不用修改边框颜色了，直接修改元素的颜色



### 如下一个box里面放了一张图片，为何图片下方会有缝隙？怎么解决？

![image-20220517002334885](C:\Users\accjf\AppData\Roaming\Typora\typora-user-images\image-20220517002334885.png)

* **为什么**

  * inline-block盒子前面会有个空白幽灵节点，我们用x代替这个节点看一下，如图

    ![O5Owo4.png](https://s1.ax1x.com/2022/05/17/O5Owo4.png)

  * 图片默认`verticle-align:baseline`，于是图片要与`x`的基线，也就是`x`下部对其，则自然`x`的下半行距就撑开盒子了

* **解决方法**
  
  * 图片设置为块级，可以直接干掉空白幽灵结点
  * 设置容器line-height足够小，则base-line就和bottom一样了
  * 容器的font-size足够小
  * 图片设置其他`verticle-aligign`







### flex布局，实现一个布局

```js
12345
6789
数字代表元素
```

```css
.father{
    with:100%;
    display:flex;
    align-content:flex-start;/*从起始位置排列*/
    flex-flow: row wrap;     /*主轴为行且默认换行*/
}
.son{
    flex:0,0,25%;   /*不放大，不缩小，占据25%*/
}
```

