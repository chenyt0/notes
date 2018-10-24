## 注册事件的两种方式

#### on+事件名称

> onclick、onmouseover这种on+事件名称的方式注册事件几乎所有的浏览器都支持。

注册事件：

```javascript
box.onclick = function(){
	//事件处理程序	
}
```

移除事件：

```javascript
box.onclick = null;	
```

on+事件名称注册事件的缺点：

同一个元素同一类型的事件，只能注册一个，如果注册了多个，会出现覆盖问题。

```
 <script>
        var btn = document.getElementById('btn');
        // 使用普通方式设置的事件会出现覆盖的问题
        //如下情况 第二个事件的代码就会把第一个事件的代码给覆盖掉
        //只显示自己本身的事件
        btn.onclick = function() {
            console.log('这是第一个事件代码');
        };
        btn.onclick = function() {
            console.log('这是第二个事件代码');
        }; 
        //普通事件的移除方式:
        // 值为null时会移除掉该按钮上的事件
        btn.onclick = null;
    </script>
```

##### on+事件名称注册事件的缺点：

##### 同一个元素同一类型的事件，只能注册一个，如果注册了多个，会出现覆盖问题。

### 注册事件的新方式

#### addEventListener与removeEventListener

##### 现代浏览器支持的注册事件的新方式，这种方式注册的事件不会出现覆盖问题。

##### addEventListener的语法

```
//第一个参数：事件类型：click mouseover
//第二个参数：事件处理程序
//第三个参数：false 
DOM对象.addEventListener(type, func, useCapture);
```

```
  // 添加事件监听
        // 参数: 1
        // 事件的类型名称,不加on,字符串形式。
        // 例如:onclick 在参数中 就应该是 'click'
        // 2 事件处理程序, 函数
        
  //特点: 多次进行设置操作,不会出现覆盖问题
        // addEventListener直接加小括号 没有等号！！
        //小括号中用逗号隔开，第一个参数是字符串形式
        btn.addEventListener('click',function(){
            console.log('这是点击事件1');
        });
```

#### 注意：如果想要让你注册的事件能够移除，不能使用匿名函数。

```
function fn1() {
    alert("hehe");
}
//如果想让注册的事件能移除，不能用匿名函数。
box.addEventListener("click", fn1, false);
```

removeEventListen的语法

```javascript
//第一个参数：事件类型
//第二个参数：事件处理程序
//第三个参数：false
removeEventListener(type, func, useCapture);
```

```
//定义变量接收函数体
        var fun = function() {
            console.log('这是点击事件2');
        };
        btn.addEventListener('click',fun);

        //移除事件操作:
        // 元素.removeEventListener();
        //移除时必须与设置时的参数完全一样
        //(事件处理程序必须设置为命名形式，不能再是匿名函数)

        btn.removeEventListener('click',fun)
```

**attachEvent与detachEvent**

> IE678不支持addEventListener与removeEventListen两个方法，但是支持attachEvent与detachEvent

attachEvent的用法：

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:事件处理程序
attachEvent(type, func)
```

detachEvent的用法

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:事件处理程序
detachEvent(type, func)
```

```
<script>
        var btn = document.getElementById('btn');
        
        //addEventListener组功能在ie9以下不支持

        // ie中 提供了一组方法用于进行事件操作

        //下面的一组方法虽然是ie提出的,但是ie的新版本11已经不支持了,主要学习的是上面一组功能

        //这组方法作为了解即可
        //书写方式和addEventListener 要注意第一个参数需要加on
        // 例如 click事件  写参数的时候需要写 onclick
        //如果有要移除的事件  必须得保证参数完全相同 (定义变量接收函数更简单明了一点)
        //1 添加事件
        btn.attachEvent('onclick',function(){
            console.log('这是第一个点击事件');
        });
        
        var fun = function() {
            console.log('这是第二个点击事件');
        };
        btn.addachEvent('onclick',fun);

        //2 移除事件：必须保证参数完全相同
        btn.detachEvent('onclick', fun);


        //总结:  了解即可。ie出的，ie11版本都已经不在支持了
    </script>
```

### 事件流

> 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡。

说白了就是：当我们触发了子元素的某个事件后，父元素对应的事件也会触发。

通常情况，事件冒泡对于我们来说是没有问题的，我们直接不管就行了，但是如果当事件冒泡给我们带来影响的时候，我们需要阻止事件冒泡。

> 阻止事件冒泡有浏览器兼容性问题

正常浏览器：

```javascript
link.onclick = function (event) {
    event = event || window.event;
    //stop :停止  propagation：传播
    event.stopPropagation();
}
```

```
// 通过演示我们发现，事件默认会进行传递。
		// 这种默认的传递方式称为事件冒泡，传递的顺序为由内向外。
		// 具体说明：某个元素触发事件后默认会进行事件冒泡，将事件传递给父元素，如果父元素具有相同类型的事件，会进行触发操作，后续操作以此类推。

		// 小结：当前我们需要掌握的是：1 事件冒泡是默认的事件传递方式  2 执行顺序
```

#### 事件捕获（了解）

> 事件捕获是火狐浏览器提出来的，IE678不支持事件捕获（基本上，我们都是用事件冒泡）
> 事件的处理将从DOM层次的根开始，而不是从触发事件的目标元素开始，事件被从目标元素的所有祖先元素依次往下传递

```javascript
//当addEventListener第三个参数为true时，表示事件捕获
arr[i].addEventListener("click", function () {
    console.log(this);
},true);
```

```
		// 小结：当前我们需要掌握的是：
		//1 事件冒泡是默认的事件传递方式  2 执行顺序
		
		//另一种事件传递方式
		// 事件捕获
		// 参数是布尔值类型  true 和  false
		// 默认是false 冒泡顺序   由内向外(子到父)
		//  true    与冒泡顺序相反  由外向内 (父到子)  
		
		//这种传递方式没有使用场景，只需要掌握基本概念(设置方式，执行顺序) 了解即可！
		
		//设置事件捕获  把addEventListener（）小括号中第三个参数设置为true即可。默认为false，事件冒泡
```

####  结论：元素是否设置了事件与事件是否可以触发是无关的 !

#### 事件的三个阶段

1. 事件的捕获阶段
2. 事件的目标阶段（触发自己的事件）
3. 事件的冒泡阶段

事件有三个阶段，首先发生的是捕获阶段，然后是目标阶段，最后才是冒泡阶段，对于捕获和冒泡，我们只能干预其中的一个，通常来说，我们可能会干预事件冒泡阶段，而不去干预事件捕获阶段

```
//任意的元素触发事件后都会经历3个阶段，依次为
        // 1 捕获阶段  (由外向内)     人过来
        // 2 当前目标阶段(执行阶段)   人在做事
        // 3 冒泡阶段  （由内向外）   人走

        //我们设置的事件冒泡或事件捕获只是决定了某个事件在哪个阶段会被执行

```

#### 常见的事件

> 常见的鼠标事件

**onmousedown**:鼠标按下事件

onmouseup:鼠标弹起事件

onclick:单击事件

ondblclick：双击事件

onmouseover：鼠标经过事件

onmouseout：鼠标离开事件

onmousemove：鼠标移动事件

onfocus：鼠标获得焦点事件

onblur：鼠标失去焦点事件



> 常见的键盘事件

onkeydown:键盘按下时触发

onkeyup:键盘弹起时触发



> 对于鼠标事件，事件对象中有一系列的XY记录了鼠标的位置信息。而键盘事件中，事件对象有一个event.keyCode属性，记录了按下去的键的键盘码

### 事件对象的概述

##### 概念: 保存了事件的一些信息的对象称为事件对象

> 在触发某个事件的时候，都会产生一个事件对象Event，这个对象中包含所有与事件相关的一些信息，包括触发事件的元素，事件的类型以及其他与事件相关的信息。

鼠标事件触发时，事件对象中会包含鼠标的位置信息。

键盘事件触发时，事件对象中会包含按下的键相关的信息。

```javascript
每一个事件在触发时，都会产生一个事件对象。
你见或者不见，我就在那里，不悲不喜。
你爱或者不爱，爱就在那里，不增不减。
你用或者不用，我都会给你，不离不弃。 
```

### 获取事件对象

> 既然事件对象中存储了这么多的信息，我们首先需要做的就是获取到这个事件对象。获取事件对象的时候，存在浏览器的兼容问题。



对于现代浏览器，获取事件对象非常的简单，只需要在注册事件的时候，指定一个形参即可。这个形参就是我们想要获取到的事件对象。

```javascript
btn.onclick = function(event){
    //event就是事件对象，里面包含了事件触发时的一些信息。
	console.log(event);
}

```



对于IE678来说，获取事件对象则是另一种方式，在事件里面，通过window.event来获取事件对象

```javascript
btn.onclick = function(){
	//IE678通过window.event获取事件对象
	var event = window.event;
	console.log(event);
}
```

兼容性封装

```javascript
btn.onclick = function(event){
  	//只要用到了事件对象，就要记得处理浏览器兼容性
	event = event || window.event;
}

```

```
<script>
        var btn = document.getElementById('btn');

        // 当我们进行事件触发后，某些特殊的信息是我们自己无法得到的(坐标等信息)
        //js的事件会给我们提供这些信息,我们只需要利用某些方式得到后进行使用即可。
        //由于得到的数据是一组值，为对象结构，所以也成为事件对象
        
        //接收的方式(兼容性问题)
        // 1在事件处理程序的形参位置接收一个参数，这种方式ie9以下不支持
        // 2 在ie9以下可以使用一个window.event对象进行操作

        //event对象进行操作 
        // 形参可以是任意命名的变量 
        // 此时形参的e是event的缩写，因为形参是变量，所以可以任意设置，符合标准就可以
        btn.onclick = function(e) {
            //兼容性操作
            //利用函数的参数默认值的设置方式对事件对象的获取进行兼容性操作 
            //&& 见false 即false
            //|| 见true  即为true
            e = e || window.event;

            // 事件对象中具有许多属性，我们掌握对应的含义和用法就可以
            //事件对象具有一个type属性，表示当前事件的类型名称(例如：click，mouseover等)

            console.log(e);
            //检测事件的属性是什么
            console.log(e.type);
        };

        //例如：我们可以利用这个type属性实现对一个元素的多个事件的统一管理
        //对type属性的使用演示。(了解)
        var fun = function(e){
            //兼容性操作
            e = e || window.event;
            //根据e的type属性检测当前事件的类型
            if(e.type === 'click') {
                consoel.log('点击事件功能');
            } else if(e.type === 'mouseover'){
                console.log('点击移入功能');
            }
        };
        
        btn.omclick = fun;
        btn.onmouseover = fun;
        btn.onmouseout = fun;
    </script>
```

### 事件对象的常用属性

> 事件对象中有很多很多的属性，但是很多属性并不常用。我们经常用到的是***鼠标位置信息*** 和***键盘码***  相关的信息。

记录了鼠标位置信息的相关属性

```javascript
clientX与clientY：光标相对于可视区左上角的水平位置和垂直位置。
pageX与pageY：光标相对于网页（文档document）左上角的水平位置与垂直位置（推荐使用）
```

```
        var box = document.getElementById('box');
        //鼠标跟随移动 mousemove
        // mousemove - 鼠标移动时触发事件
        // 在页面任意位置点击鼠标时,获取鼠标坐标,将元素box移动到点击位置

        document.onmousemove = function(e) {
            // console.log(e.clientX, e.clientY);
            //设置样式属性
            //距离可视窗口左侧的坐标  X轴
            // 观察打印出来的坐标是纯数值,所以这里要字符串拼接单位
            var x = box.style.left = e.clientX + 'px';
            //距离可视窗口上侧的坐标  Y轴
            var y = box.style.top = e.clientY + 'px';
            console.log(x,y);     
        }; 
        
        // 总结:
        //注意  X，Y 要大写
        // clientX: 针对页面可视区域的横坐标
        // clientY: 针对页面可视区域的纵坐标
        //  clientX，clientY，打印出的是纯数值  注意！！！
        // 需要单位的话需要字符串拼接 例如: clientX + 'px';
```



记录了键盘码的属性

```javascript
event.keyCode:键盘按下的那个键的键盘码
```

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		#box {
			width: 200px;
			height: 300px;
			border: 1px solid #000;
		}
	</style>
</head>
<body>
	<div id="box">
		<span>这是span</span>
		<p>这是box中原始的p标签</p>
		<p>这是box中原始的p标签</p>
		<p>这是box中原始的p标签</p>
		<div class="text">这是类名为text的div</div>
		<div class="text">这是类名为text的div</div>
	</div>
	<button id="btn">按钮</button>
	<script>
		// 需求：给box中的所有p标签设置点击事件
		var box = document.getElementById('box');
		var btn = document.getElementById('btn');
		var ps = box.children;

		// 点击按钮后，向box内部动态创建p标签
		btn.onclick = function () {
			var p = document.createElement('p');
			p.innerText = '这是新创建的p标签';
			box.appendChild(p);
		};

		// 问题：动态创建的元素无法使用页面加载过程中设置的事件。
		// for(var i = 0; i < ps.length; i++) {
		// 	ps[i].onclick = function() {
		// 		console.log('这是p标签');
		// 	};
		// }
		// 发现内部的任意元素点击后均会事件冒泡,一定会触发父元素box的点击事件。
		//新方式虽然可以让任意p标签具有事情,但同时其他的一些元素也可以使用。
        box.onclick = function(e) {
            // 兼容性操作
            e = e || window.event;
	
			//能够触发这个事件的元素有很多,但我们只需要内部的p标签
			// 需要获取到当前触发事件的元素,检测是不是P标签。
			// 1 事件对象的target属性用于获取真正触发事件的元素    console.log(e.target);s
			// 2 检测当前元素是否满足规则，(此处的意思是  它是不是p标签)
			// 事件对象的target属性用于获取真正触发事件的元素

            //   因为nodeName获取的标签名为大写 
            // 所以此处设置标签名需要大写
            if(e.target.nodeName === 'P') {
                console.log('这是p标签');
            } else if(e.target.nodeName === 'SPAN') {
                console.log('这是span标签');
            } else if (e.target.className === 'text') {
                console.log('这是类名为text的元素功能');
            }
        };

        // 事件对象的target属性用于获取真正触发事件的元素


		// 这种设置方式称为事件委托：
		//   概念：将内部元素的事件设置给父级元素（将内部元素的事件委托给父级元素设置）。
		//   作用：
		// 	1 可以解决动态创建的元素没有事件的问题
		//	2 可以减少事件的设置个数，对内部元素的事件进行统一管理
	</script>
</body>
</html>

```

### 事件委托

##### 概念：将内部元素的事件设置给父级元素（将内部元素的事件委托给父级元素设置）

### offset系列属性

```
	<script>
		var box = document.getElementById('box');
		// offsetLeft 和 offsetTop
		// offsetLeft用于获取当前元素到定位父盒子的左侧距离
		//   offsetLeft的结果是数值类型，只读
		/*console.log(box.offsetLeft);
		// box.offsetLeft = 500;
		console.log(box.offsetLeft);*/

		// offsetHeight 和 offsetWidth
		// offsetHeight表示元素的真实高度（除了margin以外的高度）
		// console.log(box.offsetHeight);

		// offsetParent - 用于获取当前元素外的定位父盒子 (了解)
		console.log(box.offsetParent);
	</script>

```

