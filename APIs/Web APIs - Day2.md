## Web APIs - Day2

### 01.事件中的this使用

观察以下示例代码：

```javascript
var btn = document.getElementById('btn');
btn.onclick = function () {
  btn.innerText = '修改了btn的内容';
};
```

通过事件可以发现，事件实际上是方法形式，在方法中可以使用this代表调用者(btn)。

示例中，点击事件内部修改了btn的内容，而btn等同与this，所以可以使用this在事件中替代事件源。

观察以下示例：

```javascript
// 假定页面中有多个li，要求给每个li设置点击事件，点击后打印本li的内容
var lis = document.getElementsByTagName('li');
for (var i = 0; i < lis.length; i++) {
  lis[i].onclick = function () {
    console.log(lis[i].innerText); // 报错
  };
}
```

以上写法中我们发现代码似乎是合理的，但却出现了报错，原因在于事件内i的取值有问题(原因见课上演示)。

此时可以在事件内使用this来表示事件源，方便又好用哦~

```
 var lis = document.getElementsByTagName('li');
        for (var i = 0;  i < lis.length; i++) {
            lis[i].onclick = function() {
                // console.log(i); // 我们发现i的取值为6，这个值是循环执行结束后的结果
                // console.log(lis[i].innerText);   // 报错
                console.log(this.innerText);
            };
        }

        // 实际上，循环执行过程中只是进行了事件设置，内部的代码并没有执行，意味着i不会取值。
		// 当li被点击时，循环早已执行完毕，这是获取i的结果为lis.length
        
        // 总结:
        // 1 循环添加事件时，事件内不要使用循环变量(报错)
        // 2 推荐在任意的事件内部使用this替代事件源 (统一性)
```

##### 小结：在循环添加事件时，事件中不能使用循环变量！全部使用this替代即可。// 重点

#### 01 - 1 this 小案例

```
script>
        //第一步：
        //选择用标签获取元素
        var imgs = document.getElementsByTagName('img');
        //遍历获取的元素
        for (var i = 0; i < imgs.length; i++) {
            //给每一个获取的元素添加触发事件
            imgs[i].onclick = function () {
                //body的特殊样式  document.body
                                 //地址可以理解为'url(' + imgs[i].src +')';
                                 //但是如果写imgs[i]会报错 因为当i进行触犯事件时 i的值已经循环完了
                                  //所以这里要用this 
                                 //尽量所有的都用this  他们是一样的

                    //当我们需要在一个字符串内部添加一个变量或者属性时，可以使用字符串拼接操作。
                document.body.style.backgroundImage = 'url(' + this.src + ')';
            }
        }
        
        // 总结：  字符串拼接
        // var obj = { 
        //     name: 'jack'
        // };
        
        //我们希望拼接出： '我是jack，你是谁？'; 
        //jcak部分要根据 obj.name的值决定
        //所以这里我们不能直接写死，万一更换的话这里也得跟着改动
        //此处用的就是  '' + + ''
        // console.log('我是' + obj.name + ',你是谁？');
```

### 02 取消标签默认事件

许多标签具有默认的事件效果，例如a标签，默认点击后会进行跳转。如果不希望执行跳转，可以在自定义事件代码最后设置return false。

```javascript
var link = document.getElementById('link');
link.onclick = function () {
  console.log('这是要执行的代码');
  return false; // 阻止a标签的跳转  //重点 其实就是这行代码
};
```

### 03 移入移出事件

js中的事件类型有很多，除点击外，还有鼠标的移入mouseover和移出mouseout事件

```javascript
var box = document.getElementById('box');
box.onmouseover = function () {
  console.log('鼠标移入到box中了');
};
box.onmouseout = function () {
  console.log('鼠标从box中移出了');
};
```

```
<body>
<!--父盒子-->
<div class="nodeSmall" id="node_small">
  <a href="#"></a>
  <!--二维码的盒子-->
  <div class="erweima hide fl colorBlue abc" id="er">
    <img src="images/456.png" alt=""/>
  </div>
</div>
<script>
  // 通过对父盒子的移入和移出，设置内部二维码盒子的显示与隐藏（通过类名控制）

  // 1 获取元素
  var box = document.getElementById('node_small');
  var er = document.getElementById('er');

  // 2 移入事件
  box.onmouseover = function () {
      // er.className = 'erweima show';
      // 定义一个变量接收获取的元素 因为html里的class 在DOM中是className 
      //所以此时的className就是HTML中的 class属性
      //定义一个变量，便于操作这个属性
      var oldclass = er.className;
      //此时er.className 是字符串形式，就可以采取之前学到的 
      //用replace('旧元素','新元素') 操作
      // 因为字符串样式的不可变性。 不能修改原字符串，所以要从新接收
      er.className = oldclass.replace('hide','show');
  };
  // 3 移出事件
   box.onmouseout = function () {
      // er.className = 'erweima hide';
      //定义一个变量方便于操作er.className
      var newclass = er.className;
      //此时er.className 是字符串形式，就可以采取之前学到的 
      //用replace('旧元素','新元素') 操作
      // 因为字符串样式的不可变性。不能修改原字符串，所以要从新接收
      er.className = newclass.replace('show','hide');
  };
</script>

</body>

//注意不能直接变更，这样会把其他类名也干掉，要只替换需要更换的属性即可！
```



##   兼容性

### 01 innerText的兼容性问题

innerText用于对元素进行文本内容操作，但他具有一些兼容性问题(见MDN - MDN有问题，innerText属性在ie中没有兼容性问题)。

与innerText对应的属性为textContent，textContent使用方式与innerText相同，但不支持ie678。

我们会发现现在我们有了两个功能相同的属性，虽然分别使用时不支持一部分浏览器，但组合在一起时可以涵盖所有浏览器。

这时我们就可以利用两者进行兼容性操作了。

> **兼容性操作：谁能用，就用谁。**

```
var getText = function (element) {
  if (typeof element.innerText !== 'undefined') {
    return element.innerText;
  } else {
    return element.textContent;
  }
};

		//函数功能可以分为两类, 获取型操作，设置型操作
        //获取型操作必须设置返回值。 return
        //设置型操作不需要返回值。  
```

```
<body>
    <div id="box">这是内容</div>

    <script>
        //获取元素
        var box = document.getElementById('box');
        // 不严谨的 不能用
        // // 判断结果为字符串还是undefined  兼容问题
        // //先获取元素的类型再判断
        // if (typeof box.innerText !== undefined) {
        //     console.log(box.innerText);
        // } else {
        //     console.log(box.textContent);
        // }
            /*
                功能；获取纯文本内容
                参数：需要获取内容的元素
                返回值：获取到的内容， 字符串类型
            */

        // 封装了一个函数，用于对元素进行纯文本内容获取
        var getText = function (element) {
            // 判断结果为字符串还是undefined  兼容问题
            //先获取元素的类型再判断
            if (typeof box.innerText !== undefined) {
                // console.log(box.innerText);
                return element.innerText;
            } else {
                // console.log(box.textContent);
                return element.textContent;
            }
        };


        //设置型操作   return 不需写
        var setText = function(element,value) {
            // 判断结果为字符串还是undefined  兼容问题
            //先获取元素的类型再判断
            if (typeof box.innerText !== undefined) {
                // console.log(box.innerText);
                // return element.innerText;
                element.innerText = value;
            } else {
                // console.log(box.textContent);
                // return element.textContent;
                element.textContent = value;
            }
        };
        setText(element, box);

        //函数功能可以分为两类, 获取型操作，设置型操作
        //获取型操作必须设置返回值。 return
        //设置型操作不需要返回值。  

    </script>
</body>
```

### **02 样式获取的兼容性问题**

**以前我们使用过style方式可以直接对元素的样式进行操作，但只是设置。style方式其实也可以进行样式获取，但同样只能获取行内样式。**



```
<style>
  div {
    width : 100px;
  }
</style>
<div id="box" style="height:100px;">div的内容</div>
<script>
  var box = document.getElementById('box');
  console.log(box.style.width); // '' width没有设置为行内样式
  console.log(box.style.height); // '100px' height设置为行内样式
  
  box.style.backgroundColor = 'red'; // 使用style方式设置的样式同样为行内样式，可以获取
  console.log(box.style.backgroundColor); // 'red'
</script>

老师的笔记！
```

```
<body>
    <div id="box" style="height: 100px"></div>

    <script>
        var box = document.getElementById('box');
        // // 方法的返回值是对象。如果需要操作具体的样式还需要进行属性访问！
        // //样式的值是字符串形式，有单位。

        // console.log(getComputedStyle(box).width);
        // console.log(getComputedStyle(box).height);

        //由于一个是属性，一个是函数，属性的检测方式要更稳妥
        if (box.currentStyle) {
            connsole.log(box.currentStyle.width);
        } else {
            console.log(getComputedStyle(box).width);
        }
        //两个书写方式不一样，属性 是用 点 . 连接
        //函数是先写getComputedStyle()  小括号里是获取的元素 加 .属性

        // 因为形参是局部变量 
        //所以实在的styleName输入值必须是字符串样式
        var getStyle = function (element, styleName) {
            if (box.currentStyle) {
                // connsole.log(box.currentStyle.width);  
                // 此时的 .width属性 
                //也需要改成[styleName]代表的就是[width]                 
                return box.currentStyle[styleName];
            } else {
                return getComputedStyle(box)[styleName];
            }
        };
        console.log(getStyle(box, 'width'));
    </script>
</body>
```

实际开发中，我们不可能将所有的样式均设置为行内样式。如果希望获取任意位置设置的样式，可以使用方法getComputedStyle()。

- getComputedStyle()
  - 功能：用于获取某个元素计算后(最终生效的)的样式
  - 参数：要进行样式获取的元素(DOM对象)
  - 返回值：所有样式的集合(对象，类似元素的style属性，需要再次访问某个样式名称)

```php+html
<style>
  div {
    width : 100px;
  }
</style>
<div id="box" style="height:100px;">div的内容</div>
<script>
  var box = document.getElementById('box');
  console.log(getComputedStyle(box).width); // '100px' 
  console.log(getComputedStyle(box).height); // '100px' 
</script>
```

此方法虽然好用，但是ie9以下不支持(见MDN)，对应功能为一个属性currentStyle，使用方式与getComputedStyle()相同，同样可以进行兼容性操作：

```javascript
var getStyle = function (element, styleName) {
  if (element.currentStyle) {
    return element.currentStyle[styleName];
  } else {
    return getComputedStyle(element)[styleName];
  }
}
```

### 03 根据类名获取元素

```
老师的笔记！！！！

function getByClass (leiMing, element) {
	element = element || document.body;
	if (typeof document.getElementsByClassName === 'function') {
		return element.getElementsByClassName(leiMing);
	} else {
		var resultArr = [];
		// 1 根据标签名获取element中的所有标签
		var tags = element.getElementsByTagName('*');
		// 2 检测类名是否为box
		var tempArr, j;
		for (var i = 0; i < tags.length; i++) {
			// 需要准确的检测tags[i]的className属性中是否含有box的部分
			tempArr = tags[i].className.split(' ');
			// 遍历tempArr中的每个部分是否含有box
			for (j = 0; j < tempArr.length; j++) {
				// 如果类名中含有为box的部分，将tags[i]保存到结果数组中
				if (tempArr[j] === leiMing) {
					resultArr.push(tags[i]);
					break;
				}
			}
		}
		return resultArr;
	}
}
```

```
<body>
    <div class="box">这是box</div>
    <div></div>
    <div class="box">这是box</div>
    <div class="box">这是box</div>
    <div id="text">
        <div class="box">这是text的div</div>
        <div class="box">这是text的div</div>
    </div>

    <script>
        function getByClass(cls, element) {
            // element参数表示本次查找的范围
            // element 是可选参数，需要设置默认值，默认值为body，缩小范围
            // element 和 document.body  不能更换前后位置
            element = element || document.body;

            var arr = [];
            // 1获取body中的所有标签
            var tags = element.getElementsByTagName('*');
            // 2 检测每个标签的类名，如果有box 这个类名   取出
            for (var i = 0; i < tags.length; i++) {
                //3 检测时不能直接比较，而是需要判断类名内是否含有box的部分
                //  为了检测准确，可以将类名按照空格分隔split，再依次检测
                var classArr = tags[i].className.split(' ');
                    //4检测classArr中 是否含有box，如果有取出
                    for (var j = 0; j < classArr.length; j++) {
                        if (classArr[j] === cls) {
                            arr.push(tags[i]);
                            break;
                        }
                    }
                }
                return arr;
            }
            console.log(getByClass('box'));
            var text = document.getElementById('text');
            console.log(getByClass('box',text));
    </script>
</body>
```

