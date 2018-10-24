## Web APIs - Day1

### 01.回顾JavaScript的组成

![](F:\就业班\02 WebAPI\WebAPI 笔记\Web APIs - Day1\images\2.png)

- ECMAScript - JavaScript的核心 （必需）

  - ECMAScript是JavaScript的核心，描述了语言的基本语法和数据类型。
  - ECMAScript是一套标准，但标准与 **具体实现** 无关。

- BOM - 浏览器对象模型 （工具）

  - 通过BOM可以操作浏览器，比如：弹框、控制台操作、浏览器跳转、获取坐标与分辨率等信息。

- DOM - 文档对象模型 （工具）

  - 通过DOM可以操作页面，DOM会将HTML看做 '文档树' ，通过DOM可以对 '树'上的 '节点' 进行操作。

  ![](F:\就业班\02 WebAPI\WebAPI 笔记\Web APIs - Day1\images\1.png)



### 02.API的概念

名词解析：API （Application Programming Interface , 应用程序编程接口）

总结：能够 **提供某种能力** 的事物，称为接口。

API ：

- 能够 **提供编程能力（让编程更方便的能力）** 的事物称为应用程序编程接口（API）
- API 实际上是 '环境' **预先提供** 的一些 **函数 (方法)**

### 03.WebAPI概念

Web API 是浏览器提供的一套 **用于操作浏览器功能和页面元素(标签)** 的方法( BOM和DOM )

- BOM ：用于操作浏览器的相关功能。

- DOM ：用于操作页面的相关功能。

- 用于API是工具，所以在学习时我们只需记忆常用的方法名称以及使用方式即可，十分简单。

  #### 学习方法

  [相关链接：MDN](https://developer.mozilla.org/zh-CN/)

  [相关链接：MDN-Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)

  #### 如何学习一个方法(封装好的函数)？（重要）

  1. 方法的功能
  2. 参数的意义和**类型**
  3. 返回值意义和**类型**
  4. **书写demo进行测试（简单练习）

### 04.DOM的概念 （重点）

文档对象模型（Document Object Model，简称DOM），用于对文档中的内容进行操作，为了方便操作，它会根据文档的内容层级自动生成 '树状模型结构'，所以DOM又被称为文档树模型（图示）。

![](F:\就业班\02 WebAPI\WebAPI 笔记\Web APIs - Day1\images\1.png)

- 文档：一个网页可以称为文档
- 页面元素：网页中的标签

### 05.DOM常用操作

#### 1.获取页面元素

##### 01.根据id获取元素

```
var div = document.getElementById('main'); //()小括号里是字符串形式的id名称
console.log(div);

// 获取到的数据类型 HTMLDivElement，对象都是有类型的
```

```
<div id = "box"></div>
  var box = document.getElementById('box');
  consolel.log（box）;
```

- 参数：id名称，字符串类型。
- 返回值：
  - 当页面中不存在对应参数id对应的标签时，返回null。
  - 当获取到对应的页面元素时，返回对应的DOM对象。

##### 注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

```
//根据id名称获取元素的特殊方式
        //<div id = "box"></div>
        
        //由于浏览器的特殊实现方式，允许用户直接使用id名称来访问元素
        //但是不是标准的方式，不推荐使用
        //console.log(box);
```

#### 2.根据标签名获取元素

```
// 获取页面中所有div：
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
} 

// 获取指定标签内部的所有div：
var box = document.getElementById('box');
var divs = box.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
} 
```

```
 //  DOM对象
        //根据标签名获取元素有两种方式
        
        //获取页面上所有的div标签数
        //还是用decument 
        // getElementsByTagName
        var divs = document.getElementsByTagName('div');
        //打印的结果是以伪数组的形式显示的
        // console.log(divs);
        for ( var i = 0; i < divs.length; i++) {
            console.log(divs[i]);
        }
        //获取一个类名中的div标签数
        var box = document.getElementById('box');
                //  获取一个类名中有多少div
                //  要用类名+getElementsByTagName
        var divs = box.getElementsByTagName('div');
        for (var i = 0; i < divs.length; i++) {
            var div = divs[i];
            console.log(div);
        }
```

详细说明：

- 参数：标签名，字符串形式，不区分大小写（强制要求统一使用小写）。
- 返回值：
  - 由获取到的所有DOM对象组成的伪数组。
  - 当没有获取到元素时，返回空数组。

**总结：**

- **getElementById() 用于获取单个元素**
- **getElementsByTagName() 用于获取多个元素**
- **注意getElementsByTagName()获取结果为伪数组**。

### 06.样式设置操作

##### 01.style样式

```
var box = document.getElementById('box');
box.style.width = '100px';
box.style.height = '100px';
// 注意 background-color 这种形式的样式在js中需要更改为驼峰命名法
// font-size 变成 fontSize .. 
box.style.backgroundColor = 'red';
```

```
 //设置样式属性
        //使用style方式设置的样式在标签的行内生效(行内样式)
        //值 是字符串类型  有单位必须带单位
        box.style.height = '100px';
        box.style.width = '100px';
        //背景颜色可以用单词，和十六进制，#000000;  包括rgb()  rgba() 都是可以用的
        box.style.backgroundColor = 'blue';
```

##### 02.类名操作

修改标签的className属性相当于直接修改标签的类名。

调用类名，直接更换标签的属性

```
var box = document.getElementById('box');
box.className = 'show';
```

```
   <style>
        .colorRed {
            width:100px;
            height: 100px;
            background-color:red;
        }
        .colorBlue {
            width:100px;
            height: 100px;
            background-color:blue;
        }
    </style>
    
    <div id="box" class="colorBlue"></div>
 	 var box = document.getElementById('box');
            //普通内嵌式类名
            //使用类名设置样式的好处,样式能重复使用，
            //js中通过元素的className属性进行操作即可
        box.className = 'colorRed';
```

### 07.文本操作

##### 1. innerHTML 和 innerText

```
var box = document.getElementById('box');
box.innerHTML = '我是文本<p>我会生成为标签</p>'; （标签会有它原本的作用）
console.log(box.innerHTML);
box.innerText = '我是文本<p>我不会生成为标签</p>';（标签也只是文本）
console.log(box.innerText);
```

```
   <div id="box">这是原始内容</div>
   var box = document.getElementById('box');
        // innerHTMl操作
        // 会生成文本,以及赋值内的标签会有它原本的作用
        // box.innerHTML = '这是文本内容<p>段落</p>';
        // console.log(box.innerHTML);

        //innerText操作
        //赋值内容里的标签不会起到标签作用,会被当成文本一样显示
        //没有标签原本的用途
        box.innerText = '这是文本内容<p>这是span</p>';
        //会把前面的内容覆盖掉
        console.log(box.innerText);
```

### 08.属性操作

##### 1. 常用标签行内属性

例如：href、title、id、src

```
var link = document.getElementById('link');
console.log(link.href);
console.log(link.title);

var pic = document.getElementById('pic');
console.log(pic.src);
```

```
  // 自带属性的修改
   var box = document.getElementById('box');
        // ID类名
        console.log(box.id);
        //ID类名更换
        box.id = 'box2';
        console.log(box.id);
        
//特殊的标签行内自带属性: class 
        //这个属性需要通过标签的className属性进行操作

        box.className = 'box2';
        console.log(box.className);   //box2

        console.log(box.class);  //undefined
```

##### 2. 标签行内自定义属性

##### 知识点：如果是自定义属性的话，必须要带date-  例如： data- haha

```
<div id="box" data-hehe="a"></div>
var box = document.getElementById('box');
// 获取行内属性：
console.log(box.getAttribute('data-hehe'));
// 设置行内属性：
box.setAttribute('data-hehe', '新内容');
// 移除行内属性：
box.removeAttribute('data-hehe');
```

### 09. 事件

事件的作用：让用户可以与网页进行交互操作（触发 - 响应 机制）

#### 事件三要素(三个组成部分)

- 事件源：(被)触发事件的元素
- 事件类型：例如 click 表示点击事件
- 事件处理程序：事件触发后要执行的代码（函数形式）

#### 事件的基本使用

注意：在使用事件时需要在事件类型名称前加on，例如点击事件为onclick

```
var box = document.getElementById('box');
box.onclick = function() {
  console.log('代码会在box被点击后执行');  
};
```

#### 注意： 在使用事件时 是 onclick  一定要写on！！！！

```
<button id="box">按钮</button>

    <script>
        var box = document.getElementById('box');
        
        //事件源.事件类型 = function() {事件触发后执行的操作}
        //点击事件类型是click 使用时是 onclick
        box.onclick = function() {
            console.log('这是按钮被点击后的效果');
        };
        
        //函数的概念:
        //函数是由事件驱动的或在调用时执行的,可重复使用的代码块。
    </script>
```

### 常用的事件类型：

- #### click 鼠标点击（单击）事件

- #### mouseover 鼠标移入事件

- #### mouseout 鼠标移出事件

### 10.小案例（开关灯）

**知识点：body标签的获取方式  document.body (body标签是唯一的。)**

```
  <style>
        .white {
            background-color: #fff;
        }
        .black {
            background-color: #000;
        }
    </style>
    
    <script>
   	 // //效果1:使用两个按钮控制效果
        // //body标签的获取方式  document.body (body标签是唯一的。)
        // //要求使用标签名获取方式操作的两个按钮
        // //1.获取元素 
        // var btns = document.getElementsByTagName('button');
        // //2.给两个标签设置事件
        // btns[0].onclick  = function () {
        //     document.body.className = 'black';
        // };
        // btns[1].onclick  = function () {
        //     document.body.className = 'white';
        // };
     //效果2:使用一个按钮控制效果
        // var 是声明变量
        var btn = document.getElementById('btn1');
        var flag = true;
        btn.onclick = function () {
            if(flag){
                document.body.className = 'black';
                btn.innerText = '变成白色';
                //为了下次进入else，所以设置为false
                flag = false;
            }else {
                document.body.className = 'white';
                btn.innerText = '变成黑色';
                //为了下次进入if，所以设置为true
                flag = true;
            }
        };
     </script>
```

