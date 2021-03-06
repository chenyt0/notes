# Ajax技术-1 #
# 1. 案例---新用户注册时用户名冲突问题 #
##   1.1 传统模式解决方案 ##
1) 在注册页面中输入用户名和密码，点击“注册”时，要将表单数据提交给后台

![1523691565801](assets/05.png)

2) 后台PHP页面，接收用户名和密码之后，要去验证用户名是否存在，如果存在则提示用户名存在，再跳转回注册页面，重新输入。

  当用户名存在时，提示用户名已被占用，再跳转回登录页

![1523691637131](assets/06.png)

 当用户名不存在时，正常注册新用户

![1523691696235](assets/07.png)





##   1.2 ajax解决方案 ##

当光标离开用户名文本框时，就已经验证了用户名是否存在，并给予提示了。

  用户名被占用： 

![1523691892998](assets/08.png)

  用户名可用 :

![1523691866761](assets/09.png)



##   1.3 两种模式对比 ##
 传统模式： 

  两个页面 ---  前端注册表单页（index.html）  和  后端数据验证页（index.php）

 ![1524655686232](assets/10.png)

 Ajax模式 :

  两个页面 --- 前端注册表单页（index.html）  和  后端数据验证页（index.php）

![1524656343611](assets/11.png)



  Ajax的优势：没有页面跳转，刷新页面内容，用户体验提升。

​    ajax就是在页面没有刷新或者没有跳转的情况下还能更新页面的某一部分数据



# 2.ajax快速入门 #
##    2.1 ajax概述  ##
- Ajax:  Asynchronous  javascript  and  xml (异步javascript和xml)。

- ==Ajax并不是一种新技术，而是已有技术的集合。JavaScript是核心载体==。
- Ajax优势：在不刷新页面的情况下，更新页面数据，提升用户体验。
- ==Ajax就像一个小秘书==，能够实现异步工作。



##    2.2 发送Ajax请求 ##

###      2.2.1 ajax核心对象 --- XMLHttpRequest对象 ###

  历史：
	1999年诞生，微软在IE5中集成了XMLHttpRequest对象，但是并没有受到人们重视。
	2005年，google在gtalk即时聊天工具中使用了该对象，从此之后Ajax技术开始受到人们的重视。

  创建XMLHTTPRequest对象要分为(低版本) IE和==非IE两种方式(主流)==：

   IE浏览器（IE7之前） :  

​                  var xhr = new ActiveXObject('Msxml2.XMLHTTP');

   非IE浏览器（chrome、firefox、safair、搜狗等，包括IE7+之后） (主流浏览器):

​		  var xhr = new XMLHttpRequest();



案例：创建XMLhttpRequest对象，兼容IE7之前和主流浏览器

```
//创建XMLHttpRequest对象，兼容低版本IE和非IE浏览器
function getXhr () {
    var xmlhttp;

    if (window.XMLHttpRequest) {
        //IE7+ 和 非IE 中都有 XMLHttpRequest对象
        xmlhttp = new XMLHttpRequest();
    } else {
        xmlhttp = new ActiveXObject('Msxml2.XMLHTTP');
    }

    return xmlhttp;
}

alert(getXhr());
```



chrome访问结果:

![1534562204874](assets/1534562204874.png)



IE访问结果:

![1534562252947](assets/1534562252947.png)



###    2.2.2 核心方法

   XMLHttpRequest对象有了，可以发送Ajax请求了。发送请求需要两个方法:

   open(var1, var2, var3): 准备Ajax请求
     var1: 请求方式  get/post
     var2: 请求的后端程序地址
     var3: 异步(true)/同步(false)，可选参数，默认为true

   示例: xhr.open(‘get’, ‘index.php’);   //准备以get方式请求后端的index.php文件

   send(var): 发送Ajax请求
     var: 分为两种情况。 如果是get请求，则填写null。 如果是post请求，则填写要发送到后端的数据。

   示例: xhr.send(null); 



###    2.2.3 发送请求案例

 在index.html页面上创建按钮，点击该按钮时使用get方式请求后端的index.php页面

 发送Ajax请求流程:

   1) 创建XMLHttpRequest对象

   2) 调用open方法准备ajax请求

   3) 调用send方法发送ajax请求



 代码实现

   1) 创建按钮，绑定点击事件

   2) 创建XMLHttpRequest对象

   3) 调用open方法准备ajax请求

​   4) 调用send方法发送ajax请求



![1534563208094](assets/1534563208094.png)

![1534563224252](assets/1534563224252.png)



  访问结果: --- 通过newwork来确定请求是否发出

点击"btn"时，又发送了请求，请求了 index.php文件，并且正常接收到结果

![1534563287777](assets/1534563287777.png)





##    2.3 接收后端响应结果 ##

###      2.3.1 核心属性 --- readyState ###

   Ajax的整个过程有5个状态，对应readyState的5个值：0-4

​    《Pragmatic Ajax A Web 2.0 Primer 》 中对readyStae状态的介绍 

   0: (Uninitialized) the send( ) method has not yet been invoked.  

   1: (Loading) the send( ) method has been invoked, request in progress.  

   2: (Loaded) the send( ) method has completed, entire response received. 

   3: (Interactive) the response is being parsed. 

   4: (Completed) the response has been parsed, is ready for harvesting.  

   0 － （未初始化）还没有调用send()方法 

   1 － （载入）已调用send()方法，正在发送请求 

   2 － （载入完成）send()方法执行完成，已经接收到全部响应内容 

   3 － （交互）正在解析响应内容 

   4 － （完成）响应内容解析完成，可以在客户端调用了 



百度百科: 

  0 （未初始化） 	对象已建立，但是尚未初始化（尚未调用open方法）               
  1 （初始化）  	已调用send()方法，正在发送请求                      
  2 （发送数据） 	send方法调用完成，但是当前的状态及http头未知              
  3 （数据传送中）  已接收部分数据，因为响应及http头不全，这时通过responseBody和responseText获取部分数据会出现错误，
  4 （完成）   	数据接收完毕，此时可以通过通过responseBody和responseText获取完整的回应数据

 

**==最核心的重点：   4 ,  后端返回的数据已经可以在浏览器中使用了。==**





###      2.3.2  核心事件 --- onreadystatechange ###
​    onreadystatechange事件:  readyState的值每次发生变化都会触发该事件。
        0-->1    1-->2    2-->3    3-->4 总共触发4次



###     2.3.3  其他重要属性

​     responseText：以字符串形式接收后端程序的返回值。

​         以PHP为例: PHP程序最终会被解释程序一段字符串，responseText接收的就是这段字符串

​     responseXML：以XML格式接收后端程序返回值



###      2.3.4 响应案例 --- index.php ###
​     index.php：返回字符串“Hello Ajax”给前端 --- 就是  echo "Hello Ajax"

​     index.html： 将Hello Wrold 显示在页面的div中



 1) index.php 返回一个字符串（Hello Ajax！！）

![1534564764184](assets/1534564764184.png)



  2) 在index.html中检测readyState的状态，当readyState状态等于4的时候，使用responseText来接收后端返回的数据

 ![1534564786499](assets/1534564786499.png)



responseText本质是接收后端返回的字符串。



##   2.4 Ajax程序总结

  一般我们编写Ajax程序时需要两个页面，三大步骤:

![1525944330962](assets/12.png)

  两个页面:

   前端静态html页面 (php页面也行)，用来发送ajax请求，将结果渲染到页面上

   后端php页面 (jsp、asp也行)，用来接收前端请求，处理数据，并将结果返回给前端页面

 

  三大步骤:

  1) 前端静态页面发送ajax请求。

​       ① 创建 XMLHttpRequest 对象

​       ② 调用open方法准备ajax请求

​       ③ 调用send方法发送ajax请求

​       ④ 调用onreadystatechange事件，判断readyState=4时，使用responseText接收后端返回数据

  2) 后端php页面，处理请求并返回结果

  3) 前端页面接收结果，显示在网页指定位置



##   2.5 综合案例

 点击按钮，从student表中随机取出一条学生信息，显示在网页上。

 思路分析:
 1) 两个页面
   前端静态页面: student/index.html
   后端php页面: student/index.php

 ![1524658135608](assets/13.png)

 

 2) 三大步骤
  ① index.html 页面设置一个按钮，用来触发ajax请求
  ② index.php 随机取出一条学生数据，并返回给index.html页面
	$sql = "select * from student order by rand() limit 0,1";
  ③ index.html 接收到后显示在页面上



 代码实现:

 第一步骤:  index.html页面发送ajax请求

 ![1534566337714](assets/1534566337714.png)



第二步骤: 后端php页面

![1534566429341](assets/1534566429341.png)



第三步骤： index.html -- 将接收到的数据渲染到页面

![1534566508821](assets/1534566508821.png)





 关键点总结:

1) index.html 通过点击事件发送ajax请求
 ① 创建XMLHttpRequest对象
 ② 调用open方法准备ajax请求
 ③ 调用send方法发送ajax请求


**==此时不要着急将数据渲染到网页上==**。

 2) index.php 随机取出一条学生数据，并返回给index.html页面
  ① mysqli操作MySQL服务器的6步骤
  ② 核心SQL:  select * from student order by rand() limit 0,1 
  ③ 将结果拼接成字符串再输出，因为前端是以字符串形式接收的



 3) index.html接收到后显示在页面上
  ① 创建一个div标签，用来显示接收到数据
  ② 获取div对象，再将数据显示到该标签中




