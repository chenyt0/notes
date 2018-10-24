## 内置对象

###  1.内置对象、宿主对象、自定义对象的区别？

- 内置对象

  > 系统所提供的对象如：Object、Array、Math、Date等等。

- 宿主对象

  > JS所运行的环境提供的对象比如：BOM中的Window、DOM中的document；

- 自定义对象

  > 自定义构造函数所创建的对象。

  ### 2. 如何学习内置对象？

  - 手册

    > [MDN](https://developer.mozilla.org/zh-CN/)
    >
    > W3C在线或离线手册

  - 如何学习一个对象中的方法？

    > 1. 方法的功能
    > 2. 方法的参数和类型
    > 3. 方法的返回值
    > 4. 写一个demo

  ## 3. Math 对象

  #### 01.Math 对象介绍

  **Math本身就是一个对象**， **不需要再通过构造函数去创建**，该对象中集合了很多关于数学运算的方法。也就是说，对于后期的一些复杂一些的数学运算，不需要自己动手去运算，直接调用Math对象中的方法实现即可。

  #### 02. Math对象常用属性和方法

  - Math.abs(数字);	获取一个数字的绝对值
  - Math.round(数字);   四舍五入
  - Math.PI;    π
  - Math.ceil(数字);    向上取整
  - Math.floor(数字);  向下取整
  - Math.random();    随机数(0,1之间);  (0至1之间  不包括 0 和 1)
  - Math.max(数字,数字,数字...);    求最大数
  - Math.min(数字,数字,数字...);     求最小数

  ### 4. Date 类型对象

  #### 方法1：常用！

  ```
  var 变量名 = new Date();   // 创建当前时间对象
  ```

  ```
  //当前时间
          // var date = new Date();
          // console.log(date);
          //年份
          // var year = date.getFullYear();
          // console.log(year);
          //月份  // 注意：获取月份是从0开始的 0 - 11
          // var month = date.getMonth();
          // console.log(month);
          //多少号
          // var day = date.getDate();
          // console.log(day);
          //小时
          // var hours = date.getHours();
          // console.log(hours);
          //分钟
          // var minutes = date.getMinutes();
          // console.log(minutes);
          //秒
          // var seconds = date.getSeconds();
          // console.log(seconds);
          //毫秒
          // var milliseconds = date.getMilliseconds() ;
          // console.log(milliseconds);
          //周几  // 0-6（周日0到周六6） 不能够设置，原因是周天是由今天的日期决定的。
          // var week = date.getDay();
          // console.log(week);
  ```

  #### 常用的Date类型对象方法（获取）

  ```
  日期对象.getFullYear() / 日期对象.setFullYear(数字) // 年

  日期对象.getMonth() / 日期对象.setMonth(数字)   // 月
  注意：获取月份是从0开始的

  日期对象.getDate() / 日期对象.setDate(数字)  //日

  日期对象.getHours()  /  日期对象.setHours(数字)  // 时

  日期对象.getMinutes()  /  日期对象.setMinutes(数字) // 分

  日期对象.getSeconds()  /  日期对象.setMinutes(数字) // 秒

  对象. getMilliseconds()  / 对象.setMilliseconds(数字) // 毫秒

  日期对象.getDay();   // 0-6（周日0到周六6） 不能够设置，原因是周天是由今天的日期决定的。

  //获取1970年至指定时间的 总毫秒数
  日期对象.getTime()  /  日期对象.setTime(数字); 
  ```

  ​

  #### 方法2：常用！

  语法：

  ```
  var 变量名 = new Date(stringdate);  // 创建指定的时间对象
  // 参数 stringdate, 字符串格式→ 'year-month-date hh:mm:ss'   或  'year/month/date hh:mm:ss'
  ```

  ```
  var date = new Date('2018/10/16 12:12:12');
  var date2 = new Date('2018-10-16 12:12:12');
  console.log(date);
  console.log(date2);
  ```

  #### 方式3：

  语法

  ```javascript
  var 变量名 = new Date(value);  // 创建1970年开始value毫秒后的时间对象
  // 参数 value, 数字，指的是毫秒数
  ```

  代码

  ```javascript
  var date = new Date(99999999999);
  console.log(date);
  ```

  #### 方式4：

  语法

  ```javascript
  var 变量名 = new Date(year, month[, day[, hour[, minutes[, seconds[, milliseconds]]]]]);
  // 参数 year、month、day、hour、minutes、seconds、milliseconds 都是数字，分别指的是年、月、日、时、分、秒、毫秒
  // 特别注意： month的范围是 [0-11]
  ```

  代码

  ```javascript
  var date = new Date(2018,9,16,12,12,12,12);
  console.log(date);
  ```

  ### 5.Date小案例

  ```
   	//封装一个函数,实现格式化日期

          // function getTime(date) {
          //     var year = date.getFullYear();
          //     var month = date.getMonth();
          //     var day = date.getDate();
          //     var hours = date.getHours();
          //     var minutes = date.getMinutes();
          //     var seconds = date.getSeconds();
          //     var time = year + '年' + month + '月' + day + '日' + hours + '时' + minutes + '分' + seconds + '秒';
          //     return time;
          // }
          // var date1 = new Date('2020/1/23 14:34:40')
          // var result = getTime(date1);
          // console.log(result);
  ```



###  6. Array类型对象

​	方式1：构造函数Array

```javascript
// 语法：
var 数组名 = new Array(数据,数据,数据);
// 代码：
var names = new Array('张三','李四','王五','赵六');
```

#### 方式2：数组字面量【推荐使用方式】

```javascript
// 语法：
var 数组名 = [数据,数据,数据];  // 数组字面量
// 代码：
var names = ['张三','李四','王五','赵六'];
```



### 7. 数组对象常用的方法

```

       var names = ['张三', '李四', '王五', '赵六', '张三','张三','张三'];
        console.log(names);

        //在数组前面添加元素，并返回新的长度。【原数组会发生变化】 
        names.unshift('小二','谢广坤');
        console.log(names);

        //在数组后面添加元素，并返回新的长度。【原数组会发生变化】 
        names.push('刘能');
        console.log(names);

        //删除数组的第一个元素【原数组会发生变化】
        names.shift();
        console.log(names);

        //删除数组的最后一个元素【原数组会发生变化】
        names.pop();
        console.log(names);

        //向数组添加,删除元素splice(index,howmany,item1,.....,itemX);
        //【原数组会发生变化】
       
        //在数组中删除元素
        //小括号里的第一个值是从哪开始
        //小括号里的第二个值是删除数量（几个元素）
        //前包后不包
        names.splice(1,2);
        console.log(names);

        //在索引值前面添加元素
        //第一个值是开始添加的地方的索引
        //小括号里的第二个值是删除的个数 如果是0的话可以省略不写
        names.splice(1, 0, '谢永强', '王小蒙');
        console.log(names);
        
        //替换元素
        names.splice(1, 0, '杨过');
        console.log(names);

        //查找数组中的元素存不存在。不存在返回-1
        //从索引0开始查找,正向查找
        console.log(names.indexOf('张三'));

        //从索引值最后一个倒着往前查找,反向查找
        console.log(names.lastIndexOf('张三'));

        //元素不存在,返回-1
        console.log(names.lastIndexOf('郭靖'));
```

##### **数组的反转 和 排序**

```
// 颠倒数组中元素的顺序。 【原数组会发生变化】
数组名.reverse();

// 对数组的元素进行排序 
数组名.sort();   // 默认排序顺序是根据字符串Unicode编码 【了解】

数组名.sort(function(a,b){    
  //【重点】
  return a - b;   // 升序（从小到大）
})

数组名.sort(function(a,b){    
  //【重点】
  return b - a;   // 降序（从大到小）
})
```

##### 数组截取

```
// 从已有的数组中返回选定的元素。【截取后，不会改变原数组，而是返回新的数组】
数组名.slice(start,end);  //前包后不包  开始和结束的值都是索引
```

##### 数组元素的拼接

```
// 用于把数组中的所有元素放入一个字符串。
数组名.join(separator);
```

##### 数组的其他方法【扩展】

```
// 数组遍历
//                       固定value      索引     数组名
数组名.forEach(function(value,index,currentArray){
  console.log(value);
});

// 过滤出符合筛选条件的元素，返回一个新的数组
数组名.filter(function(value,index,currentArray){
	return 条件;    // 如：return value >= 1000;
});

// 验证数组中的每一个元素是否都符合指定的条件,返回布尔值
数组名.every(function(value,index,currentArray){
  return 条件;    // 如：return value >= 1000;
});

// 验证数组中的元素，是否有符合指定条件的，返回布尔值
数组名.some(function(value,index,currentArray){
  return 条件;  // 如：return value >= 1000;
});

// 遍历数组中的每一个元素，更改后存入一个新的数组中，返回一个新的数组
数组名.map(function(value,index,currentArray){
  return 操作;   // 如：return value * 2;
});
```

##### 清空数组

```
var arr = [22,33,44,55];
// 方式1 推荐 
arr = [];
// 方式2 
arr.length = 0;
// 方式3
arr.splice(0, arr.length);
```

##### 数组的反转和冒泡

```
 //数组反转(并不是倒着遍历数组！要分清楚！！)
        var nums = [1, 22, 3, 4, 55, 6, 7];
        nums.reverse();
        console.log(nums);
        
        //数组的默认排序
        //默认排序是根据字符串的Unicode码
        nums.sort();
        console.log(nums);

        //冒泡  
        nums.sort(function(a,b){
            //升序(从小到大)
            return a - b;

           // 降序(从大到小)
            return b - a;
        });
        console.log(nums);
```

##### 数组的截取和拼接

```
var names = ['张三', '李四', '王五', '赵六', '张三'];
        //前包后不包。
        //(包括前面的数对应的元素,不包括后面的数对应的元素)
        var arr = names.slice(1,3);
        //不改变原来的数组,在新数组中显示
        console.log(names);
        console.log(arr);

        //数组元素的拼接,返回的是字符串,原数组不变
        var arr = names.join('|');
        console.log(arr);

```



### 8.数据结构-栈和队列（了解）

栈

- 特点：先进后出-FILO（**F**irst **I**n **L**ast **O**ut）电梯
- 代码：

```
var userNames = [];
// 先进
console.log(userNames); // []
userNames.push('张三');
console.log(userNames); // ["张三"]
userNames.push('李四');
console.log(userNames); // ["张三", "李四"]
userNames.push('王五');
console.log(userNames); // ["张三", "李四", "王五"]

// 后出
userNames.pop();   
console.log(userNames); // ["张三", "李四"]
userNames.pop();   
console.log(userNames); // ["张三"]
userNames.pop();       
console.log(userNames); // []
```

队列

- 特点：先进先出-FIFO（ **F**irst  **I**n  **F**irst  **O**ut）排队买票
- 代码：

```
var userNames = [];
// 先进
console.log(userNames); // []
userNames.push('张三');
console.log(userNames); // ["张三"]
userNames.push('李四');
console.log(userNames); // ["张三", "李四"]
userNames.push('王五');
console.log(userNames); // ["张三", "李四", "王五"]

// 先出出
userNames.shift();   
console.log(userNames); // ["李四", "王五"]
userNames.shift();   
console.log(userNames); // ["王五"]
userNames.shift();       
console.log(userNames); // []
```

### 9. String字符串对象

#####  1.字符串的不可变性【了解】

```
var str = 'abc';
str = 'hello';
// 当重新给str赋值的时候，数据'abc'不会被修改，依然在内存中
// 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
// 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
```

```
//字符串的不可变性
        var str = 'abc';
        console.log(str);
        str = 'hello';
        console.log(str);
        //总结: 重新给字符串赋值时.数据不会被修改,依然存在内存中
        //会重新再内存中开辟空间。 特点:字符串的不可变性
```



#### 2. 基本包装对象【了解】

```
// 普通字符串
var str = 'abc';   // 普通字符串不是对象
var len = str.length; // 但是为什么可以像对象一样使用点出东西？
alert(len); //3

//把字符串包装成对象 → 基本包装类型
var strObj = new String('abc');  // 把字符串包装成对象
var len = strObj.length;  // 因为是对象，所以可以点出东西。
alert(len); //3
```

```
 // 字符串的基本包装对象
        var str = 'abc';   //普通的字符串不是对象
        var len = str.length 
        //当字符串加上.length后会变成对象
        console.log(len);
```

```
//把字符串包装成对象  →  基本包装类型
                    //  String  首字母要大写,否则会报错
        var strObj = new String('abc');  //把字符串包装成对象
        var len = strObj.length; // 因为是对象,所以可以点出东西
        console.log(len);
```

#### 3. 字符串对象常用的方法

##### 字符串转对象以后每个字符都代表一个索引，即使是字母数字也不例外

##### 字符串所有的方法，都 **不会修改字符串本身**(字符串是不可变的)，操作完成会 **返回一个新的字符串**

##### 获取字符串中的单个字符

```javascript
字符串.charAt(index);
字符串[index];      // 推荐使用   //中括号里是字符串的索引值
字符串[索引值]；   //中括号里是字符串的索引值
```

##### 字符串的拼接 和 截取

```javascript
// 拼接
字符串.concat(str1,str2,str3...);
拼接符 +     //推荐使用

// 截取
字符串.slice(start,end); //小括号里是字符串的索引，前包后不包
```

##### 查询字符是否在字符串中存在

```javascript
字符串.indexOf();  //小阔号里是字符串的值，不是索引 
字符串.lastIndexOf();  //小阔号里是字符串的值，不是索引 反向查询 从字符串最后一个值往前
```

##### 去除空白符(去出字符串左右两边的空格，不包括中间的)

```javascript
字符串.trim();  // 去除字符串两边的空格  //小括号里不需要输入值
```

字母字符大小写转换

```javascript
字符串.toUpperCase(); 	// 转换大写 重点   //小括号里不需要输入值
字符串.toLowerCase(); 	// 转换小写 重点   //小括号里不需要输入值
```

##### 字符串替换

```javascript
字符串.replace(oldStr, newstr);  //小括号里的是字符串的值，不是索引 //只替换一次
	//	var str = '搜狗输入法';
    //  var str1 =str.replace('搜狗','百度');
    //  console.log(str1);
```

字符串分割

```javascript
字符串.split(sp);  // 把一个字符串分割成字符串数组。
		var str = '搜i狗i输i入i法';
        var str1 = str.split('i');
        console.log(str1);   // ["搜", "狗", "输", "入", "法"]
```

### 本节小结

> 1. 学会查用MDN文档 或 离线手册 学习内置对象的属性 或 方法。
> 2. 理解什么是包装对象
> 3. 掌握使用字符串常用的方法操作字符串