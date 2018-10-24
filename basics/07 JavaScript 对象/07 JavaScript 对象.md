## 对象

### 1. 核心知识点

对象的创建

对象的操作

#### 1.为什么要学习对象【了解】

> ① 为后面JS高级课程中的 **面向对象** 编程做准备
>
> ② 在后面的课程我们会频繁去使用 **系统**提供的或者 **第三方提供**的对象帮助我们实现功能，所以前提我们必须知道 **对象的创建**以及 **对象的操作**

#### 2.类 和 对象【了解】

**类**，抽象出的**模板**。【ECMAScript6.0之前没有类的概念，但是ES6之前可以通过函数可以模拟出类，该函数被称为 **构造函数**】

> ECMAScript 核心语法   ES3.0  ES5.0  ES6.0
>
> DOM   文档对象模型
>
> BOM   浏览器对象模型

**对象**， 具体的 **实例**。

类和对象的关系：就像月饼模子 和 月饼的关系。  类是对象的模板，对象是类的一个实例。

> **小结：要创建对象，之前必须得先有模板（构造函数）**



### 2. 对象的创建（重要！）

#### 1. 创建方式【重要】

- 方式1：通过 **new**关键字调用**系统**提供 **Object**构造函数

  ```javascript
  var 变量名 = new Object();   //创建一个对象
  var 变量名 = {};             //字面量，是对new Object(); 的一个简写 推荐使用
  ```

  ​

- 方式2：通过创建并调用 **自定义构造函数**

  ```javascript
  // 自定定义的构造函数
  function 函数名(参数1, 参数2...){  // 构造函数命名首字母要大写（帕斯卡命名法）
    // this表示通过new创建的哪个当前的对象
    this.键 = 参数1;
    this.键 = 参数2;
    ...
  }

  var dx1 = new 函数名(实参,实参...);
  ```

```
 	//自定义构造函数首字母大写
    // function Hero(age,name,gender) {
    //     this.age = age;
    //     this.name = name;
    //     this.gender = gender;
    //     this.play = function() {
    //         console.log('玩游戏');
    //     };
    // }
    // var tom = new Hero(18, '小红', '女')
    // console.log(tom);
```



#### 2. 普通函数 和 构造函数的区别【了解】

> - 命名规则不一样。
>   - 普通函数，驼峰命名法
>   - 构造函数，帕斯卡命名法
> - 调用方式不一样。
>   - 普通函数，直接调用。
>   - 构造函数，需要通过 **new关键字**调用



#### 3. 系统提供的构造函数  和 自定义构造函数的区别 【了解】

> - 系统提供的构造函数创建的对象，叫做 **内置对象。【现阶段重点就是使用内置对象】**。
> - 自定义构造函数创建的对象，叫做 **自定义对象。【后面js高级会深入讲解和使用】**



#### 4. new 关键字的作用【了解】

> **作用**：通过调用构造函数创建对象
>
> **new关键字的执行过程：**
> ① 在内存中创建了一个空的Object类型的对象（看不见）
>
> ② 让this关键字指向这个空的对象（看不见）
>
> ③ 通过this给这个对象添加属性和方法（看的见）
>
> ④ 将对象 **返回给**用new关键字调用构造函数的 **调用者**(看不见)。

备注：Object在JS中是祖宗类（构造函数），所有不同类型的对象，都直接或间接的继承于它。

### 4. 对象的操作【重要】

#### 1. 对象组织数据的方式

- 对象组织数据的方式：

  > 对象组织数据的方式是： **键值对**。
  >
  > - **键**，指的是属性名或方法名，命名规范和变量名一样。
  > - **值**，指的是实际的数据。

#### 2. 设置属性和方法

- 给对象设置属性和方法：

  > - **对象名.键名 = 值;【重点】**
  >
  > - **对象名['键名'] = 值;**
  >
  > - 代码：
  >
  >   ```javascript
  >   var dog1 = {};
  >   dog1.name = '旺财'; // 属性
  >   dog1.age = 1;    // 属性
  >   dog1.call = function () {  // 方法
  >     alert(this.name + '在汪汪叫...')
  >   }
  >   // 注意，方法要用函数来表示
  >   ```

#### 3. 获取属性 和 调用方法

- 访问对象中的属性和方法：

  > - **对象.键名; 【重点】**
  >
  > - **对象[‘键名’];**
  >
  > - 代码：
  >
  >   ```javascript
  >   var dog1 = {};
  >   dog1.name = '旺财'; // 属性
  >   dog1.age = 1;    // 属性
  >   dog1.call = function () {  // 方法
  >     alert(this.name + '在汪汪叫...')
  >   }
  >   // 注意，方法要用函数来表示
  >   dog1.call(); // 调用
  >   console.log(dog1.name);
  >   console.log(dog1.age);
  >   ```

### 5. 删除属性 和 方法【了解】

- 删除对象中的属性和方法：

  > - **delete 对象.键名;  【重点】**
  >
  > - **delete 对象['键名'];**
  >
  > - 代码：
  >
  >   ```javascript
  >   var dog1 = {
  >   	name:'旺财',
  >   	age:1,
  >   	call:function(){
  >         alert(this.name + '在汪汪叫...')
  >   	}
  >   };
  >   //删除之前访问
  >   console.log(dog1.name); //旺财
  >   //删除
  >   delete dog.name;
  >   //删除之后访问
  >   console.log(do1.name); //undefiend
  >   //检测对中是否还要name属性
  >   console.log(dog1.hasOwnProperty('name'));  //false;
  >   ```

### 6. 检测属性 或 方法 【了解】

- 检测一个对象中是否存在某个属性或方法：

  > - **对象.hasOwnProperty('键名');**  // 返回boolean值，false表示不存在，true表示存在
  >
  > - 代码：
  >
  >   ```javascript
  >   var dog1 = {
  >   	name:'旺财',
  >   	age: 1,
  >   	call:function(){
  >         alert(this.name + '在汪汪叫...')
  >   	}
  >   };
  >   var r1 = do1.hasOwnProperty('age');
  >   console.log(r1); // true
  >   var r2 = do1.hasOwnProperty('gender');
  >   console.log(r2); // false
  >   var r3 = do1.hasOwnProperty('call');
  >   console.log(r3); // true
  >   var r4 = do1.hasOwnProperty('eat');
  >   console.log(r4); // false
  >   ```
  >
  >   ​

### 7. 遍历对象的成员 【了解】

- 遍历对象中的键值对

  > - 遍历方式  **for-in**
  >
  >   ```javascript
  >   for(var key in 对象){
  >     //key 是对象中的每一个键
  >     //对象[key]; 
  >   }
  >   ```
  >
  > - 代码
  >
  >   ```javascript
  >   var student1 = {
  >     name:'张三',
  >     age:17,
  >     gender:'男',
  >     scroe:100
  >   };
  >   for(var key in student1){
  >     console.log(student1[key]);
  >   }
  >   ```

### 8.检测对象的类型 【了解】

- 检测一个对象的数据类型

  > - 对象是引用数据类型，检测对象时不要用typeof去检测，要用**instanceof**
  >
  >   ```javascript
  >   对象 instanceof 构造函数名;    // 返回boolean值，true表示属于，false表示不属于
  >   ```
  >
  > - 代码
  >
  >   ```javascript
  >   /*
  >   	创建构造函数 Person
  >   */
  >   function Person(name,age,gender){
  >     this.name = name;
  >     this.age = age;
  >     this.gender = gender;
  >   }
  >   // 创建一个Person类型的对象 p1
  >   var p1 = new Person('张三',17,'男');
  >   // 检测对象p1是否属于Person
  >   console.log(p1 instanceof Person);  //true
  >   ```

### 9. 回顾

- 基本数据类型

  > 指的是 **简单的数据类型**，也叫值类型，有数字Number、字符串String、布尔Boolean、未定义Undefined、空Null。

- 引用数据类型

  > 指的是 **复杂的数据类型**， 也叫引用类型，有数组Array、函数Function、对象等。

### 10.内存中的栈和堆

注意：js中没有堆和栈，在这里只是为了理解基本数据类型和引用数据类型的区别 或 方便以后学习其他编程语言（如：C、C++、Java）![](F:\就业班\JavaScript 基础\JavaScript基础 笔记\07 JavaScript 对象\images\栈和堆.jpg)

![](F:\就业班\JavaScript 基础\JavaScript基础 笔记\07 JavaScript 对象\images\基本数据类型传递给函数的参数时.jpg)

![](F:\就业班\JavaScript 基础\JavaScript基础 笔记\07 JavaScript 对象\images\引用类型数据传递给函数的参数时.jpg)

## 本章小结

> ① 理解对象由 **属性**和 **方法**组成
>
> ② 理解对象 由 **构造函数创建**
>
> ③ 理解 **系统构造函数**  和  **自定义构造函数**的区别
>
> ④ 掌握对象的基本操作【设置、访问、删除、检测属性和方法、遍历对象成员、检测类型】
>
> ⑤ 理解基本数据类型 和 引用数据类型的区别【栈、堆、复制】
>
> ⑥ 简单类型和复杂（引用）类型的数据作为函数参数的差异

