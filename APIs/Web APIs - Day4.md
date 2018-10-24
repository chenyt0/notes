## 节点

### 节点的属性

**节点分类：**

**​	常见节点：元素节点、文本节点、属性节点**

**节点常用的属性**

- nodeType:  节点类型，数值形式	
  - **1 代表元素节点 （常用）**
  - **2 代表属性节点**
  - **3 代表文本节点**


- **nodeName: 节点名称**
  - **元素节点的nodeName为标签名**


- **nodeValue: 节点值**
  - **元素节点的nodeValue为null**

```
<body>
    <div id="box"></div>
    <script>
        var box = document.getElementById('box');
        //节点的属性 
        // 1 代表元素节点(常用)
        // 2 代表属性节点
        // 3 代表文本节点
        console.log(box.nodeType);
        // 当前元素的标签名  大写
        console.log(box.nodeName);
        //值为空  value 不是标签中所包含的内容
        console.log(box.nodeValue);
    </script>
</body>
```

### 节点访问关系

##### 节点访问关系一共分两类：上下级关系(父子关系)和同级关系(兄弟关系)。

#### 父节点

```
node.parentNode // 父节点
```

#### 子节点

#### children // 获取所有的子元素，伪数组（最常用）

```
childNodes  // 获取所有的子节点，伪数组
children // 获取所有的子元素，伪数组（最常用）
firstChild // 第一个子节点
firstElementChild // 第一个子元素节点 有兼容性问题
lastChild // 最后一个子节点
lastElementChild // 最后一个子元素节点 有兼容性问题
```

```
<body>
    <div id="box1">
        <div id="box">
            <p>这是p标签</p>
            <span>这是span</span>
        </div>
    </div>

    <script>
        var box = document.getElementById('box');
        //获取父节点
        console.log(box.parentNode);
        
        //获取所有子节点
        // 获取结果包含文本节点
        console.log(box.childNodes);
        // 获取所有子元素节点  (非常常用，必须掌握)
        console.log(box.children);

        // 第一个子节点
        console.log(box.firstChild);  //#text
        //第一个子元素节点 - ie9以下不支持
        //可以获取到内容  就是有兼容性问题
        console.log(box.firstElementChild); 
        //第一个子节点    (常用,重点记住)
        console.log(box.children[0]);

        //最后一个节点
        console.log(box.lastChild);  // #text
        //最后一个子元素节点 - ie9以下不支持
        //可以获取到内容  就是有兼容性问题
        console.log(box.lastElementChild);
        //最后一个子节点  (常用,重点记住)
        console.log(box.children[box.children.length - 1]);
        // 可以定义变量接收children的legtn  方便于操作
        var last = [box.children.length - 1];
        console.log(box.children[last]);
    </script>
</body>
```

#### 同级节点（兄弟节点）

```
nextSibling // 下一个同级节点
nextElementSibling // 下一个同级元素节点 有兼容性问题
previousSibling // 上一个同级节点
previousElementSibling // 上一个同级元素节点 有兼容性问题

//以上四个属性如果无法获取到对应节点,返回null
```

```
<body>
    <ul>
        <li id="kong">这是li1</li>
        <li id="li">这是li2</li>
        <li>这是li3</li>
        <li>这是li4</li>
    </ul>
    <script>
        var li = document.getElementById('li');
        // nextSibiling - 下一个同级节点 - 会获取到文本节点
        console.log(li.nextSibling);    // #text
        // 下一个同级元素节点  -ie9以下不支持
        console.log(li.nextElementSibling);   //可以访问到内容

        //previousSibling   -上一个同级节点  - 会获取到文本节点
        console.log(li.previousSibling);   // #text
        // 上一个同级元素节点  -ie9以下不支持
        console.log(li.previousElementSibling);

        //如果无法获取到对应节点,返回null
        console.log(kong.previousElementSibling);  //null
    </script>
</body>
```

### 移动节点

#### appendChild 追加子节点

语法：parent.appendChild(newChild)

parent：父节点（要添加到的位置）

newChild：新节点（要添加的节点）

作用：把newChild添加到parent中所有子节点的最后面。

> 如果添加的是页面中本来就存在的元素，是一个剪切的效果，原来的就不在了。

```
var demo = document.getElementById("demo");
var box = document.getElementById("box");
box.appendChild(demo);
```

```
	  btn.onclick = function() {
            //  元素的移动 从一个标签移动到另一个标签内(追加元素)
            //  默认是追加到被添加标签的所有子元素之后
            //  类名需要写被添加的元素
            box2.appendChid(text);
        }
```

#### insertBefore 插入子节点

语法：parent.insertBefore(newChild, refChild);

参数：

- parent：父节点（要添加到的位置）
- newChild：新节点（要添加的节点）
- refChild：参考节点（新节点添加到哪一个节点的前面）。

```javascript
var ul = document.getElementById("list");
var li = document.createElement("li");
li.innerHTML = "这是一个li";
// 就是添加到子节点的最前面。
ul.insertBefore(li, ul.children[0]);
```

```
btn.onclick = function () {
                    // 小括号里   第一个值是要追加的元素
                    //  第二个值是把追加元素放在哪个标签之前
            box2.insertBefore(text, span)
        }
```

### 创建元素节点（3种方式）

#### 1.document.write（基本不用）（不建议用）

可以生成新的节点，但是不推荐使用。

**注意：如果在页面加载完毕后，使用document.write进行内容写入操作，会将之前的页面给覆盖掉**

##### // 总结:不建议用（不让用）触发事件会覆盖页面所有的内容

#### 2.innerHTML

innerHTML也可以创建节点

使用innerHTML会出现的问题：

- 覆盖原内容
- 效率问题
  - console.time() 与 console.timeEnd() 的使用

```
 //好处：
        // 1可以指定位置创建元素
        // 2 创建复杂结构时非常方便(推荐使用转义符。结构不乱)
             // - 需要进行基本的字符串处理， 1. 删除换行  2 使用转义符 \
```

```
 // 缺点：
        // 1 会对内部的结构造成覆盖
        //  使用 += 的方式貌似可以解决覆盖问题，但实际上只是长得一样，并不是同一个标签
        // 影响是，如果内部元素具有事件，事件就不存在了。只存在基本结构。
      
//解决方式:(以下两种方式采用(牢记)任意一个就行)

        //   避免将innerHTML 在循环中重复使用

        //   1 字符串拼接操作
        // 测试需要多少时间
        console.time('innerHTML');
            //定义一个空字符串，接收循环里的运算
            var str = '';
            for(var i = 0; i < 1000; i++) {
                str += '<div></div>';
            }
            //  接收字符串，这样只接收依次，会节省时间 
            box.innerHTML = str;
        console.timeEnd('innerHTML');
        
        //  2 利用数组操作
        // 测试需要多少时间
        // console.time('innerHTML');
        // //定义一个空数组接收循环里的值
        // var arr = [];
        // for(var i = 0; i < 1000; i++) {
        //     //添加到数组中 arr.push(向新数组中添加元素)
        //     // 数组名.push
        //     arr.push('<div></div>')
        // } 
        //     //  把数组中的所有元素 放入一个字符串，
        //     // arr.Join('');
        // box.innerHTML = arr.join('');   
        // console.timeEnd('innerHTML');
```

#### 3.document.createElement

语法：document.createElement(tagName);

- 功能：创建一个元素节点
- 返回：元素节点（标签）
- 参数：要创建的标签的名称，字符串类型

**注意：使用document.createElement创建的元素需要添加到页面中才会显示。**

```
 // document.createElement();
        // 功能：用于创建指定的标签
        // 参数: 字符串形式的标签名
        // 特点: 使用此方式创建的元素默认不在页面上显示需要结合元素的移动功能。
        
          //时间 5ms 左右
        // 测试代码运行的时间
        console.time('createElement');
        for(var i = 0; i < 1000; i++) {
            //定义变量div 接收创建元素的div
            //小括号里需写字符串形式
            var div = document.createElement('div');
            //向页面打印div标签 小括号里直接写标签名就行
            document.body.appendChild(div);
        }
        console.timeEnd('createElement');
          // console.time();必须和 console.timeEnd();一起使用 
          //小括号的参数可		以随便起名字，两个必须一样就行，字符串形式
          // console.time();以毫秒为单位  测试代码运行时间的方法
```

##### 总结：document.write （不让用！）

#####        	innerHTML :   当要创建的结构较为复杂时，就使用innerHTML

#####         document.createElement： 除了结构复杂的情况外都可以使用

### 移除节点

语法：parent.removeChild(child);

功能：有父盒子调用，删除里面的一个子元素。

参数：child 要移除的子节点

案例：

- 模拟百度搜索框
  - 前置知识点：
    - indexOf() 数组方法
    - innerText
    - document.createElement()
    - appendChild()
    - removeChild()
- 设置表格数据删除功能（基于上一节的 “根据数据创建表格” 案例）

```
var box = document.getElementById('box');
        // 根据box 的子节点获取p标签
        var text = box.children[0];

        // 父节点.removeChild(要移除的子节点)
        // 移除子节点  小括号里写id命名~
        document.body.removeChild(text);
```

### 克隆节点

语法：node.cloneNode(deep)

功能：克隆一个节点

参数：deep

- false：默认值，表示浅复制：只会复制节点本身，不会复制节点的内部内容。
- true：深复制，会复制标签，以及标签内的所有内容 

> 1. 克隆出来的节点跟原来的节点没有关系
>
> 2. ##### 不要给要克隆的节点设置id（id是唯一的）

```

        // cloneNode()  克隆节点 
        // 只要结构上能看到的都会克隆，只是结构上的而已
        
        // 克隆节点的参数值为布尔值 false 或 true 
        //false 代表浅拷贝  只复制标签的本身，不复制内容(当前标签，不包括当里面嵌套的标签)
        //true 表示深拷贝，复制标签以及内部内容
        
        var a = document.body.appendChild(box.cloneNode(true));
        var b = document.body.appendChild(box.cloneNode(false));
        
        console.log(a,b);
```



#### 小练习：

```
<!DOCTYPE html>
<html>

<head lang="en">
  <meta charset="UTF-8">
  <title></title>
  <style>
    * {
      margin: 0;
      padding: 0
    }

    ul {
      list-style: none
    }

    .box {
      width: 600px;
      margin: 100px auto;
      border: 1px solid #000;
      padding: 20px;
    }

    textarea {
      width: 450px;
      height: 160px;
      outline: none;
      resize: none;
    }

    ul {
      width: 450px;
      padding-left: 80px;
    }

    ul li {
      /*line-height: 25px;*/
      border-bottom: 1px dashed #cccccc;
      word-break: break-all;
    }

    input {
      float: right;
    }
  </style>

</head>

<body>
  <div class="box" id="weibo">
    <span>微博发布</span>
    <textarea name="" id="txt" cols="20" rows="10"></textarea>
    <button id="btn">发布</button>
    <ul id="ul">
      <!-- 用于放置创建的li -->
    </ul>
  </div>
  <script>
    // 1 获取元素
    var btn = document.getElementById('btn');
    var txt = document.getElementById('txt');
    var ul = document.getElementById('ul');
    // 2 点击按钮，根据txt创建一个li，将li放入到ul的最前面位置
    btn.onclick = function () {
      //判断textarea 的内容为不为空， 如果为空执行if语句
      // 空字符串自动隐士转换为false 所以也可以写false 
      if (txt.value == false) {
        alert('hello world!');
      } else {
        var li = document.createElement('li');
        ul.insertBefore(li, ul.children[0]);
        li.innerText = txt.value;
        //给li中创建一个按钮
        li.innerHTML += '<input type ="button" value = "删除">';
        //设置删除功能
        li.children[0].onclick = function () {
          //删除li
          ul.removeChild(li);
        };
      }
      // 为了下次方便输入，进行内容清空
      txt.value = '';
    };
  </script>

</body>

</html>
```

