## 表单属性与事件

#### 表单的常用属性

##### 内容示例如下：

```
 // 基本语法：
        //有value就用value
        // input (输入框) textarea(文本域)

        // 打印原内容: console.log(类名.value);
        // 修改原内容方法： 类名.value = '新内容';

        //下拉菜单select  取值的时候可以用value
        // 修改的时候不能用value 得用 innerHTML 或 innerText
        // 打印原内容: console.log(类名.value);
        //修改原内容方法： 类名.innerHTML = '';

        //button不可以用value值,  可以用innerHTML 或 innerText
        // 打印原内容: console.log(类名.innerHTML);
        //修改原内容方法： 类名.innerHTML = '';
```

#### 内容操作

```
<body>                             
                             <!-- 清除输入框自带的四条边 -->
    <input type="text" value="请输入文本" id="text" style="border: 0 none">
    <br><br>
                          <!--清除文本域的拖动功能 -->
    <textarea id="txt" style="resize:none" >这是文本域</textarea>
    <br><br>
    <select name="">
        <option value="" id="opt">1</option>
    </select>
    <br><br>
    <button id="btn" value="">内容</button>

    <script>
        var text = document.getElementById('text');
        var txt = document.getElementById('txt');
        var opt = document.getElementById('opt');
        var btn = document.getElementById('btn');
    
        // value值修改输入框内容  
        console.log(text.value);
        text.value = '我是新的内容';

        //表单域用value值，可以用innerHTML
        // console.log(txt.innerHTML);
        console.log(txt.value);
        txt.value = '新的文本域内容';

        //下拉菜单select  取值的时候可以用value
        // 修改的时候不能用value 得用 innerHTML 或 innerText
        opt.value = '我是value的内容';
        opt.innerHTML = '新的value的内容';

        //button不可以用value值,  可以用innerHTML 或 innerText
        console.log(btn.innerHTML);
        btn.innerHTML = '这是新的内容';


        // 总结: 有value值的要用value值
        // 用value值的控件 input textarea
        // button 按钮 不能用value值
        // select 下拉菜单 可以用value取值，但是不能修改内容，
        //修改内容需要用 innerHTML 或 innerText
    </script>
</body>
```

#### 下拉菜单选中属性

```
// 下拉菜单
<body>
    <select>
        <option>张三</option>
        <option id="lisi">李四</option>
        <option>王五</option>
    </select>
    <button id="btn">选中李四</button>
    <script>
        btn.onclick = function () {
            //selected 下拉菜单选项选中
            // 同样是布尔值类型，true为选中,false为取消选中
            // 如果不是布尔值, 会自动隐士转换
            lisi.selected = true;
        };
    </script>
</body>
```

#### 禁用属性（了解）

```
<body>
    <input type="text" id="ipt" value="输入框">
    <button id="btn">按钮</button>
    <script>
        // 当点击按钮式 输入框就会禁止输入内容
        btn.onclick = function () {
            // 同样是布尔值， true为禁用  false为取消禁用
            //如果不是布尔值  自动隐士转换
            ipt.disabled = true;
        };
    </script>
</body>
```

### 输入框常用事件

##### // 获取光标焦点:  类名.onfocus,// 失去焦点事件:  类名.onblur

```
<script>
        var ipt = document.getElementById('ipt');
        var txt = document.getElementById('txt');
        //获取焦点事件  onfocus
        ipt.onfocus = function () {
            //检测 如果内容为默认提示词 去除
            if (this.value === '我是新的输入框内容') {
                this.value = '';
            }
        };
        ipt.onblur = function () {
            if (this.value === '') {
                this.value = '我是新的输入框内容';
                //鼠标移开之后会重新赋值
            }
        };
    </script>
```