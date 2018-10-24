## 05.JavaScript函数

#### 01.概念：函数是一种方法， 功能，  功能可以反复调用

##### 作用：封装性，将执行代码封闭在一个独立的执行环境中。可以反复调用，减少代码冗余。



#### 02.函数的声明和表达式以及调用

##### 01.函数的创建

```
// 函数声明

function 函数名() {     // 函数名和变量名的命名规则规范一样 

  // 函数体

}

// 【注意】：函数创建完后，函数体中的代码不会执行，只用调用时才会执行

//调用函数

函数名();

```



##### 02.小案例

```
     //写一个函数，实现对数字数组的排序。
        // var nums = [12, 24, 44, 56, 2, 34, 53, 42,];
        // function getMp() {
        //     for(var j = 0; j < nums.length - 1; j++) {
        //         for(var i = 0; i < nums.length - 1 - j; i++) {
        //             if (nums[i] > nums[i + 1]) {
        //                 var temp = nums[i];
        //                 nums[i] = nums[i + 1];
        //                 nums[i + 1] = temp;
        //             }
        //         } 
        //     }
        //     console.log(nums);
        //     return;
        // }
        //调用函数
        // getMp();
```



#### 03.函数的参数

##### 01.为什么要有参数

```
function getSum() {
  var sum = 0;
  for (var i = 1; i <= 100; i++) {
    sum += i;
  }
  console.log();
}

// 虽然上面代码可以重复调用，但是只能计算1-100之间的值
// 如果想要计算n-m之间所有数的和，应该怎么办呢？
```

##### 02.形参和实参

- 形参，在 **函数创建时**，在小扩号中定义的标识符。
- 实参，在 **函数调用时**，在小扩号中所传入的实际的数据。

#### 04.函数的返回值

##### 01.作用：

可以终止函数的执行

可以 **将数据返回给调用者**，调用者  **可以用变量接收**函数返回的结果

##### 02.语法

```
// return 关键字，要在函数体内使用
function 函数名(形参,形参,形参) {
  //① 函数体内没有return时; 函数默认返回undefined
  //② return 数据;  //终止函数，并返回数据。
  //③ return;   //终止函数，并返回undefined
  
}
```

##### 03.返回值详解

```
如果函数没有显示的使用 return语句 ，那么函数有默认的返回值：undefined
如果函数使用 return语句，那么跟再return后面的值，就成了函数的返回值
如果函数使用 return语句，但是return后面没有任何值，那么函数的返回值也是：undefined
函数使用return语句后，这个函数会在执行完 return 语句之后停止并立即退出，也就是说return后面的所有其他代码都不会再执行。

推荐的做法是要么让函数始终都返回一个值，要么永远都不要返回值。
```

#### 05.函数是一种数据类型

```
function fn() {}
console.log(typeof fn);
```

- 函数作为参数

因为函数也是一种类型，可以把函数作为两一个函数的参数，在两一个函数中调用

- 函数做为返回值

因为函数是一种类型，所以可以把函数可以作为返回值从函数内部返回，这种用法在后面很常见。

#### 06.小案例

##### 去重

```
       function getQc() {
            var nums =[1, 2, 2, 4, 5, 1, 5, 6, 7, 8, 9, 6, 2];
            //创建一个空数组接收不等的值
            var newArray = [];
            //  遍历nums数组 
            for (var i = 0; i < nums.length; i++) {
                //创建for循环 让两个数组里面的数挨个去比较
              for (var j = 0; j < newArray.length; j++) {
                  // 比较条件是nums[0] != nums[1] 那么nums[0]就进入到新的数组中
                    //假设新数组中的数全部相同
                    var flag = false;
                  //判断条件 去比较 nums数组中的数 对应着等于 newArray数组中的数
                  if (nums[i] === newArray[j]) {
                    //假设条件为true时,跳出循环
                    flag = true;
                    break;
                  }
              }
              //要跳出上一个if语句所在的for循环
              // flag = true 取反   flag = falas;
              if(!flag) {
                      newArray[newArray.length] = nums[i];
                  }
            }
            console.log(newArray);
            return ;
        }
        getQc();
```

![](F:\就业班\01 JavaScript 基础\JavaScript基础 笔记\05 JavaScript 函数\images\js排重的一种方式.jpg)