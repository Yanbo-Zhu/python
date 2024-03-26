## 第十一章   前端开发

### 11.1   如何创建html文件

HTML的定义：超文本标记语言

- 字体标签：h1-h6/b/strong/i/em/u

- 超链接标签a标签中的href属性的作用：
  - 链接到一个新的地址
  - 回到顶部或指定位置
  - 跳转邮箱
  - 下载文件
  
- 标签也成为标记：
  - 双闭合标签<html></html>
  - 单闭合标签<meta charset='utf-8'>
  
- head标签
  - meta基本网站元信息标签
  - title网站的标题
  - link链接css文件
  - script内嵌样式
  
- body标签
  - h1-h6标题标签
  - p标签 段落标签
  - div标签
    - 称为盒子标签，division：分割，把网页分割成不同的独立的逻辑区域
  - span标签
    - 用于对文档中的行内元素进行组合，小区域标签，在不影响文本正常显示的情况下，单独设置对应的样式
  
  ```html
  <style>
      span.active{
          font-weight:bold;
      }
  </style>
  <p>
      <span class='active'>标题</span>内容
  </p>
  ```
  
  - lable标签
    - 它中的for属性跟表单控件的id属性有关联
  - a anchor 锚点 超链接标签
    - href 链接的网址
    - title鼠标悬浮上的标题
    - style行内样式
    - target目标
      - 默认是_self在当前页面中打开新的链接
      - _blank在新的空白页面打开新的链接
    - img
      - src链接的图片资源
      - title标题
      - style
      - alt 图片加载失败的时候显示文本
    - ul无序列表
      - li
    - ol有序列表
      - li
    - table列表
    - form标签中的action属性和method属性的作用
      - action：提交到服务器的地址，如果是空的字符串，它表示当前服务器地址
      - method：提交的方式。get和post
        - get：明文不安全，地址栏值允许提交2kb的内容，提交的内容会在地址栏显示，
        - post：密文提交安全，可以提交任意内容
        - 后期要把http协议的内容看下
    - form表单
      - input
        - type控件的类型
          - text文本输入框
          - password密码框
          - radio单选框
          - checkbox多选框
        - name
          - 名称 提交服务器的键值对的name
        - value
          - 值 提交服务器的键值对的value
      - select name multiple：多选框
        - option value
      - textarea 
        - name
        - value
        - cols
        - rows
    - html特征
      - 对换行和空格不敏感
      - 空白折叠
  
- 在一行内显示的标签有：

```html
a/span/b/strong/e/i
不可用设置宽高，在一行内显示
```

- 行内块标签：

```html
input/img   可以设置宽高  在一行内显示
```

- 独占一行的标签有块级标签：

```html
h1-h6/ul/ol/li/form/table/tr/p/div
可以设置宽高，若果不设置宽度，默认是父级标签的100%宽度，独占一行
```

```python
<p>段落内容</p>
<a href="网址" target="_self">显示内容</a> #_slef在当前页显示，_blank跳转到新页面
<h3 style="background-color:yellow;">
    <a href="网址" style="text-decoration:none;color:red; " title="小圆圈">显示名</a>
</h3>#title是当鼠标放到目标不点进去时显示的悬浮名称
```

```python
<img src="http://www.bbra.cn/UploadFiles/imgs/2018/01/mm1/001.jpg" alt="校花" width="200">#src=图片地址 alt是在图片加载不出来时候显示的内容，width是显示宽度
<u>显示内容带下划线</u>
<strong>加粗</strong>
<em>显示内容斜体</em>
<i>显示内容斜体</i>
```

- 列表

```python
<h3>有序列表</h3>#有顺序有序号
    <ol type="">#默认为空时序号从1开始，可以是i，a,A
        <li>python</li>
        <li>web前端</li>
        <li>java</li>
        <li>linux</li>
    </ol>
```

```python
<h3>无序列表</h3>
<ul type="cricle">#可以是cricle、square默认圆
        <li>
            <a href="" title="假的">小米手机</a>
        </li>
        <li>女神</li>
        <li>太白</li>
        <li>mjj</li>
        <li>江老板</li>
    </ul>
```

- 表格

```python
<table border="1" cellspacing="0" width="90%">#border环绕包边 cellspacing 单元格间距 width表格布满页面比例
        <tr>#table row 表格行
            <td>id</td>
            <td>name</td>
            <td>age</td>
            <td>sex</td>
        </tr>
        <tr>
            <td>1</td>
            <td>沛齐</td>
            <td>19</td>
            <td>女</td>
        </tr>
        <tr>
            <td>2</td>
            <td>女神</td>
            <td>18</td>
            <td>男</td>
        </tr>
    </table>
```

- 单选

```python
<h4>单选框</h4>#radio 单选
<p>
    <input type="radio" name="sex" checked = 'checked'>男
    <input type="radio" name="sex">女
 </p>#checked 为默认选择项可有值可无值 name=相同内容产生互斥效果，只能选一个
```

- 多选

```python
<h4>我的爱好：</h4>#checkbox 多选
<p>
    <input type="checkbox" name="a" value="抽烟"> 抽烟
    <input type="checkbox" name="b" value="喝酒"> 喝酒
    <input type="checkbox" name="c" value="烫头"> 汤头
</p>
```

- 下拉列表

```python
<h4>下拉列表</h4>
    <p>
        <select name="fav" multiple>#mutiple倍数，可多选，不加则默认单选
            <option value="smoke">抽烟</option>
            <option value="drink" selected>喝酒</option>
            <option value="tangtou">烫头</option>
        </select>
    </p>
```

- 时间选择框

```python
</p>#date是日期，不带时刻，datetime-local带时刻
<input type="datetime-local">
<p>
```

- form表格输入框

```python
<p>#cosl垂直分割窗口，表格宽度，rows表示行的宽度
	<textarea name="" id="" cols="30" rows="1"></textarea>
</p>
```

- 提交按钮

```python
<p>#若默认不写value的话则显示提交，若赋值value是什么名字就显示什么
	<input type="submit" value="登录">
</p>
```

```python
body{background-color:red}#显示背景颜色
```

### 11.2   css选择器

css 层叠样式表 cascading style sheets

- css选择器的作用：选中标签

- 基础选择器
  - id选择器
    - 唯一的（#xxx）
  - 类选择器
    - 可以重复，归类，类也可以设置多个
    - 语法：（.xxx）

```html
<style>
  .box{
    width:200px;
    height:200px;
    background-color:yellow;
 }
  .active{
    border-radius: 200px;
 }
</style>
<div class='box active'></div>
<div class='box'></div>
<div class='box'></div>
```

- 标签选择器

```html
div{}
p{}
ul
ol...
```

- 高级选择器

  - 后代选择器

  ```html
  div p{color:red}
  ```

  - 子代选择器

  ```html
  div>p{colo:red}
  ```

  - 组合选择器
  
  ```html
  div,p,body,html,ul,ol...{
      padding:0
      margin:0
  }
  ```
  
  - 交集选择器
  
  ```html
  div.activ{}
  ```
  
- 属性选择器：层叠性和继承性

  - 继承性：在css有某些属性是可以继承下来，color，text，-xxx，line-height，font-xxx是可以继承下来，权重比较规则：继承来的属性权重为0
  - 前提是选中了标签，权重比较：
    - 1.选择器数量：id 类 标签 谁大他的优先级越高，如果一样大，后面的会覆盖掉前面的属性。
    - 2.选中的标签的属性优先级用大于继承来的属性，他们没有可比性
    - 3.同时继承来的属性
      - 谁描述的近谁的优先级高
      - 描述的一样的近，这个时候才回归到选择器的数量

- css的盒模型

  - width：内容宽度  height：内容的高度 padding：内边距，边框到内容的距离  border：边框   margin：外边距

- css引入方式

  - 行内样式

  ```html
  <div style='color:red;'>
      mjj
  </div>
  ```

  - 内嵌式

  ```html
  在head标签内部书写style
  <style>代码
  </style>
  ```

  - 外接式

  ```html
  <link href='css/index.css' rel='stylesheet'>
  ```

  - 三种引入方式的优先级：行内样式》内嵌式和外接式（内嵌式和外接式要看谁在后面，在后面的优先级高）

- css中可以继承的属性：color，text-xxx，font-xxx，line-height，letter-spacing，word-spacing

- HTML的嵌套关系

```html
<!--块级标签：1.独占一行 2.可以设置宽度，如果不设置宽，默认就是父标签的100%宽度-->
<!--行内标签：1.在一行内显示 2.可以不设置宽度，如果不设置宽度，默认是字体的大小   块内标签：1.在一行内显示 2.可以设置宽度>
在网页中：行内砖块和行内块是经常使用的
dispaly:
	inline
	inline-block
	block
嵌套关系：
1.块级标签可以嵌套块级和行内以及行内块
2.行内标签尽量不要嵌套块级
3.p标签不要嵌套div，也不要嵌套p，可以嵌套a/img/表单控件
```



```html
<stlye>
    div{
    width:200px;
    heigth:60px;
    background-color:red;
    text-align:center;
    line-height:60px;
    }
</stlye>
<div>
    name
</div>
#让行高等于盒模型的高度实现垂直居中，使用text-align:center；实现文本水平居中
```

清除a标签下下划线

```html
text-decoration:none
nong:无线
underline：下划线
overline：上划线
line-through：删除线
```

重置网页样式：reset.css

```html
html,body,p,ul,ol{
margin:0;
padding:0;
}
/*通配符*/
*{
margin:0;
padding:0;
}
a{
text-decoration:none;
}
input,textarea{
border:none;
outline:none;
}
```

### 11.3   伪类选择器/属性选择器/伪元素选择器

- 伪类选择器
- 对于a标签，如果想设置a标签的样式，要作用于a标签上，对于继承性来说，a标签不起作用的，“爱恨准则”，LoVe HAte

```html
/*LoVe HAte*/
/*a标签没有被访问时候设置的属性*/
a:link{
    /*color: red;*/
}
/*a标签被访问时候设置的属性*/
a:visited{
    color:yellow;
}
/*a标签悬浮时设置的属性*/
a:hover{
    color: deeppink;
}
/*a标签被摁住的时候设置的属性*/
a:active{
    color: deepskyblue;
}
```

- 属性选择器

```html
input[type='text']{
    background-color: red;
}
input[type='checkbox']{
}
input[type='submit']{

}
```

- 伪元素选择器

```css
p::first-letter{
    color: red;
    font-size: 20px;
    font-weight: bold;
}
p::before{
    content:'@';
}
/*解决浮动布局常用的一种方法*/
p::after{
    /*通过伪元素添加的内容为行内元素*/
    content:'$';
}yun
```

- 设置网页字体及备选字体

```css
font-family:'宋体','楷体';
```

- 设置文字间距和英文单词间距

```css
文字间距:letter-spacing
英文单词间距:word-spacing
```

- 字体加粗使用哪些属性

```css
font-weight:lighter| normal | bold |bolder| 100~900 字体加粗
font-style:italic;/*斜体*/
```

- 文本修饰用哪个属性

```css
text-decoration:none| underline | overline | line-through
```

- px em rem单位 首行缩进可以用em

```css
px: 绝对单位  固定不变的尺寸
em和rem :相对单位     font-size
	em:相对于当前的盒子
	rem:相对于根元素（html）
```

- 让盒子水平居中

```css
盒子必须有宽度和高度，再设置margin: 0 auto;
让文本水平居中： text-align:center;
让文本垂直居中：line-height = height
```

- 让两个盒子并排一行上显示

```css
1.float浮动属性
2.设置盒子的显示方式 display:inline | inline-block;
```

- 简单阐述浮动对盒子产生了什么现象

```css
1.脱离标准文档流，不在页面上占位置 “脱标”
2.文字环绕 设置浮动属性的初衷
3.“贴边” 现象： 给盒子设置了浮动，会找浮动盒子的边，如果找不到浮动盒子的边，会贴到父元素的边，如果找到了，就会贴到浮动盒子的边上
4.收缩效果
 有点像 一个块级元素转成行内块
```

- 盒子模型
  - margin：在水平方向上不会出问题，垂直方向上会出现塌陷问题

### 11.4   盒子浮动

浮动的应用：布局方案实现元素并排

浮动现象：脱离了标准文档流，不在页面上占位置；贴边现象；收缩效果。

浮动带来的问题：不能撑起父盒子的高度

- 清除浮动的四种方式：

```css
给父元素添加固定高度 （不灵活，后期不易维护）
可以用在一直不会发生改变的导航栏
```

```css
内墙法：给最后一个浮动元素的后面添加一个空的块级标签，并且设置该标签的属性为clear:both;
问题：冗余
clear的作用是不允许某一侧有浮动元素
```

```css
伪元素清除法 推荐大家使用
.clearfix::after{
    content:'';
    display: block;
    clear: both;
    /*visibility: hidden;*/
    /*height: 0;*/
}
```

```css
overflow:hidden; 常用

因为overflow:hidden;会形成BFC区域，形成BFC区域之后，内部有它的布局规则
计算BFC的高度时，浮动元素也参与计算
但是小心overflow：hidden它自己的本意
```

### 11.5   定位

定位

```css
position:static | relative | absolute | fixed;
		 静态      相对        绝对        固定
```

- 相对定位 relative
  - 特征：
    - 与标准文档流下的盒子没有任何区别
    - 留‘坑’，会影响页面布局
  - 作用：做‘子绝父相’布局方案的参考
  - 参考点：以原来的盒子做参考点
- 绝对定位 absolute
  - 参考点
  - 如果单独设置一个盒子为绝对定位，以top描述，他的参考点是以body的（0,0）为参考点，以bottom描述，他的参考点是以浏览器的左下角为参考点。
  - 子绝父相：以最近的父辈元素的左上角为参考点进行定位
  - 特征：1.脱标 2.压盖 3.子绝父相

- 固定定位

```css
1.脱标
2.固定不变
3.提高层级
参考点：以浏览器的左上角作为参考点
```

只适用于定位的元素 z-index:auto

```css
z-index只能应用在定位的元素，默认z-index:auto;
z-index取值为整数，数值越大，它的层级越高
如果元素设置了定位，没有设置z-index，那么谁写在最后面的，表示谁的层级越高。(与标签的结构有关系)
从父现象。通常布局方案我们采用子绝父相，比较的是父元素的z-index值，哪个父元素的z-index值越大，表示子元素的层级越高。
```

background背景

```css
/*设置背景图*/
background-image: url("xiaohua.jpg");
background-repeat: no-repeat;
/*调整背景图的位置*/
background-position: -164px -106px;
```

border

```css
border-radius 设置圆角或者圆
```

阴影box-shadow

```css
box-shadow: 水平距离 垂直距离 模糊程度 阴影颜色 inset
```

行内的水平和垂直居中

第一种line-height+text-align

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        p{
            width: 200px;
            height: 200px;
            background: #666;
            color:#fff;
            line-height: 200px;
            text-align: center;
        }
    </style>
</head>
<body>
    <p>
        MJJ
    </p>
</body>
</html
```

第二种 给父元素设置display:table-cell,并设置vertical-align:middle

```css
div{
    position: relative;
    width: 200px;
    height: 200px;
    background: #666;
    color:#fff;
    text-align: center;
    display: table-cell;
    vertical-align: middle;
}
```

块的水平和垂直居中

方法：position+margin

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .father{
            width: 200px;
            height: 200px;
            background-color: red;
            position: relative;
        }
        .child{
            position: absolute;
            width: 100px;
            height: 100px;
            background-color: green;
            margin: auto;
            left:0;
            right: 0;
            top: 0;
            bottom: 0;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="child">我是个居中的盒子</div>
    </div>
</body>
</html>
```

方法二：display:table-cell

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .father{
            width: 200px;
            height: 200px;
            background-color: red;
            display: table-cell;
            vertical-align: middle;
            text-align: center;
        }
        .child{
            width: 100px;
            height: 100px;
            background-color: green;
            display: inline-block;
            vertical-align: middle;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="child">我是个居中的盒子</div>
    </div>
</body>
</html>
```

第三种：纯position

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .father{
            width: 200px;
            height: 200px;
            background-color: red;
            position: relative;
        }
        .child{
            width: 100px;
            height: 100px;
            background-color: green;
            position: absolute;
            left: 50%;
            top: 50%;
            margin-left: -50px;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="child">我是个居中的盒子</div>
    </div>
</body>
</html>
```

### 11.6   JavaScript核心编程

- 变量名的命名
  - 必须字母、下划线或美元符号开始
  - 可以使用任意多个英文字符、数字、下划线或美元符号组成
  - 不能使用JavaScript关键字和JavaScript保留字来进行命名
  - 严格区分大小写
- 变量类型
  - 基本数据类型
    - number数值
    - string字符串
    - boolean布尔
    - undefined未定义
    - null空
  - 引用数据类型
    - Array数组
    - Object对象
    - Function函数

11.6.1   在页面中插入JavaScript

- 内部JavaScript
  - 使用<style>元素向html嵌入内部样式

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script type="text/javascript">
    //编写Javascript代码
</script>
</body>
</html>
//<script type="text/javascript">表示在<script></script>之间的是文本类型(text),javascript是为了告诉浏览器里面的文本是属于JavaScript语言。
```

- 外部JavaScript
  - html文件所在目录下创建script.js的新文件之后再script.js内编写

```js
<script src="script.js" async></script>
```

11.6.2   数学、字符串相关

- 函数

```js
1.创建方法
（1）普通函数
   function fn(){
       
   }
   fn();
(2)函数表达式
  var fn = function(){}
  
 (3) 自执行函数
 ;(function(){
    this指向 一定是指向window
 })()

全局作用域下，函数作用域，自执行函数都指向了window,函数作用域中this指向可以发生改变，可以使用call()或者apply()


var obj = {name：'mjj'};
function fn(){
    console.log(this.name);
}
fn();//是空值，因为函数内部this指向了window
fn.call(obj)//此时函数内部的this指向了obj


作用： 解决冗余性代码，为了封装


构造函数
new Object();
new Array();
new String();
new Number();


//使用构造函数来创建对象
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);

//es6用class来创建对象
class Person{
    constructor(x,y){
        this.x = x;
        this.y = y
    }
    toString(){
        
    }
    
}
var p = new Person();
```



- 递增和递减运算符

```js
<script>
    var a = 4;
	var b = a ++;//此处后a=5 b=4
    var c = ++a;//此处后a=6 c=6
    console.log(b);
	console.log(c);
	console.log(a);
</script>
```

- 字符串拼接与格式化

```js
<script>
    var name = 'wusir', age = 28;
    var str = name + '今年是' + age + '岁了，快要结婚了，娶了个黑姑娘';
    console.log(str);
    //    es6的模板字符串 ``
    var str2 = `${name}今年是${age}岁了，快要结婚了，娶了个黑姑娘`;
    console.log(str2);
</script>
```

- 字符串的常用方法

```js
slice() 切片，有一个参数，从当前位置切到最后，两个参数，顾头不顾尾
substring()
substr() 如果有两个参数，第二个参数表示切字符串的个数

拼接字符串
concat() 返回新的字符串
+
es6的模板字符串
``  插入变量用${变量名}

//获取索引
indexOf()
lastIndexOf()

//获取字符
charAt()
//获取字符的ASCII码
charCodeAt()


//转大写
toUppercase()
//转小写
tolowercase()


typeof 校验当前变量的数据类型

trim() 清除左右的空格
```

- 数组

```js
var arr  = [1,'2','mjj'];
    //解释器 遇到var声明的变量 会把var声明的变量提升到全局作用域下
    var i;
    var c;
    for(i = 0;i < arr.length;i++){
        console.log(arr[i]);
    }
    function fn(){
        var d = 4;
    }
    console.log(i,c);
</script>
```

- 数组的常用方法

```js
toString()
join('*')
concat()

//栈方法 后进先出
push()
pop()

//堆方法 先进先出
unshift()
shift()


splice(起始位置，删除的个数，添加的元素)； 对数组的增加，删除，替换
slice()
reverse()
sort()


//迭代方法
for
forEach() 仅能在数组对象中使用
在函数中arguments 这个对象是伪数组
```

- 流程控制

```js
var arr  = [1,'2','mjj'];
    var weather = prompt('请输入今天的天气');
    switch (weather) {
        case '晴天':
            console.log('可以去打篮球');
            break;
        case '下雨':
            console.log('可以睡觉');
            break;
        default:
            console.log('学习');
            break;
    }
</script>
```

- 赋值运算符，逻辑运算符==与===

```js
var arr  = [1,'2','mjj'];
    var a = 2;
    var b = '2';
    console.log(a == b);//比较的是值
    console.log(a === b); //比较是值和数据类型
</script>
$$  and
||  or
!   not
i++  加1
```

- 循环

```js
<script>
    var arr = [8,9,0];
    //1.初始化循环变量  2.循环条件  3.更新循环变量
    for(var i = 0;i < arr.length; i++){
        console.log(arr[i]);
    }

//    1到100之间的数
//     while
    var a = 1;
    while(a <= 100){
        console.log(a);
        a+=1;
    }
</script>
```

- 函数和三元运算

```js
<script>
    function fn() {
        switch (arguments.length) {
            case 2:
                console.log('2个参数')
                break;
            case 3:
                console.log('3个参数')
                break;
            default:
                break;
        }
    }
    fn(2, 3);
    fn(2, 3, 4);
    fn(2, 3, 4, 6);
//三元运算
1 > 3 ? 'true' : 'false';
</script>
```

- 创建对象object

```js
<script>
    //1.字面量创建方式
    var obj = {};
    obj.name = 'mjj';
    obj.fav = function(){
        //obj
        console.log(this);
    };
    obj.fav();
   //点语法 set 和get
    console.log(obj.name);

    //构造函数
    var obj2 = new Object();
    console.log(obj2);
    obj2.name = 'wusir';
	class Person{
        constructor(name,age){
            //初始化
            this.name = name;
            this.age = age;
        }
        fav(){
            console.log(this.name);
        }
        showName(){

        }
    }
    var p = new Person('mjj',18);
    p.fav();
</script>
```

- 数组array的常用方法

```js
<script>
        //1,判断当前数组是否为数组，返回值是true,则证明是数组

        var num = 123;
        var arr = ['red','green','yellow'];
        console.log(Array.isArray(arr));
        console.log(arr.toString());//red,green,yellow
        console.log(num.toString());
        console.log(typeof num.toString());
        console.log(arr.join('^'));
        console.log(arr.push('purple')); //返回了数组的最新的长度
        console.log(arr);
        console.log(arr.pop());//返回删除的内容
        console.log(arr);
        // 往数组的第一项上添加内容
        console.log(arr.unshift('gray','black'));//返回数组的最新长度
        console.log(arr);
        console.log(arr.shift());//删除第一项
        console.log(arr);
        //
        var names = ['女神','wusir','太白'];
        // names.splice(); //对数组进行添加，删除，替换操作
        // name.slice(1); //对数组进行分割
        for(var i = 0; i < names.length; i++){
            names[i];
        }
        names.forEach(function (index,item) {
            console.log(index);
            console.log(item);
        });
        function  fn(a,b) {
            //arguments.length //代指的实参的个数
            //arguments它不是一个数组，它被称为叫伪数组
            console.log(arguments);
            for(var i = 0; i < arguments.length; i++){
                console.log(arguments[i]);
            }
        }
        fn(2,3,4);
        console.log(fn.length);//形参的个数

        var  str = '            mjj          '


    </script>
```

- 日期对象

```js
<script>
    var date = new Date();
    console.log(date);
    console.log(date.getDate());
    console.log(date.getMonth()+1);
    console.log(date.getFullYear());
    console.log(date.getDay());
    console.log(date.getHours());
    console.log(date.getMinutes());
    console.log(date.getSeconds());

    console.log(date.toLocaleString());
    /*var weeks = ['星期天','星期一','星期二','星期三','星期四','星期五','星期六'];
    console.log(weeks[date.getDay()]);
    var day = weeks[date.getDay()];
    document.write(`<a href="#">${day}</a>`);*/

    var a =  1 < 2 ? "yes": "no";
    console.log(a);

</script>
```

- 数字时钟案例

```js
<h2 id="time"></h2>
<script>
    var timeObj = document.getElementById('time');
    console.log(time);

    function getNowTime() {
        var time = new Date();
        var hour = time.getHours();
        var minute = time.getMinutes();
        var second = time.getSeconds();
        var temp = "" + ((hour > 12) ? hour - 12 : hour);
        if (hour == 0) {
            temp = "12";
        }
        temp += ((minute < 10) ? ":0" : ":") + minute;
        temp += ((second < 10) ? ":0" : ":") + second;
        temp += (hour >= 12) ? " P.M." : " A.M.";
        timeObj.innerText = temp;
    }

    setInterval(getNowTime, 20)//设置20毫秒刷新异形词
</script>
```

- window对象

```js
<script>
    var name = 'mjj';
    console.log(window);
    console.log(window.name);
</script>
```

- math对象

```js
<script>
    var obj = {name:'mjj'};
    function add() {
        console.log(this.name);
    }
    // add();
    // add.call(obj);
    // add.apply(obj,[]);
    //求最大值和最小值
    var values = [1,2,36,23,43,3,41];
    var max = Math.max.apply(null,values);
    console.log(max);
    var a = 1.49999999;
    console.log(Math.ceil(a));//天花板函数
    console.log(Math.floor(a))//地板函数
    console.log(Math.round(a))//四舍五入
//    随机数
    console.log(Math.random());
//    min~  max
    //0.113131313
    function random(min,max) {
       return min+Math.floor(Math.random()*(max-min))
    }
    console.log(random(100, 400));
//    rgb(237,100,10)
</script>
```

### 11.7   BOE  Browser Object Model

- 系统对话框方法
  - alert()弹出警示框
  - confirm()弹出警示框确认返回true，取消返回false
  - prompt()弹出警示框可以输入内容

```js
<script type="text/javascript">
    window.alert('mjj');
    var a = window.confirm('你确定要删除?');
    console.log(a); 
    var weather = window.prompt('今天天气如何??');
    console.log(weather);
</script>
```

- 一次性任务setTimeout()
  - setTimeout()方法表示一次性定时任务做某件事情，他接收两个参数，第一个参数为执行的函数，第二个参数为时间（毫秒计时：1000毫秒=1秒）

```js
<script type="text/javascript">
    window.setTimeout(function(){
    console.log('mjj');
},2000)
console.log('xiongdada');
</script>
```

- 周期性循环setInterval()
  - setInterval()方法表示周期性循环的定时任务，他接收的参数与setTimeout()方法相同

```js
var num = 0;
var timer = null;
timer = setInterval(function(){
    num++;
    if (num > 5) {
        clearInterval(timer);
        return;
    }
    console.log('num:'+ num);
},1000);
//clearInterval()用来清除当前的定时任务
```

### 11.8   location对象的属性和方法

- location.href跳转到页面
- location.replace跳转页面不会产生历史记录

```js
//跳转到网址会有记录
<script type="text/javascript">
    setTimeout(function(){
    location.href = 'https://www.baidu.com';
},3000)
</script>
//跳转到网址不会有历史记录
<script type="text/javascript">
    setTimeout(function(){
    location.replace = 'https://www.baidu.com';
},3000)
</script>
```

- reload()方法
  
- 它的作用是重新加载当前显示的页面,如果调用 reload() 时不传递任何参数，页面就会以最有效的方式重新加载。也就是说，如果页面自上次请求以来并没有改 变过，页面就会从浏览器缓存中重新加载。如果要强制从服务器重新加载，则需要像下面这样为该方法 传递参数 true
  
- ```js
  location.reload();//重新加载(有可能从缓存中加载)
  location.reload(true);//重新加载(强制从服务器加载)
  ```

### 11.9   DOM  Document Object Model文档对象模型

- 获取节点对象的方式

```js
document.getElementById();
document.getElementsByTagName();
document.getElementsByClassName();
```

- 对样式操作

```js
box.style.color
box.style.backgroundColor
box.style.width
....
```

- 对属性设置

```js
setAttribute(name,value);
getAttribute(name);
```

- 事件

```js
onclick
onmouseover()
onmouseout()

onfocus当用户在输入框时
onblur当用户离开输入框时
```

### 11.10    jQuery插件库

- jQuery是一个快速，小巧，功能丰富的JavaScript库。它通过易于使用的API在大量浏览器中运行，使得HTML文档遍历和操作，事件处理，动画和Ajax变得更加简单。通过多功能性和可扩展性的结合，jQuery改变了数百万人编写JavaScript的方式。操作: 获取节点元素对象，属性操作，样式操作，类名，节点的创建，删除，添加，替换。jquery核心：write less,do more
- jQuery对象转换js对象
  - $('button')[0]
- js对象转换jQuery对象
  - $(js对象)
- jQuery的选择器
  - 基础选择器
  - 高级选择器
  - 属性选择器
  - 基本过滤选择器
    - :eq()选择一个 索引从0开始
    - :first 获取第一个
    - :last 获取最后一个
    - :odd  获取奇数
    - :even  获取偶数
  - 过滤的方法
    - .eq()
    - .children() 获取儿子
    - .find() 获取后代
    - .parent() 获取父级对象
    - .siblings() 获取除他之外的同级元素
  - 动画
    - 普通动画：
      - show()
      - hide()
      - toggle()
    - 卷帘门动画
      - slideDown()
      - slideUp()
      - slideToggle()
    - 淡入淡出效果
      - fadeIn()
      - fadeOut()
      - fadeToggle()
    - 自定义动画
      - .animate({parems},speed,callback)
  - 样式操作
    - 通过调用.css()方法，如果传入一个参数，看一下这个参数如果是一个字符串表示获取值，如果是对象，表示设置多少属性值，如果是两个参数，设置单个属性值
  - 类操作
    - addClass()
    - removeClass()
    - toggleClass()
  - 对属性操作
    - attr(name,value); 设置属性
    - removeAttr(name);删除属性

### 11.11   jQuery的属性操作

文档加载后激活函数

```js
$(document).ready(function(){
  $(".btn1").click(function(){
    $("p").slideToggle();
  });
});
```

jquery的属性操作模块分为四个部分：html属性操作，dom属性操作，类样式操作和值操作

- html属性操作：是对html文档中的属性进行读取，设置和移除操作。比如attr()、removeAttr()
- DOM属性操作：对DOM元素的属性进行读取，设置和移除操作。比如prop()、removeProp()
- 类样式操作：是指对DOM属性className进行添加，移除操作。比如addClass()、removeClass()、toggleClass()
- 值操作：是对DOM属性value进行读取和设置操作。比如html()、text()、val()

设置属性值或者返回被选元素而的属性值attr()

```js
//获取值：attr()设置一个属性值的时候 只是获取值
        var id = $('div').attr('id')
        console.log(id)
        var cla = $('div').attr('class')
        console.log(cla)
        //设置值
        //1.设置一个值 设置div的class为box
        $('div').attr('class','box')
        //2.设置多个值，参数为对象，键值对存储
        $('div').attr({name:'hahaha',class:'happy'})
```

移除属性removeAttr()

```js
//删除单个属性
$('#box').removeAttr('name');
$('#box').removeAttr('class');

//删除多个属性
$('#box').removeAttr('name class');
```

prop()方法设置或返回被选元素的属性和值，当该方法用于返回属性值时，则返回第一个匹配元素的值，当该方法用于设置属性值时，则为匹配元素集合设置一个或多个属性/值对。语法：

返回属性值：

```js
$(selector).prop(property)
```

设置属性和值：

```js
$(selector).prop(property,value)
```

设置多个属性和值：

```js
$(selector).prop({property:value, property:value,...})
```

关于attr()和prop()的区别

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    男<input type="radio" id='test' name="sex"  checked/>
    女<input type="radio" id='test2' name="sex" />
    <button>提交</button>
    <script type="text/javascript" src="jquery-3.3.1.js"></script>
    <script type="text/javascript">
        $(function(){
            //获取第一个input
            var el = $('input').first();
            //undefined  因为attr是获取的这个对象属性节点的值，很显然此时没有这个属性节点，自然输出undefined
            console.log(el.attr('style'));
            // 输出CSSStyleDeclaration对象，对于一个DOM对象，是具有原生的style对象属性的，所以输出了style对象
            console.log(el.prop('style'));
            console.log(document.getElementById('test').style);
            $('button').click(function(){
                alert(el.prop("checked") ? "男":"女");
            })
        })
    </script>
    
</body>
</html>
```

什么时候使用attr()，什么时候使用prop()？

- 当有true，false两个属性使用prop()；
- 其他使用attr();

addClass(添加多个类名)

为每个匹配的元素添加指定的类名。

```js
$('div').addClass("box");//追加一个类名到原有的类名
```

还可以为匹配的元素添加多个类名

```js
$('div').addClass("box box2");//追加多个类名
```

removeClass 

- 从所有匹配的元素中删除全部或指定的类

- 移除指定的类（一个或多个）

  ```js
  $('div').removeClass('box')；
  ```

- 移除全部的类

  ```js
  $('div').removeClass();
  ```

- 可以通过添加删除类名，来实现元素的显示隐藏

  ```js
  var tag  = false;
          $('span').click(function(){
              if(tag){
                  $('span').removeClass('active')
                  tag=false;
              }else{
                  $('span').addClass('active')
                  tag=true;
              }    
  })
  ```

  ```js
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title></title>
      <style type="text/css">
          .active{
              color: red;
          }
      </style>
  </head>
  <body>
       <ul>
           <li class="item">张三</li>
           <li class="item">李四</li>
           <li class="item">王五</li>
       </ul>
       <script type="text/javascript" src="jquery-3.3.1.js"></script>
       <script type="text/javascript">
           $(function(){
  
               $('ul li').click(function(){
                   // this指的是当前点击的DOM对象 ,使用$(this)转化jquery对象
                   $(this).addClass('active').siblings('li').removeClass('active');
               })
           })
       </script>
      
  </body>
  </html>
  ```

toggleClass 像开关

如果存在就删除，不存在就删除，语法：toggleClass('box')

```js
$('span').click(function(){
    //动态的切换class类名为active
    $(this).toggleClass('active')
})
```

html 获取值

语法：html()是获取选中标签元素中的所有的内容

```js
$('#box').html();
```

设置值：设置该元素的所有内容会替换掉标签中原来的内容

```js
$('#box').html('<a href="https://www.baidu.com">百度一下</a>');
```

text 获取值

语法：text()获取匹配元素包含的文本内容

```js
$('#box').text();
```

设置值：设置该所有的文本内容

```js
$('#box').text('<a href="https://www.baidu.com">百度一下</a>');
注意：值为标签的时候 不会被渲染为标签元素 只会被当做值渲染到浏览器中
```

val  获取值

val()用于表单控件中获取值，比如input textarea select等

```js
$('input').val('设置了表单控件中的值')；
```



## 第十二章   djiango框架

### 12.0  http协议

- http协议简介

超文本传输协议（英文：Hyper Text Transfer Protocol，HTTP）是一种用于分布式、协作式和超媒体信息系统的应用层协议。HTTP是万维网的数据通信的基础。HTTP有很多应用，但最著名的是用于web浏览器和web服务器之间的双工通信。

- http协议概述

HTTP是一个客户端终端（用户）和服务器端（网站）请求和应答的标准（TCP）。通过使用网页浏览器、网络爬虫或者其它的工具，客户端发起一个HTTP请求到服务器上指定端口（默认端口为80）。我们称这个客户端为用户代理程序（user agent）。应答的服务器上存储着一些资源，比如HTML文件和图像。我们称这个应答服务器为源服务器（origin server）。在用户代理和源服务器中间可能存在多个“中间层”，比如代理服务器、网关或者隧道（tunnel）。

尽管TCP/IP协议是互联网上最流行的应用，HTTP协议中，并没有规定必须使用它或它支持的层。事实上，HTTP可以在任何互联网协议上，或其他网络上实现。HTTP假定其下层协议提供可靠的传输。因此，任何能够提供这种保证的协议都可以被其使用。因此也就是其在TCP/IP协议族使用TCP作为其传输层。

通常，由HTTP客户端发起一个请求，创建一个到服务器指定端口（默认是80端口）的TCP连接。HTTP服务器则在那个端口监听客户端的请求。一旦收到请求，服务器会向客户端返回一个状态，比如"HTTP/1.1 200 OK"，以及返回的内容，如请求的文件、错误消息、或者其它信息。

- http协议工作原理

HTTP协议定义Web客户端如何从Web服务器请求Web页面，以及服务器如何把Web页面传送给客户端。HTTP协议采用了请求/响应模型。客户端向服务器发送一个请求报文，请求报文包含请求的方法、URL、协议版本、请求头部和请求数据。服务器以一个状态行作为响应，响应的内容包括协议的版本、成功或者错误代码、服务器信息、响应头部和响应数据。

以下是 HTTP 请求/响应的步骤：

1. 客户端连接到Web服务器
一个HTTP客户端，通常是浏览器，与Web服务器的HTTP端口（默认为80）建立一个TCP套接字连接。例如，http://www.luffycity.com。

2. 发送HTTP请求
通过TCP套接字，客户端向Web服务器发送一个文本的请求报文，一个请求报文由请求行、请求头部、空行和请求数据4部分组成。

3. 服务器接受请求并返回HTTP响应
Web服务器解析请求，定位请求资源。服务器将资源复本写到TCP套接字，由客户端读取。一个响应由状态行、响应头部、空行和响应数据4部分组成。

4. 释放连接TCP连接
若connection 模式为close，则服务器主动关闭TCP连接，客户端被动关闭连接，释放TCP连接;若connection 模式为keepalive，则该连接会保持一段时间，在该时间内可以继续接收请求;

5. 客户端浏览器解析HTML内容
客户端浏览器首先解析状态行，查看表明请求是否成功的状态代码。然后解析每一个响应头，响应头告知以下为若干字节的HTML文档和文档的字符集。客户端浏览器读取响应数据HTML，根据HTML的语法对其进行格式化，并在浏览器窗口中显示。

在浏览器地址栏键入URL，按下回车之后会经历以下流程：

浏览器向 DNS 服务器请求解析该 URL 中的域名所对应的 IP 地址;
解析出 IP 地址后，根据该 IP 地址和默认端口 80，和服务器建立TCP连接;
浏览器发出读取文件(URL 中域名后面部分对应的文件)的HTTP 请求，该请求报文作为 TCP 三次握手的第三个报文的数据发送给服务器;
服务器对浏览器请求作出响应，并把对应的 html 文本发送给浏览器;
释放 TCP连接;
浏览器将该 html 文本并显示内容;

- http请求方法:HTTP/1.1协议中共定义了八种方法（也叫“动作”）来以不同方式操作指定的资源

```python
get
向指定的资源发出“显示”请求。使用GET方法应该只用在读取数据，而不应当被用于产生“副作用”的操作中，例如在Web Application中。其中一个原因是GET可能会被网络蜘蛛等随意访问。
HEAD
与GET方法一样，都是向服务器发出指定资源的请求。只不过服务器将不传回资源的本文部分。它的好处在于，使用这个方法可以在不必传输全部内容的情况下，就可以获取其中“关于该资源的信息”（元信息或称元数据）。
POST
向指定资源提交数据，请求服务器进行处理（例如提交表单或者上传文件）。数据被包含在请求本文中。这个请求可能会创建新的资源或修改现有资源，或二者皆有。
PUT
向指定资源位置上传其最新内容。
DELETE
请求服务器删除Request-URI所标识的资源。
TRACE
回显服务器收到的请求，主要用于测试或诊断。
OPTIONS
这个方法可使服务器传回该资源所支持的所有HTTP请求方法。用'*'来代替资源名称，向Web服务器发送OPTIONS请求，可以测试服务器功能是否正常运作。
CONNECT
HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。通常用于SSL加密服务器的链接（经由非加密的HTTP代理服务器）。
注意事项：
方法名称是区分大小写的。当某个请求所针对的资源不支持对应的请求方法的时候，服务器应当返回状态码405（Method Not Allowed），当服务器不认识或者不支持对应的请求方法的时候，应当返回状态码501（Not Implemented）。
HTTP服务器至少应该实现GET和HEAD方法，其他方法都是可选的。当然，所有的方法支持的实现都应当匹配下述的方法各自的语义定义。此外，除了上述方法，特定的HTTP服务器还能够扩展自定义的方法。例如PATCH（由 RFC 5789 指定的方法）用于将局部修改应用到资源。
```

- http状态码

所有HTTP响应的第一行都是状态行，依次是当前HTTP版本号，3位数字组成的状态代码，以及描述状态的短语，彼此由空格分隔。

状态代码的第一个数字代表当前响应的类型：

​	1xx消息——请求已被服务器接收，继续处理
​	2xx成功——请求已成功被服务器接收、理解、并接受
​	3xx重定向——需要后续操作才能完成这一请求
​	4xx请求错误——请求含有词法错误或者无法被执行
​	5xx服务器错误——服务器在处理某个正确请求时发生错误
虽然 RFC 2616 中已经推荐了描述状态的短语，例如"200 OK"，"404 Not Found"，但是WEB开发者仍然能够自行决定采用何种短语，用以显示本地化的状态描述或者自定义信息。

- url

超文本传输协议（HTTP）的统一资源定位符将从因特网获取信息的五个基本元素包括在一个简单的地址中：

- 传送协议。
  层级URL标记符号(为[//],固定不变)
  访问资源需要的凭证信息（可省略）
  服务器。（通常为域名，有时为IP地址）
  端口号。（以数字方式表示，若为HTTP的默认值“:80”可省略）
  路径。（以“/”字符区别路径中的每一个目录名称）
  查询。（GET模式的窗体参数，以“?”字符为起点，每个参数以“&”隔开，再以“=”分开参数名称与数据，通常以UTF8的URL编码，避开字符冲突的问题）
  片段。以“#”字符为起点
  以http://www.luffycity.com:80/news/index.html?id=250&page=1 为例, 其中：

  ​	http，是协议；
  ​	www.luffycity.com，是服务器；
  ​	80，是服务器上的网络端口号；
  ​	/news/index.html，是路径；
  ​	?id=250&page=1，是查询。
  大多数网页浏览器不要求用户输入网页中“http://”的部分，因为绝大多数网页内容是超文本传输协议文件。同样，“80”是超文本传输协议文件的常用端口号，因此一般也不必写明。一般来说用户只要键入统一资源定位符的一部分（www.luffycity.com:80/news/index.html?id=250&page=1）就可以了。

- http请求格式

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180322001733298-201433635.jpg)

- http响应格式

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180322001744323-654009411.jpg)

### 12.1   web框架原理

#### 12.1.1   web框架本质

- web框架的功能

```python
1.socket收发消息    - wsgiref   uwsgi 

2.根据不同的路径返回不同的内容

3.返回动态页面（字符串的替换） —— jinja2

django  2  3
flask  2
tornado 1 2 3 
```

我们可以这样理解：所有的Web应用本质上就是一个socket服务端，而用户的浏览器就是一个socket客户端。 这样我们就可以自己实现Web框架了。

- socket服务端

```python
import socket    
    
sk = socket.socket()    
sk.bind(("127.0.0.1", 80))    
sk.listen()    
    
    
while True:    
    conn, addr = sk.accept()    
    data = conn.recv(8096)    
    print(data)  # 将浏览器发来的消息打印出来    
    conn.send(b"OK")    
    conn.close() 
```

```python
#输出
b'GET / HTTP/1.1\r\nHost: 127.0.0.1:8080\r\nConnection: keep-alive\r\nCache-Control: max-age=0\r\nUpgrade-Insecure-Requests: 1\r\nUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3355.4 Safari/537.36\r\nAccept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8\r\nAccept-Encoding: gzip, deflate, br\r\nAccept-Language: zh-CN,zh;q=0.9\r\nCookie: csrftoken=CtHePYARJOKNx5oNVwxIteOJXpNyJ29L4bW4506YoVqFaIFFaHm0EWDZqKmw6Jm8\r\n\r\n'
#转换成字符串
GET / HTTP/1.1  
Host: 127.0.0.1:8080  
Connection: keep-alive  
Cache-Control: max-age=0  
Upgrade-Insecure-Requests: 1  
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3355.4 Safari/537.36  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8  
Accept-Encoding: gzip, deflate, br  
Accept-Language: zh-CN,zh;q=0.9  
Cookie: csrftoken=CtHePYARJOKNx5oNVwxIteOJXpNyJ29L4bW4506YoVqFaIFFaHm0EWDZqKmw6Jm8  
  
 
```

- http协议对首发消息的格式要求

每个HTTP请求和响应都遵循相同的格式，一个HTTP包含Header和Body两部分，其中Body是可选的。

HTTP响应的Header中有一个 Content-Type表明响应的内容格式。它的值如text/html; charset=utf-8。

text/html则表示是网页，charset=utf-8则表示编码为utf-8。

- http get请求的格式：

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180330221943115-1291906159.png)

- http响应的格式：

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180330222031912-1851965755.png)

- 自定义web框架

```python
import socket    
    
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)    
sock.bind(('127.0.0.1', 8000))    
sock.listen()    
    
while True:    
    conn, addr = sock.accept()    
    data = conn.recv(8096)    
    # 给回复的消息加上响应状态行    
    conn.send(b"HTTP/1.1 200 OK\r\n\r\n")    
    conn.send(b"OK")    
    conn.close() 
```

- 根据不同的路径返回不同的内容

```python
""" 
根据URL中不同的路径返回不同的内容 
"""  
  
import socket  
  
sk = socket.socket()  
sk.bind(("127.0.0.1", 8080))  # 绑定IP和端口  
sk.listen()  # 监听  
  
while True:  
    # 等待连接  
    conn, add = sk.accept()  
    data = conn.recv(8096)  # 接收客户端发来的消息  
    # 从data中取到路径  
    data = str(data, encoding="utf8")  # 把收到的字节类型的数据转换成字符串  
    # 按\r\n分割  
    data1 = data.split("\r\n")[0]  
    url = data1.split()[1]  # url是我们从浏览器发过来的消息中分离出的访问路径  
    conn.send(b'HTTP/1.1 200 OK\r\n\r\n')  # 因为要遵循HTTP协议，所以回复的消息也要加状态行  
    # 根据不同的路径返回不同内容  
    if url == "/index/":  
        response = b"index"  
    elif url == "/home/":  
        response = b"home"  
    else:  
        response = b"404 not found!"  
  
    conn.send(response)  
    conn.close()
```

- 根据不同的路径返回不同的内容--函数版

```python
""" 
根据URL中不同的路径返回不同的内容--函数版 
"""  
  
import socket  
  
sk = socket.socket()  
sk.bind(("127.0.0.1", 8080))  # 绑定IP和端口  
sk.listen()  # 监听  
  
  
# 将返回不同的内容部分封装成函数  
def func(url):  
    s = "这是{}页面！".format(url)  
    return bytes(s, encoding="utf8")  
  
  
while True:  
    # 等待连接  
    conn, add = sk.accept()  
    data = conn.recv(8096)  # 接收客户端发来的消息  
    # 从data中取到路径  
    data = str(data, encoding="utf8")  # 把收到的字节类型的数据转换成字符串  
    # 按\r\n分割  
    data1 = data.split("\r\n")[0]  
    url = data1.split()[1]  # url是我们从浏览器发过来的消息中分离出的访问路径  
    conn.send(b'HTTP/1.1 200 OK\r\n\r\n')  # 因为要遵循HTTP协议，所以回复的消息也要加状态行  
    # 根据不同的路径返回不同内容，response是具体的响应体  
    if url == "/index/":  
        response = func(url)  
    elif url == "/home/":  
        response = func(url)  
    else:  
        response = b"404 not found!"  
  
    conn.send(response)  
    conn.close() 
```

- 根据不同的路径返回不同的内容--函数进阶版

```python
""" 
根据URL中不同的路径返回不同的内容--函数进阶版 
"""  
  
import socket  
  
sk = socket.socket()  
sk.bind(("127.0.0.1", 8080))  # 绑定IP和端口  
sk.listen()  # 监听  
  
  
# 将返回不同的内容部分封装成不同的函数  
def index(url):  
    s = "这是{}页面XX！".format(url)  
    return bytes(s, encoding="utf8")  
  
  
def home(url):  
    s = "这是{}页面。。！".format(url)  
    return bytes(s, encoding="utf8")  
  
  
# 定义一个url和实际要执行的函数的对应关系  
list1 = [  
    ("/index/", index),  
    ("/home/", home),  
]  
  
while True:  
    # 等待连接  
    conn, add = sk.accept()  
    data = conn.recv(8096)  # 接收客户端发来的消息  
    # 从data中取到路径  
    data = str(data, encoding="utf8")  # 把收到的字节类型的数据转换成字符串  
    # 按\r\n分割  
    data1 = data.split("\r\n")[0]  
    url = data1.split()[1]  # url是我们从浏览器发过来的消息中分离出的访问路径  
    conn.send(b'HTTP/1.1 200 OK\r\n\r\n')  # 因为要遵循HTTP协议，所以回复的消息也要加状态行  
    # 根据不同的路径返回不同内容  
    func = None  # 定义一个保存将要执行的函数名的变量  
    for item in list1:  
        if item[0] == url:  
            func = item[1]  
            break  
    if func:  
        response = func(url)  
    else:  
        response = b"404 not found!"  
  
    # 返回具体的响应消息  
    conn.send(response)  
    conn.close() 
```

- 返回具体的html文件

```python
""" 
根据URL中不同的路径返回不同的内容--函数进阶版 
返回独立的HTML页面 
"""  
  
import socket  
  
sk = socket.socket()  
sk.bind(("127.0.0.1", 8080))  # 绑定IP和端口  
sk.listen()  # 监听  
  
  
# 将返回不同的内容部分封装成不同的函数  
def index(url):  
    # 读取index.html页面的内容  
    with open("index.html", "r", encoding="utf8") as f:  
        s = f.read()  
    # 返回字节数据  
    return bytes(s, encoding="utf8")  
  
  
def home(url):  
    with open("home.html", "r", encoding="utf8") as f:  
        s = f.read()  
    return bytes(s, encoding="utf8")  
  
  
# 定义一个url和实际要执行的函数的对应关系  
list1 = [  
    ("/index/", index),  
    ("/home/", home),  
]  
  
while True:  
    # 等待连接  
    conn, add = sk.accept()  
    data = conn.recv(8096)  # 接收客户端发来的消息  
    # 从data中取到路径  
    data = str(data, encoding="utf8")  # 把收到的字节类型的数据转换成字符串  
    # 按\r\n分割  
    data1 = data.split("\r\n")[0]  
    url = data1.split()[1]  # url是我们从浏览器发过来的消息中分离出的访问路径  
    conn.send(b'HTTP/1.1 200 OK\r\n\r\n')  # 因为要遵循HTTP协议，所以回复的消息也要加状态行  
    # 根据不同的路径返回不同内容  
    func = None  # 定义一个保存将要执行的函数名的变量  
    for item in list1:  
        if item[0] == url:  
            func = item[1]  
            break  
    if func:  
        response = func(url)  
    else:  
        response = b"404 not found!"  
  
    # 返回具体的响应消息  
    conn.send(response)  
    conn.close() 
```

```html
#index
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>index</title>
</head>
<body>
<div>这是index页面</div>
</body>
</html>
```

```html
#home
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>index</title>
</head>
<body>
<div>这是home页面</div>
</body>
</html>
```

- 使用时间戳来模拟动态数据让网页动起来

```python
""" 
根据URL中不同的路径返回不同的内容--函数进阶版 
返回独立的HTML页面 
"""  
  
import socket  
  
sk = socket.socket()  
sk.bind(("127.0.0.1", 8080))  # 绑定IP和端口  
sk.listen()  # 监听  
  
  
# 将返回不同的内容部分封装成不同的函数  
def index(url):  
    # 读取index.html页面的内容  
    with open("index.html", "r", encoding="utf8") as f:  
        s = f.read()  
    # 返回字节数据  
    return bytes(s, encoding="utf8")  
  
  
def home(url):  
    with open("home.html", "r", encoding="utf8") as f:  
        s = f.read()  
    return bytes(s, encoding="utf8")  
  
  
def timer(url):  
    import time  
    with open("time.html", "r", encoding="utf8") as f:  
        s = f.read()  
        s = s.replace('@@time@@', time.strftime("%Y-%m-%d %H:%M:%S"))  
    return bytes(s, encoding="utf8")  
  
  
# 定义一个url和实际要执行的函数的对应关系  
list1 = [  
    ("/index/", index),  
    ("/home/", home),  
    ("/time/", timer),  
]  
  
while True:  
    # 等待连接  
    conn, add = sk.accept()  
    data = conn.recv(8096)  # 接收客户端发来的消息  
    # 从data中取到路径  
    data = str(data, encoding="utf8")  # 把收到的字节类型的数据转换成字符串  
    # 按\r\n分割  
    data1 = data.split("\r\n")[0]  
    url = data1.split()[1]  # url是我们从浏览器发过来的消息中分离出的访问路径  
    conn.send(b'HTTP/1.1 200 OK\r\n\r\n')  # 因为要遵循HTTP协议，所以回复的消息也要加状态行  
    # 根据不同的路径返回不同内容  
    func = None  # 定义一个保存将要执行的函数名的变量  
    for item in list1:  
        if item[0] == url:  
            func = item[1]  
            break  
    if func:  
        response = func(url)  
    else:  
        response = b"404 not found!"  
  
    # 返回具体的响应消息  
    conn.send(response)  
    conn.close()
```

#### 12.1.2   服务程序和应用程序

对于真实开发中的python web程序来说，一般会分为两部分：服务器程序和应用程序。

服务器程序负责对socket服务端进行封装，并在请求到来时，对请求的各种数据进行整理。

应用程序则负责具体的逻辑处理。为了方便应用程序的开发，就出现了众多的Web框架，例如：Django、Flask、web.py 等。不同的框架有不同的开发方式，但是无论如何，开发出的应用程序都要和服务器程序配合，才能为用户提供服务。

这样，服务器程序就需要为不同的框架提供不同的支持。这样混乱的局面无论对于服务器还是框架，都是不好的。对服务器来说，需要支持各种不同框架，对框架来说，只有支持它的服务器才能被开发出的应用使用。

这时候，标准化就变得尤为重要。我们可以设立一个标准，只要服务器程序支持这个标准，框架也支持这个标准，那么他们就可以配合使用。一旦标准确定，双方各自实现。这样，服务器可以支持更多支持标准的框架，框架也可以使用更多支持标准的服务器。

WSGI（Web Server Gateway Interface）就是一种规范，它定义了使用Python编写的web应用程序与web服务器程序之间的接口格式，实现web应用程序与web服务器程序间的解耦。

常用的WSGI服务器有uWSGI、Gunicorn。而Python标准库提供的独立WSGI服务器叫wsgiref，Django开发环境用的就是这个模块来做服务器。

- wsgiref

```python
"""  
根据URL中不同的路径返回不同的内容--函数进阶版  
返回HTML页面  
让网页动态起来  
wsgiref模块版  
"""   
     
from wsgiref.simple_server import make_server   
     
     
# 将返回不同的内容部分封装成函数   
def index(url):   
    # 读取index.html页面的内容   
    with open("index.html", "r", encoding="utf8") as f:   
        s = f.read()   
    # 返回字节数据   
    return bytes(s, encoding="utf8")   
     
     
def home(url):   
    with open("home.html", "r", encoding="utf8") as f:   
        s = f.read()   
    return bytes(s, encoding="utf8")   
     
     
def timer(url):   
    import time   
    with open("time.html", "r", encoding="utf8") as f:   
        s = f.read()   
        s = s.replace('@@time@@', time.strftime("%Y-%m-%d %H:%M:%S"))   
    return bytes(s, encoding="utf8")   
     
     
# 定义一个url和实际要执行的函数的对应关系   
list1 = [   
    ("/index/", index),   
    ("/home/", home),   
    ("/time/", timer),   
]   
     
     
def run_server(environ, start_response):   
    start_response('200 OK', [('Content-Type', 'text/html;charset=utf8'), ])  # 设置HTTP响应的状态码和头信息   
    url = environ['PATH_INFO']  # 取到用户输入的url   
    func = None   
    for i in list1:   
        if i[0] == url:   
            func = i[1]   
            break   
    if func:   
        response = func(url)   
    else:   
        response = b"404 not found!"   
    return [response, ]   
     
     
if __name__ == '__main__':   
    httpd = make_server('127.0.0.1', 8090, run_server)   
    print("我在8090等你哦...")   
    httpd.serve_forever() 
```

- jinja2

上面的代码实现了一个简单的动态，我完全可以从数据库中查询数据，然后去替换我html中的对应内容，然后再发送给浏览器完成渲染。 这个过程就相当于HTML模板渲染数据。 本质上就是HTML内容中利用一些特殊的符号来替换要展示的数据。 我这里用的特殊符号是我定义的，其实模板渲染有个现成的工具： jinja2

下载jinja2：pip install jinja2

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Title</title>
</head>
<body>
    <h1>姓名：{{name}}</h1>
    <h1>爱好：</h1>
    <ul>
        {% for hobby in hobby_list %}
        <li>{{hobby}}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

使用jinja2渲染index2.html文件：

```python
from wsgiref.simple_server import make_server  
from jinja2 import Template  
  
  
def index(url):  
    # 读取HTML文件内容  
    with open("index2.html", "r", encoding="utf8") as f:  
        data = f.read()  
        template = Template(data)   # 生成模板文件  
        ret = template.render({'name': 'alex', 'hobby_list': ['抽烟', '喝酒', '烫头']})   # 把数据填充到模板中  
    return bytes(ret, encoding="utf8")  
  
  
def home(url):  
    with open("home.html", "r", encoding="utf8") as f:  
        s = f.read()  
    return bytes(s, encoding="utf8")  
  
  
# 定义一个url和实际要执行的函数的对应关系  
list1 = [  
    ("/index/", index),  
    ("/home/", home),  
]  
  
  
def run_server(environ, start_response):  
    start_response('200 OK', [('Content-Type', 'text/html;charset=utf8'), ])  # 设置HTTP响应的状态码和头信息  
    url = environ['PATH_INFO']  # 取到用户输入的url  
    func = None  
    for i in list1:  
        if i[0] == url:  
            func = i[1]  
            break  
    if func:  
        response = func(url)  
    else:  
        response = b"404 not found!"  
    return [response, ]  
  
  
if __name__ == '__main__':  
    httpd = make_server('127.0.0.1', 8090, run_server)  
    print("我在8090等你哦...")  
    httpd.serve_forever()
```

使用pymysql连接数据库：

```python
conn = pymysql.connect(host="127.0.0.1", port=3306, user="root", passwd="xxx", db="xxx", charset="utf8")
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
cursor.execute("select name, age, department_id from userinfo")
user_list = cursor.fetchall()
cursor.close()
conn.close()
```

创建一个测试的user表：

```python
CREATE TABLE user(
  id int auto_increment PRIMARY KEY,
  name CHAR(10) NOT NULL,
  hobby CHAR(20) NOT NULL
)engine=innodb DEFAULT charset=UTF8;
```

模板的原理就是字符串替换，我们只要在HTML页面中遵循jinja2的语法规则写上，其内部就会按照指定的语法进行相应的替换，从而达到动态的返回内容。

### 12.2   Django

Django的下载安装

- 命令行：
  - pip install django==1.11.21
  - pip install django==1.11.21 -i 源
- pycharm
  - setting--解释器--点+号---输入Django---选择版本--下载安装

#### 12.2.1  Django基础必备三件套

- 创建项目
  - 命令行：django-admin startproject 项目名称
  - pycharm
- 创建app
  - 命令行创建：pythonmanage.py startapp  app名
- 启动
  - 命令行：cd 项目的根目录 --> manage.py
  - python manage.py runserver  #127.0.0.1:8000
  - python manage.py runserver 80 #127.0.0.1:80
  - python manage.py runserver 0.0.0.0:80 #0.0.0.0:80
  - 使用pycharm
    - 点绿色三角    配置   ip  端口

from sjango.shortcuts import HttpResponse,render,redirect

响应

- HttpResponse

内部传入一个字符串参数，返回给浏览器

```python
def index(request):
    #业务逻辑代码
    return Httpresponse('ok')
```

- render

除request参数外还接受一个待渲染的模板文件和一个保存具体数据的字典参数。

将数据填充进模板文件，最后把结果返回给浏览器。（类似于我们上面用到的jinja2）

```python
def index(request):
    # 业务逻辑代码
    return render(request, "index.html", {"name": "alex", "hobby": ["烫头", "泡吧"]})
```

- redirect

接受一个URL参数，表示跳转到指定的URL。

```python
def index(request):
    # 业务逻辑代码
    return redirect("/home/")
```

- request函数
  - request.methon  --->请求方式  GET   PSOT 
  - request.GET     --->URL上的参数？name=xxx&age=18  {}.get
  - resquest.POST  --->form表单提交post请求的数据

#### 12.2.2   静态文件的配置和使用

1.静态文件的配置和使用

- settings.py

```python
STATIC_URL = '/static/'   # 别名
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static1'),
    os.path.join(BASE_DIR, 'static'),
    os.path.join(BASE_DIR, 'static2'),
]
```

```html
<link rel="stylesheet" href="/static/css/login.css">   # 别名开头
```

按照STATICFILES_DIRS列表的顺序进行查找。

2.简单的登录的实例

form表单提交数据注意的问题：

- 提交的地址action='' 请求的方式method='post'
- 所有的input框有name属性
- 有一个input框的type='submit'或者有一个button

提交post请求，把settings中的MIDDLEWARE的'django.middleware.crsf.CsrfViewMiddleware'注释掉

#### 12.2.3 .app

![1560324201437](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1560324201437.png)

创建app

- 使用命令行
  - python manage.py start app名称
- pycharm工具
  - tools --> run manage.py task --> startapp app名称
- 注册app

```python
INSTALLED_APPS = [
	...
    'app01',
    'app01.apps.App01Config',  # 推荐写法
]
```

urls.py 写URL路径和函数的对应关系

```python
from django.conf.urls import url
from app01 import views

urlpatterns = [
    url(r'^index/', views.index),
    url(r'^login/', views.login),
    url(r'^orm_test/', views.orm_test),
]
```

views.py写函数

```python
def login(request):
    
request.method   ——》 请求方式 GET  POST 
request.POST     ——》 form表单提交POST请求的数据  {}  request.POST['xxx'] request.POST.get('xxx',)

返回值
from django.shortcuts import HttpResponse, render, redirect
HttpResponse   —— 》 字符串 
render(request,'模板的文件名')  ——》 返回一个HTML页面 
redirect('重定向的地址')   ——》 重定向  /  响应头  Location：‘地址’ 
```

form表单

- form标签的属性  action=‘’  提交数据的地址  method='post'   提交方式
- 所有的input标签要有name属性   有的标签还需要定义value
- 要有input  type=submit  或者 button按钮

get和post请求的区别

```python
get 获取一个页面，提交的数据暴露在URL上
获取数据  request.GET
post 提交数据
数据隐藏不显示
获取数据  request.POST
```

#### 12.2.4  ORM

对象关系映射Object Relational Mapping

orm的作用：操作表，操作数据行

Django中使用MySQL数据库的流程

1.创建一个MySQL数据库

2.在settings中配置，Django连接MySQL数据库：

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',    # 引擎	
        'NAME': 'day53',						# 数据库名称
        'HOST': '127.0.0.1',					# ip地址
        'PORT':3306,							# 端口
        'USER':'root',							# 用户
        'PASSWORD':'123'						# 密码
        
    }
}
```

3.在于settings同级目录下的init文件中写：

```python
import pymysql
pymysql.install_as_MySQLdb()
```

4.创建表（在app下的models.py中写类）:

```python
from django.db import models

class User(models.Model):
    username = models.CharField(max_length=32)   # username varchar(32)
    password = models.CharField(max_length=32)   # username varchar(32)
```

5.执行数据库迁移的命令

python manage.py makemigrations   #  检测每个注册app下的model.py   记录model的变更记录

python manage.py migrate   #  同步变更记录到数据库中

orm操作

```python
# 获取表中所有的数据
ret = models.User.objects.all()  # QuerySet 对象列表  【对象】
# 获取一个对象（有且唯一）
obj = models.User.objects.get(username='alex')   # 获取不到或者获取到多个对象会报错
# 获取满足条件的对象
ret = models.User.objects.filter(username='alex1',password='dasb')  # QuerySet 对象列表
```

```python
对应关系
类        ---》  		 表
对象  	---》  		数据行（记录）
属性 		---》  		字段
```

### 12.3   图书管理系统

- 书籍管理

```python
class Book(models.Model):
    title = models.CharField(max_length=32)
    pub = models.ForeignKey('Publisher', on_delete=models.CASCADE)
```

备注：on_delete在Django2.0版本之后是必填的， 1.11之前可以不填；on_delete的参数 models.CASCADE  models.SET()  models.SET_DEFAULT models.SET_NULL

- 查询

```python
all_books = models.Book.objects.all()

for book in all_books:

    print(book.title)
    print(book.pub,type(book.pub))   #  ——> 所关联的出版社对象
    print(book.pub.pk)  #  查id 多一次查询
    print(book.pub_id)  # 直接在book表中查出的ID
    print(book.pub.name)
    print("*"*32)
```

- 新增

```python
models.Book.objects.create(title=book_name,pub=出版社的对象)
models.Book.objects.create(title=book_name,pub_id=pub_id)
```

- 删除

```python
pk = request.GET.get('id')
models.Book.objects.filter(pk=pk).delete()
```

- 编辑

```python
{% if book_obj.pub == publisher %}
    <option selected value="{{ publisher.pk }}"> {{ publisher.name }} </option>
{% else %}
    <option  value="{{ publisher.pk }}"> {{ publisher.name }} </option>
{% endif %}
```

```python
# 修改数据
book_obj.title = book_name
# book_obj.pub_id = pub_id
book_obj.pub = models.Publisher.objects.get(pk=pub_id)
book_obj.save()
```

- 模板的语法

```python
render(request,'模板的文件名'，{'xxxx':'v1'})
{{ xxxx }}

for循环
{% for i in list %}
	{{ forloop.counter }}
	{{ i }}
{% endfor %}

if判断

{% if 条件1  %}
	xxx
{% elif 条件2  %}
    xxx
{% else  %}
	xxxxx
{% endif %}
```

### 12.4   作者的管理

- 设计表结构
  - 出版社  书籍   作者

![1560760702912](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1560760702912.png)

```python
for author in all_authors:
    print(author)
    print(author.pk)
    print(author.name)
    print(author.books,type(author.books)) # 关系管理对象
    print(author.books.all(),type(author.books.all()))
    print('*'*30)
```

- 展示

  - 设计url

  ```python
  url(r'^author_list/', views.author_list),
  ```

  

  - 写函数

  ```python
  # 展示作者
  def author_list(request):
      # 查询所有的作者
      all_authors = models.Author.objects.all()
      return render(request,'author_list.html',{'all_authors':all_authors})
  ```

  - 写模板

  ```python
  {% for author in all_authors %}
      <tr>
          <td>{{ forloop.counter }}</td>
          <td>{{ author.pk }}</td>
          <td>{{ author.name }}</td>
          <td>
              {% for book in author.books.all %}
  
                  {% if forloop.last %}
                      《{{ book.title }}》
                  {% else %}
                      《{{ book.title }}》、
                  {% endif %}
  
              {% endfor %}
          </td>
  
      </tr>
  {% endfor %}
  ```

- 增加

```python
author_obj = models.Author.objects.create(name=author_name) # 只插入book表中的内容
author_obj.books.set(books)  # 设置作者和书籍多对多的关系
```

- 修改

```python
books = request.POST.getlist('books')

# 修改对象的数据
author_obj.name = name
author_obj.save()
# 多对多的关系
author_obj.books.set(books)  #  每次重新设置
```

- Django设置多对多关系三种方法

  - Django帮我们生成第三站表

  ```python
  class Author(models.Model):
      name = models.CharField(max_length=32)
      books = models.ManyToManyField('Book')  # 不在Author表中生产字段，生产第三张表
  ```

  - 自己创建第三张表

  ```python
  class AuthorBook(models.Model):
      author = models.ForeignKey(Author, on_delete=models.CASCADE)
      book = models.ForeignKey(Book, on_delete=models.CASCADE)
      date = models.DateField()
  ```

  - 自建的表和ManyToManyField联合使用

  ```python
  class Author(models.Model):
      name = models.CharField(max_length=32)
      books = models.ManyToManyField('Book',through='AuthorBook')  # 不在Author表中生产字段，生产第三张表
  
  
  class AuthorBook(models.Model):
      author = models.ForeignKey(Author, on_delete=models.CASCADE)
      book = models.ForeignKey(Book, on_delete=models.CASCADE)
      date = models.DateField()
  ```

  

#### 2.1.4   关于重定向

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180323145433091-385962907.png)

### 12.5   MVC框架和MTV框架

- MVC框架设计模式

MVC，全名是Model View Controller，是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：模型(Model)、视图(View)和控制器(Controller)，具有耦合性低、重用性高、生命周期成本低等优点。

![img](https://images2017.cnblogs.com/blog/867021/201801/867021-20180116155130396-1611801504.png)

Django框架的设计模式借鉴了MVC框架的思想，也是分成三部分，来降低各个部分之间的耦合性。

Django框架的不同之处在于它拆分的三部分为：Model（模型）、Template（模板）和View（视图），也就是MTV框架。

- Django的MTV模式

Model(模型)：负责业务对象与数据库的对象(ORM)

Template(模板)：负责如何把页面展示给用户

View(视图)：负责业务逻辑，并在适当的时候调用Model和Template

此外，Django还有一个urls分发器，他的作用是将一个个URL的页面请求分发给不用的view处理，view再调用相应的Model和Template

- Django框架图示

![img](https://images2017.cnblogs.com/blog/867021/201801/867021-20180116155153334-721949851.png)

- Django模板系统常用语法

```python
Django模板中只需要记两种特殊符号：
{{  }}和 {% %}
{{ }}表示变量，在模板渲染的时候替换成值，{% %}表示逻辑相关的操作。
```

- 变量

```python
{{ 变量名 }}
变量名由字母数字和下划线组成。
点（.）在模板语言中有特殊的含义，用来获取对象的相应属性值。
几个例子：
view中代码：
def template_test(request):
    l = [11, 22, 33]
    d = {"name": "alex"}
2
    class Person(object):
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def dream(self):
            return "{} is dream...".format(self.name)

    Alex = Person(name="Alex", age=34)
    Egon = Person(name="Egon", age=9000)
    Eva_J = Person(name="Eva_J", age=18)

    person_list = [Alex, Egon, Eva_J]
    return render(request, "template_test.html", {"l": l, "d": d, "person_list": person_list})
```

```python
render(request,'模板的文件名'，{k1:v1;k2:v2})

{{  k1 }}    {{ request }}

{{  list.索引 }}   ——正向索引

{{  dic.key   }}

{{  dic.keys   }}

{{  dic.values}}

{{  dic.items }}

{{  pub.name  }}

{{  pub.talk  }}

优先级    字典中的key  >  对象的属性或者方法  > 索引
```



模板中支持的写法：

```python
{# 取l中的第一个参数 #}
{{ l.0 }}
{# 取字典中key的值 #}
{{ d.name }}
{# 取对象的name属性 #}
{{ person_list.0.name }}
{# .操作只能调用不带参数的方法 #}
{{ person_list.0.dream }}
```

备注：模板系统遇到一个（）时，会按照如下顺序查询：

1.字典中查询 2.属性或者方法  3.数字索引

- Filters

翻译为过滤器，用来修改变量的显示结果。

语法：{{ value|filter_name:参数 }}  冒号左右无空格

default

```python
{{ value|default:"nothing"}}
如果value值没传的话就显示nothing
注：TEMPLATES的OPTIONS可以增加一个选项：string_if_invalid：'找不到'，可以替代default的的作用。
```

filesizeformat

```python
将值格式化为一个 “人类可读的” 文件尺寸 （例如 '13 KB', '4.1 MB', '102 bytes', 等等）。例如：
{{ value|filesizeformat }}
如果 value 是 123456789，输出将会是 117.7 MB。
```

add

```python
给变量加参数
{{ value|add:"2" }}
value是数字4，则输出结果为6
{{ first|add:second }}
如果first是[1,2,3],second是[4,5,6]，则输出[1,2,3,4,5,6]
```

truncatechars

```python
如果字符串字符多于指定的字符数量，那么会被截断。截断的字符串将以可翻译的省略号序列（“...”）结尾。
参数：截断的字符数
{{ value|truncatechars:9}}
```

date

```python
日期格式化
{{ value|date:"Y-m-d H:i:s"}}
```

safe

```python
Django的模板中会对HTML标签和JS等语法标签进行自动转义，原因显而易见，这样是为了安全。但是有的时候我们可能不希望这些HTML元素被转义，比如我们做一个内容管理系统，后台添加的文章中是经过修饰的，这些修饰可能是通过一个类似于FCKeditor编辑加注了HTML修饰符的文本，如果自动转义的话显示的就是保护HTML标签的源文件。为了在Django中关闭HTML的自动转义有两种方式，如果是一个单独的变量我们可以通过过滤器“|safe”的方式告诉Django这段代码是安全的不必转义。
比如：
value = "<a href='#'>点我</a>"
{{ value|safe}}
```

其他

```python
小写lower
{{ value|lower }}
大写upper
{{ value|upper }}
标题title
{{ value|title }}
左对齐ljust
{{ value|ljust }}
右对齐rjust
{{ value|rjust }}
居中center
{{ value|center }}
返回value的长度
{{ value|length }}
切片slice
{{ value|slice:'2:-1' }}
取第一个元素first
{{ value|first }}
取最后一个元素last
{{ value|last }}
使用字符串拼接 join
{{ value|join:'//' }}
```

- 自定义过滤器filter

自定义过滤器只是带有一个或两个参数的python函数：1.变量(输入)的值不一定是一个字符串  2.参数的值 这可以有一个默认值，或完全省略；         例如，在过滤器{{var|foo:'bar'}}中，过滤器foo将传递变量var和参数bar

自定义filter代码文件拜访位置：

```python
app01/
    __init__.py
    models.py
    templatetags/  # 在app01下面新建一个package package
        __init__.py
        app01_filters.py  # 建一个存放自定义filter的py文件
    views.py
```

编写自定义filter+装饰器

```python
from django import template
register = template.Library()

@register.filter
def fill(value, arg):
    return value.replace(" ", arg)

@register.filter(name="addSB")
def add_sb(value):
    return "{} SB".format(value)
```

使用自定义filter

```python
{# 先导入我们自定义filter那个文件 #}
{% load app01_filters %}

{# 使用我们自定义的filter #}
{{ somevariable|fill:"__" }}
{{ d.name|addSB }}
```

- tags

for

```python
<ul>
{% for user in user_list %}
    <li>{{ user.name }}</li>
{% endfor %}
</ul>
```

for循环可用的一些参数

```python
Variable	Description
forloop.counter	当前循环的索引值（从1开始）
forloop.counter0	当前循环的索引值（从0开始）
forloop.revcounter	当前循环的倒序索引值（到1结束）
forloop.revcounter0	当前循环的倒序索引值（到0结束）
forloop.first	当前循环是不是第一次循环（布尔值）
forloop.last	当前循环是不是最后一次循环（布尔值）
forloop.parentloop	本层循环的外层循环
```

for ....empty

```python
<ul>
{% for user in user_list %}
    <li>{{ user.name }}</li>
{% empty %}
    <li>空空如也</li>
{% endfor %}
</ul>
```

if,elif,else

```python
{% if user_list %}
  用户人数：{{ user_list|length }}
{% elif black_list %}
  黑名单数：{{ black_list|length }}
{% else %}
  没有用户
{% endif %}
```

也可以只有if和else

```python
{% if user_list|length > 5 %}
  七座豪华SUV
{% else %}
    黄包车
{% endif %}
if语句支持 and 、or、==、>、<、!=、<=、>=、in、not in、is、is not判断。
```

连续判断

```python
python  10>5>1  =》   10>5  and 5>1   true 

js     10>5>1  =》   10>5  =》 true   =》   1>1  false

模板中  不支持连续连续判断  也不支持算数运算（过滤器）
```

with定义一个中间变量

```python
{% with total=business.employees.count %}
    {{ total }} employee{{ total|pluralize }}
{% endwith %}
```

- csrf_token

```python
此标签用于跨站请求伪造保护
在页面的form表单里面写{% csrf_token %}
注释：{# ... #}
```

![1560927935148](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1560927935148.png)

![1560927949300](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1560927949300.png)

注意事项：

```python
1. Django的模板语言不支持连续判断，即不支持以下写法：

{% if a > b > c %}
...
{% endif %}
2. Django的模板语言中属性的优先级大于方法

def xx(request):
    d = {"a": 1, "b": 2, "c": 3, "items": "100"}
    return render(request, "xx.html", {"data": d})
如上，我们在使用render方法渲染一个页面的时候，传的字典d有一个key是items并且还有默认的 d.items() 方法，此时在模板语言中:

{{ data.items }}
默认会取d的items key的值
```

### 12.6   母版和继承

- 母版

就是一个普通HTML提取多个页面的公共部分 定义block块

```python
母版
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Title</title>
  {% block page-css %}
  
  {% endblock %}
</head>
<body>

<h1>这是母板的标题</h1>

{% block page-main %}

{% endblock %}
<h1>母板底部内容</h1>
{% block page-js %}

{% endblock %}
</body>
</html>
```

```python
继承母版，在子页面中在页面最上方使用下面的语句来继承母版：
{% extends 'layouts.html' %}
```

```python
块（block）
通过在母版中使用{% block  xxx %}来定义"块"。在子页面中通过定义母板中的block名来对应替换母板中相应的内容。
{% block page-main %}
  <p>世情薄</p>
  <p>人情恶</p>
  <p>雨送黄昏花易落</p>
{% endblock %}
```

```python
组件，可以将常用的页面内容如导航条，页尾信息等组件保存在单独的文件中，然后在需要使用的地方按如下语法导入即可。
{% include 'navbar.html' %}
```

```python
静态文件相关
{% load static %}
<img src="{% static "images/hi.jpg" %}" alt="Hi!" />
引用JS文件时使用：

{% load static %}
<script src="{% static "mytest.js" %}"></script>
某个文件多处被用到可以存为一个变量

{% load static %}
{% static "images/hi.jpg" as myphoto %}
<img src="{{ myphoto }}"></img>
```

- 使用get_static_prefix

```python
{% load static %}
<img src="{% get_static_prefix %}images/hi.jpg" alt="Hi!" />
或者

{% load static %}
{% get_static_prefix as STATIC_PREFIX %}

<img src="{{ STATIC_PREFIX }}images/hi.jpg" alt="Hi!" />
<img src="{{ STATIC_PREFIX }}images/hi2.jpg" alt="Hello!" />
```

- 自定义simpletag

```python
和自定义filter类似，只不过接收更灵活的参数。

定义注册simple tag

@register.simple_tag(name="plus")
def plus(a, b, c):
    return "{} + {} + {}".format(a, b, c)
使用自定义simple tag

{% load app01_demo %}

{# simple tag #}
{% plus "1" "2" "abc" %}
```

- inclusion_tag

```python
多用于返回html代码片段

示例：

templatetags/my_inclusion.py

复制代码
from django import template

register = template.Library()


@register.inclusion_tag('result.html')
def show_results(n):
    n = 1 if n < 1 else int(n)
    data = ["第{}项".format(i) for i in range(1, n+1)]
    return {"data": data}
复制代码
templates/result.html

<ul>
  {% for choice in data %}
    <li>{{ choice }}</li>
  {% endfor %}
</ul>
templates/index.html

复制代码
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>inclusion_tag test</title>
</head>
<body>

{% load my_inclusion %}

{% show_results 10 %}
</body>
</html>

```

### 12.7   Django的view（视图）

一个视图函数（类），简称视图，是一个简单的Python 函数（类），它接受Web请求并且返回Web响应。
响应可以是一张网页的HTML内容，一个重定向，一个404错误，一个XML文档，或者一张图片。
无论视图本身包含什么逻辑，都要返回响应。代码写在哪里也无所谓，只要它在你当前项目目录下面。除此之外没有更多的要求了——可以说“没有什么神奇的地方”。为了将代码放在某处，大家约定成俗将视图放置在项目（project）或应用程序（app）目录中的名为views.py的文件中。

#### 12.7.1   简单视图

下面是一个以HTML文档的形式返回当前日期和时间的视图：

```python
from django.http import HttpResponse
import datetime

def current_datetime(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return HttpResponse(html)
```

```python
让我们来逐行解释下上面的代码：
首先，我们从 django.http模块导入了HttpResponse类，以及Python的datetime库。
接着，我们定义了current_datetime函数。它就是视图函数。每个视图函数都使用HttpRequest对象作为第一个参数，并且通常称之为request。
注意，视图函数的名称并不重要；不需要用一个统一的命名方式来命名，以便让Django识别它。我们将其命名为current_datetime，是因为这个名称能够比较准确地反映出它实现的功能。
这个视图会返回一个HttpResponse对象，其中包含生成的响应。每个视图函数都负责返回一个HttpResponse对象。
Django使用请求和响应对象来通过系统传递状态。
当浏览器向服务端请求一个页面时，Django创建一个HttpRequest对象，该对象包含关于请求的元数据。然后，Django加载相应的视图，将这个HttpRequest对象作为第一个参数传递给视图函数。
每个视图负责返回一个HttpResponse对象。
```

#### 12.7.2   CBV和FBV

之前基于函数的view，称为FBV，还可以把view写成基于类的。

- FBV版(function base views)：

```python
# FBV版添加班级
def add_class(request):
    if request.method == "POST":
        class_name = request.POST.get("class_name")
        models.Classes.objects.create(name=class_name)
        return redirect("/class_list/")
    return render(request, "add_class.html")
```

- CBV版(class base views)：

```python
# CBV版添加班级
from django.views import View

class AddClass(View):

    def get(self, request):
        return render(request, "add_class.html")

    def post(self, request):
        class_name = request.POST.get("class_name")
        models.Classes.objects.create(name=class_name)
        return redirect("/class_list/")
备注：使用CBV时，urls.py中也做对应的修改;
# urls.py中
url(r'^add_class/$', views.AddClass.as_view()),
```

#### 12.7.3   给视图加装饰器

- 使用装饰器装饰FBV

FBV本身就是一个函数，所以和给普通的函数加装饰器无差：

```python
def wrapper(func):
    def inner(*args, **kwargs):
        start_time = time.time()
        ret = func(*args, **kwargs)
        end_time = time.time()
        print("used:", end_time-start_time)
        return ret
    return inner


# FBV版添加班级
@wrapper
def add_class(request):
    if request.method == "POST":
        class_name = request.POST.get("class_name")
        models.Classes.objects.create(name=class_name)
        return redirect("/class_list/")
    return render(request, "add_class.html")
```

- 使用装饰器装饰CBV

```python
类中的方法与独立函数不完全相同，因此不能直接将函数装饰器应用于类中的方法 ，我们需要先将其转换为方法装饰器。

Django中提供了method_decorator装饰器用于将函数装饰器转换为方法装饰器。
```

```python
# CBV版添加班级
from django.views import View
from django.utils.decorators import method_decorator

class AddClass(View):

    @method_decorator(wrapper)
    def get(self, request):
        return render(request, "add_class.html")

    def post(self, request):
        class_name = request.POST.get("class_name")
        models.Classes.objects.create(name=class_name)
        return redirect("/class_list/")
```

```python
# 使用CBV时要注意，请求过来后会先执行dispatch()这个方法，如果需要批量对具体的请求处理方法，如get，post等做一些操作的时候，这里我们可以手动改写dispatch方法，这个dispatch方法就和在FBV上加装饰器的效果一样。

class Login(View):
     
    def dispatch(self, request, *args, **kwargs):
        print('before')
        obj = super(Login,self).dispatch(request, *args, **kwargs)
        print('after')
        return obj
 
    def get(self,request):
        return render(request,'login.html')
 
    def post(self,request):
        print(request.POST.get('user'))
        return HttpResponse('Login.post')
```

12.7.4   request对象和response对象

- request对象

当一个页面被请求时，Django就会创建一个包含本次请求原信息的HttpRequest对象。
Django会将这个对象自动传递给响应的视图函数，一般视图函数约定俗成地使用 request 参数承接这个对象。

```python
请求相关的常用值
path_info     返回用户访问url，不包括域名
method        请求中使用的HTTP方法的字符串表示，全大写表示。
GET              包含所有HTTP  GET参数的类字典对象
POST           包含所有HTTP POST参数的类字典对象
body            请求体，byte类型 request.POST的数据就是从body里面提取到的
FILES           上传的文件  enctype='multipart/form-data'
META             请求头全大写 HTTP_开头   -变成了_
cookies    
session

```

```python
属性
所有的属性应该被认为是只读的，除非另有说明
属性：
　　django将请求报文中的请求行、头部信息、内容主体封装成 HttpRequest 类中的属性。
   除了特殊说明的之外，其他均为只读的。
0.HttpRequest.scheme
   表示请求方案的字符串（通常为http或https）
1.HttpRequest.body
　　一个字符串，代表请求报文的主体。在处理非 HTTP 形式的报文时非常有用，例如：二进制图片、XML,Json等。
　　但是，如果要处理表单数据的时候，推荐还是使用 HttpRequest.POST 。
　　另外，我们还可以用 python 的类文件方法去操作它，详情参考 HttpRequest.read() 。
2.HttpRequest.path
　　一个字符串，表示请求的路径组件（不含域名）。
　　例如："/music/bands/the_beatles/"
3.HttpRequest.method
　　一个字符串，表示请求使用的HTTP 方法。必须使用大写。
　　例如："GET"、"POST"
4.HttpRequest.encoding
　　一个字符串，表示提交的数据的编码方式（如果为 None 则表示使用 DEFAULT_CHARSET 的设置，默认为 'utf-8'）。
   这个属性是可写的，你可以修改它来修改访问表单数据使用的编码。
   接下来对属性的任何访问（例如从 GET 或 POST 中读取数据）将使用新的 encoding 值。
   如果你知道表单数据的编码不是 DEFAULT_CHARSET ，则使用它。
5.HttpRequest.GET 
　　一个类似于字典的对象，包含 HTTP GET 的所有参数。详情请参考 QueryDict 对象。
6.HttpRequest.POST
　　一个类似于字典的对象，如果请求中包含表单数据，则将这些数据封装成 QueryDict 对象。
　　POST 请求可以带有空的 POST 字典 —— 如果通过 HTTP POST 方法发送一个表单，但是表单中没有任何的数据，QueryDict 对象依然会被创建。
   因此，不应该使用 if request.POST  来检查使用的是否是POST 方法；应该使用 if request.method == "POST" 
　　另外：如果使用 POST 上传文件的话，文件信息将包含在 FILES 属性中。
 7.HttpRequest.COOKIES
　　一个标准的Python 字典，包含所有的cookie。键和值都为字符串。
8.HttpRequest.FILES
　　一个类似于字典的对象，包含所有的上传文件信息。
   FILES 中的每个键为<input type="file" name="" /> 中的name，值则为对应的数据。
　　注意，FILES 只有在请求的方法为POST 且提交的<form> 带有enctype="multipart/form-data" 的情况下才会
   包含数据。否则，FILES 将为一个空的类似于字典的对象。
9.HttpRequest.META
 　　一个标准的Python 字典，包含所有的HTTP 首部。具体的头部信息取决于客户端和服务器，下面是一些示例：
    CONTENT_LENGTH —— 请求的正文的长度（是一个字符串）。
    CONTENT_TYPE —— 请求的正文的MIME 类型。
    HTTP_ACCEPT —— 响应可接收的Content-Type。
    HTTP_ACCEPT_ENCODING —— 响应可接收的编码。
    HTTP_ACCEPT_LANGUAGE —— 响应可接收的语言。
    HTTP_HOST —— 客服端发送的HTTP Host 头部。
    HTTP_REFERER —— Referring 页面。
    HTTP_USER_AGENT —— 客户端的user-agent 字符串。
    QUERY_STRING —— 单个字符串形式的查询字符串（未解析过的形式）。
    REMOTE_ADDR —— 客户端的IP 地址。
    REMOTE_HOST —— 客户端的主机名。
    REMOTE_USER —— 服务器认证后的用户。
    REQUEST_METHOD —— 一个字符串，例如"GET" 或"POST"。
    SERVER_NAME —— 服务器的主机名。
    SERVER_PORT —— 服务器的端口（是一个字符串）。
 　　从上面可以看到，除 CONTENT_LENGTH 和 CONTENT_TYPE 之外，请求中的任何 HTTP 首部转换为 META 的键时，
    都会将所有字母大写并将连接符替换为下划线最后加上 HTTP_  前缀。
    所以，一个叫做 X-Bender 的头部将转换成 META 中的 HTTP_X_BENDER 键。
10.HttpRequest.user
　　一个 AUTH_USER_MODEL 类型的对象，表示当前登录的用户。
　　如果用户当前没有登录，user 将设置为 django.contrib.auth.models.AnonymousUser 的一个实例。你可以通过 is_authenticated() 区分它们。
    例如：
    if request.user.is_authenticated():
        # Do something for logged-in users.
    else:
        # Do something for anonymous users.
     　　user 只有当Django 启用 AuthenticationMiddleware 中间件时才可用。
     -------------------------------------------------------------------------------------
    匿名用户
    class models.AnonymousUser
    django.contrib.auth.models.AnonymousUser 类实现了django.contrib.auth.models.User 接口，但具有下面几个不同点：
    id 永远为None。
    username 永远为空字符串。
    get_username() 永远返回空字符串。
    is_staff 和 is_superuser 永远为False。
    is_active 永远为 False。
    groups 和 user_permissions 永远为空。
    is_anonymous() 返回True 而不是False。
    is_authenticated() 返回False 而不是True。
    set_password()、check_password()、save() 和delete() 引发 NotImplementedError。
    New in Django 1.8:
    新增 AnonymousUser.get_username() 以更好地模拟 django.contrib.auth.models.User。
11.HttpRequest.session
 　　一个既可读又可写的类似于字典的对象，表示当前的会话。只有当Django 启用会话的支持时才可用。
    完整的细节参见会话的文档。
```

```python
上传文件示例
def upload(request):
    """
    保存上传文件前，数据需要存放在某个位置。默认当上传文件小于2.5M时，django会将上传文件的全部内容读进内存。从内存读取一次，写磁盘一次。
    但当上传文件很大时，django会把上传文件写到临时文件中，然后存放到系统临时文件夹中。
    :param request: 
    :return: 
    """
    if request.method == "POST":
        # 从请求的FILES中获取上传文件的文件名，file为页面上type=files类型input的name属性值
        filename = request.FILES["file"].name
        # 在项目目录下新建一个文件
        with open(filename, "wb") as f:
            # 从上传的文件对象中一点一点读
            for chunk in request.FILES["file"].chunks():
                # 写入本地文件
                f.write(chunk)
        return HttpResponse("上传OK")
```

```python
方法
1.HttpRequest.get_host()

　　根据从HTTP_X_FORWARDED_HOST（如果打开 USE_X_FORWARDED_HOST，默认为False）和 HTTP_HOST 头部信息返回请求的原始主机。
   如果这两个头部没有提供相应的值，则使用SERVER_NAME 和SERVER_PORT，在PEP 3333 中有详细描述。

　　USE_X_FORWARDED_HOST：一个布尔值，用于指定是否优先使用 X-Forwarded-Host 首部，仅在代理设置了该首部的情况下，才可以被使用。

　　例如："127.0.0.1:8000"

　　注意：当主机位于多个代理后面时，get_host() 方法将会失败。除非使用中间件重写代理的首部。

 

2.HttpRequest.get_full_path()

　　返回 path，如果可以将加上查询字符串。

　　例如："/music/bands/the_beatles/?print=true"

 

3.HttpRequest.get_signed_cookie(key, default=RAISE_ERROR, salt='', max_age=None)

　　返回签名过的Cookie 对应的值，如果签名不再合法则返回django.core.signing.BadSignature。

　　如果提供 default 参数，将不会引发异常并返回 default 的值。

　　可选参数salt 可以用来对安全密钥强力攻击提供额外的保护。max_age 参数用于检查Cookie 对应的时间戳以确保Cookie 的时间不会超过max_age 秒。

        复制代码
        >>> request.get_signed_cookie('name')
        'Tony'
        >>> request.get_signed_cookie('name', salt='name-salt')
        'Tony' # 假设在设置cookie的时候使用的是相同的salt
        >>> request.get_signed_cookie('non-existing-cookie')
        ...
        KeyError: 'non-existing-cookie'    # 没有相应的键时触发异常
        >>> request.get_signed_cookie('non-existing-cookie', False)
        False
        >>> request.get_signed_cookie('cookie-that-was-tampered-with')
        ...
        BadSignature: ...    
        >>> request.get_signed_cookie('name', max_age=60)
        ...
        SignatureExpired: Signature age 1677.3839159 > 60 seconds
        >>> request.get_signed_cookie('name', False, max_age=60)
        False
        复制代码
         


4.HttpRequest.is_secure()

　　如果请求时是安全的，则返回True；即请求通是过 HTTPS 发起的。

 

5.HttpRequest.is_ajax()

　　如果请求是通过XMLHttpRequest 发起的，则返回True，方法是检查 HTTP_X_REQUESTED_WITH 相应的首部是否是字符串'XMLHttpRequest'。

　　大部分现代的 JavaScript 库都会发送这个头部。如果你编写自己的 XMLHttpRequest 调用（在浏览器端），你必须手工设置这个值来让 is_ajax() 可以工作。

　　如果一个响应需要根据请求是否是通过AJAX 发起的，并且你正在使用某种形式的缓存例如Django 的 cache middleware， 
   你应该使用 vary_on_headers('HTTP_X_REQUESTED_WITH') 装饰你的视图以让响应能够正确地缓存。
请求相关方法

备注：键值对的值是多个的时候，比如checkbox类型的input标签，select标签，需要用：
request.POST.getlist("hobby")
```

#### 12.7.4   response对象

```python
与由Django自动创建的HttpRequest对象相比，HttpResponse对象是我们的职责范围了。我们写的每个视图都需要实例化，填充和返回一个HttpResponse。
HttpResponse类位于django.http模块中。
```

```python
使用
传递字符串
from django.http import HttpResponse
response = HttpResponse("Here's the text of the Web page.")
response = HttpResponse("Text only, please.", content_type="text/plain")
设置或删除响应头信息
response = HttpResponse()
response['Content-Type'] = 'text/html; charset=UTF-8'
del response['Content-Type']
```

```python
属性
HttpResponse.content：响应内容

HttpResponse.charset：响应内容的编码

HttpResponse.status_code：响应的状态码
```

#### 12.7.5   JsonResponse对象

JsonResponse是HttpResponse的子类，专门用来生成JSON编码的响应。

```python
from django.http import JsonResponse

response = JsonResponse({'foo': 'bar'})
print(response.content)

b'{"foo": "bar"}'
```

默认只能传递字典类型，如果要传递非字典类型需要设置一下safe关键字参数。

```python
response = JsonResponse([1, 2, 3], safe=False)
```

#### 12.7.6   Django shortcut functions

- render()

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180329215116152-275073384.png)

```python
结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的 HttpResponse 对象。

参数：

request： 用于生成响应的请求对象。
template_name：要使用的模板的完整名称，可选的参数
context：添加到模板上下文的一个字典。默认是一个空字典。如果字典中的某个值是可调用的，视图将在渲染模板之前调用它。
content_type：生成的文档要使用的MIME类型。默认为 DEFAULT_CONTENT_TYPE 设置的值。默认为'text/html'
status：响应的状态码。默认为200。
useing: 用于加载模板的模板引擎的名称。
一个简单的例子：

from django.shortcuts import render

def my_view(request):
    # 视图的代码写在这里
    return render(request, 'myapp/index.html', {'foo': 'bar'})
上面的代码等于：

复制代码
from django.http import HttpResponse
from django.template import loader

def my_view(request):
    # 视图代码写在这里
    t = loader.get_template('myapp/index.html')
    c = {'foo': 'bar'}
    return HttpResponse(t.render(c, request))
```

- redirect()

```python
参数可以是：

一个模型：将调用模型的get_absolute_url() 函数
一个视图，可以带有参数：将使用urlresolvers.reverse 来反向解析名称
一个绝对的或相对的URL，将原封不动的作为重定向的位置。
默认返回一个临时的重定向；传递permanent=True 可以返回一个永久的重定向。

示例:

你可以用多种方式使用redirect() 函数。

传递一个具体的ORM对象（了解即可）

将调用具体ORM对象的get_absolute_url() 方法来获取重定向的URL：

from django.shortcuts import redirect
 
def my_view(request):
    ...
    object = MyModel.objects.get(...)
    return redirect(object)
传递一个视图的名称

def my_view(request):
    ...
    return redirect('some-view-name', foo='bar')
传递要重定向到的一个具体的网址

def my_view(request):
    ...
    return redirect('/some/url/')
当然也可以是一个完整的网址

def my_view(request):
    ...
    return redirect('http://example.com/')
默认情况下，redirect() 返回一个临时重定向。以上所有的形式都接收一个permanent 参数；如果设置为True，将返回一个永久的重定向：

def my_view(request):
    ...
    object = MyModel.objects.get(...)
    return redirect(object, permanent=True)　　
扩展阅读： 

临时重定向（响应状态码：302）和永久重定向（响应状态码：301）对普通用户来说是没什么区别的，它主要面向的是搜索引擎的机器人。

A页面临时重定向到B页面，那搜索引擎收录的就是A页面。

A页面永久重定向到B页面，那搜索引擎收录的就是B页面。
```

### 12.8   Django的路由系统

```python
URL配置(URLconf)就像Django所支撑网站的目录。它的本质是URL与要为该URL调用的视图函数之间的映射表。
我们就是以这种方式告诉Django，遇到哪个URL的时候，要对应执行哪个函数。
```

#### 12.8.1   URLconf配置

- 基本格式

```python
from django.conf.urls import url
from . import views
urlpatterns = [
    url(正则表达式, views视图，参数，别名),
    url(r'^home/$', views.home，{参数}，name='home'),
]
```

示例：

```python
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^articles/2003/$', views.special_case_2003),
    url(r'^articles/([0-9]{4})/$', views.year_archive),
    url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),
    url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),
]
```

- 参数说明

  - 正则表达式：一个正则表达式字符串
  - views视图：一个可调用对象，通常为一个视图函数
  - 参数：可选的要传递给视图函数的默认参数（字典形式）
  - 别名：一个可选的name参数

  注意：Django 2.0版本中的路由系统是下面的写法（[官方文档](https://docs.djangoproject.com/en/1.11/topics/http/urls/)）：

```python
from django.urls import path，re_path

urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    path('articles/<int:year>/', views.year_archive),
    path('articles/<int:year>/<int:month>/', views.month_archive),
    path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
]
2.0版本中re_path和1.11版本的url是一样的用法。
```

#### 12.8.2   正则表达式详解

- 基本配置

  ```python
  from django.conf.urls import url
  
  from . import views
  
  urlpatterns = [
      url(r'^articles/2003/$', views.special_case_2003),
      url(r'^articles/([0-9]{4})/$', views.year_archive),
      url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),
      url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),
  ]
  ```

  

- 注意事项

  1. urlpatterns中的元素按照书写顺序从上往下逐一匹配正则表达式，一旦匹配成功则不再继续。
  2. 若要从URL中捕获一个值，只需要在它周围放置一对圆括号（分组匹配）。
  3. 不需要添加一个前导的反斜杠，因为每个URL 都有。例如，应该是^articles 而不是 ^/articles。
  4. 每个正则表达式前面的'r' 是可选的但是建议加上。

- 补充说明

  ```
  # 是否开启URL访问地址后面不为/跳转至带有/的路径的配置项
  APPEND_SLASH=True
  ```

  Django settings.py配置文件中默认没有 APPEND_SLASH 这个参数，但 Django 默认这个参数为 APPEND_SLASH = True。 其作用就是自动在网址结尾加'/'。

  其效果就是：

  我们定义了urls.py：

  ```
  from django.conf.urls import url
  from app01 import views
  
  urlpatterns = [
      url(r'^blog/$', views.blog),
  ]
  ```

  访问 http://www.example.com/blog 时，默认将网址自动转换为 http://www.example/com/blog/ 。

  如果在settings.py中设置了 **APPEND_SLASH=False**，此时我们再请求 http://www.example.com/blog 时就会提示找不到页面。

#### 12.8.3   分组命名匹配

上面的示例使用简单的正则表达式分组匹配（通过圆括号）来捕获URL中的值并以位置参数形式传递给视图。

在更高级的用法中，可以使用分组命名匹配的正则表达式组来捕获URL中的值并以关键字参数形式传递给视图。

在Python的正则表达式中，分组命名正则表达式组的语法是`(?P<name>pattern)`，其中`name`是组的名称，`pattern`是要匹配的模式。

下面是以上URLconf 使用命名组的重写：

```
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^articles/2003/$', views.special_case_2003),
    url(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive),
    url(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/$', views.month_archive),
    url(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/(?P<day>[0-9]{2})/$', views.article_detail),
]
```

这个实现与前面的示例完全相同，只有一个细微的差别：捕获的值作为关键字参数而不是位置参数传递给视图函数。

例如，针对URL /articles/2017/12/相当于按以下方式调用视图函数：

```
views.month_archive(request, year="2017", month="12")
```

在实际应用中，使用分组命名匹配的方式可以让你的URLconf 更加明晰且不容易产生参数顺序问题的错误，但是有些开发人员则认为分组命名组语法太丑陋、繁琐。

至于究竟应该使用哪一种，你可以根据自己的喜好来决定。

- URLconf匹配的位置

  URLconf 在请求的URL 上查找，将它当做一个普通的Python 字符串。不包括GET和POST参数以及域名。

  例如，http://www.example.com/myapp/ 请求中，URLconf 将查找 /myapp/ 。

  在http://www.example.com/myapp/?page=3 请求中，URLconf 仍将查找 /myapp/ 。

  URLconf 不检查请求的方法。换句话讲，所有的请求方法 —— 同一个URL的`POST`、`GET`、`HEAD`等等 —— 都将路由到相同的函数。

- 捕获的参数永远都是字符串

  每个在URLconf中捕获的参数都作为一个普通的Python字符串传递给视图，无论正则表达式使用的是什么匹配方式。例如，下面这行URLconf 中：

  ```
  url(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive),
  ```

  传递到视图函数`views.year_archive()` 中的`year`参数永远是一个字符串类型。

- 视图函数中指定默认值

  ```python
  # urls.py中
  from django.conf.urls import url
  
  from . import views
  
  urlpatterns = [
      url(r'^blog/$', views.page),
      url(r'^blog/page(?P<num>[0-9]+)/$', views.page),
  ]
  
  # views.py中，可以为num指定默认值
  def page(request, num="1"):
      pass
  ```

  在上面的例子中，两个URL模式指向相同的view - views.page - 但是第一个模式并没有从URL中捕获任何东西。

  如果第一个模式匹配上了，page()函数将使用其默认参数num=“1”,如果第二个模式匹配，page()将使用正则表达式捕获到的num值。

- 路由分发include其他的RULconfs

  ```python
  
  #At any point, your urlpatterns can “include” other URLconf modules. This
  #essentially “roots” a set of URLs below other ones.
  
  #For example, here’s an excerpt of the URLconf for the Django website itself.
  #It includes a number of other URLconfs:
  
  
  from django.conf.urls import include, url
  
  urlpatterns = [
     	# url(r'^admin/', admin.site.urls),
      url(r'^app01/', include('app01.urls', namespace='app01')),
      url(r'^app02/', include('app02.urls', namespace='app02')),  # 可以包含其他的URLconfs文件
  ]
  ```

#### 12.8.4   命名URL和URL反向解析

在使用Django 项目时，一个常见的需求是获得URL的最终形式，以用于嵌入到生成的内容中（视图中和显示给用户的URL等）或者用于处理服务器端的导航（重定向等）。
人们强烈希望不要硬编码这些URL（费力、不可扩展且容易产生错误）或者设计一种与URLconf 毫不相关的专门的URL 生成机制，因为这样容易导致一定程度上产生过期的URL。
换句话讲，需要的是一个DRY 机制。除了其它有点，它还允许设计的URL 可以自动更新而不用遍历项目的源代码来搜索并替换过期的URL。
获取一个URL 最开始想到的信息是处理它视图的标识（例如名字），查找正确的URL 的其它必要的信息有视图参数的类型（位置参数、关键字参数）和值。
Django 提供一个办法是让URL 映射是URL 设计唯一的地方。你填充你的URLconf，然后可以双向使用它：

- 根据用户/浏览器发起的URL 请求，它调用正确的Django 视图，并从URL 中提取它的参数需要的值。
- 根据Django 视图的标识和将要传递给它的参数的值，获取与之关联的URL。

第一种方式是我们在前面的章节中一直讨论的用法。第二种方式叫做反向解析URL、反向URL 匹配、反向URL 查询或者简单的URL 反查。
在需要URL 的地方，对于不同层级，Django 提供不同的工具用于URL 反查：

- 在模板中：使用url模板标签。
- 在Python 代码中：使用django.core.urlresolvers.reverse() 函数。
- 在更高层的与处理Django 模型实例相关的代码中：使用get_absolute_url() 方法。

上面说了一大堆，你可能并没有看懂。（那是官方文档的生硬翻译）。

咱们简单来说就是可以给我们的URL匹配规则起个名字，一个URL匹配模式起一个名字。

这样我们以后就不需要写死URL代码了，只需要通过名字来调用当前的URL。

举个简单的例子：

```python
url(r'^home', views.home, name='home'),  # 给我的url匹配模式起名为 home
url(r'^index/(\d*)', views.index, name='index'),  # 给我的url匹配模式起名为index
```

这样：

在模板里面可以这样引用：

```
{% url 'home' %}
```

在views函数中可以这样引用：

```
from django.urls import reverse

reverse("index", args=("2018", ))
```

例子：
考虑下面的URLconf：

```python
from django.conf.urls import url

from . import views

urlpatterns = [
    # ...
    url(r'^articles/([0-9]{4})/$', views.year_archive, name='news-year-archive'),
    # ...
]
```

根据这里的设计，某一年nnnn对应的归档的URL是`/articles/nnnn/`。

你可以在模板的代码中使用下面的方法获得它们：

```python
<a href="{% url 'news-year-archive' 2012 %}">2012 Archive</a>

<ul>
{% for yearvar in year_list %}
<li><a href="{% url 'news-year-archive' yearvar %}">{{ yearvar }} Archive</a></li>
{% endfor %}
</ul>
```

在python代码中，这样使用：

```python
from django.urls import reverse
from django.shortcuts import redirect

def redirect_to_year(request):
    # ...
    year = 2006
    # ...
    return redirect(reverse('news-year-archive', args=(year,)))
```

如果出于某种原因决定按年归档文章发布的URL应该调整一下，那么你将只需要修改URLconf 中的内容。

在某些场景中，一个视图是通用的，所以在URL 和视图之间存在多对一的关系。对于这些情况，当反查URL 时，只有视图的名字还不够。

**注意：**

为了完成上面例子中的URL 反查，你将需要使用命名的URL 模式。URL 的名称使用的字符串可以包含任何你喜欢的字符。不只限制在合法的Python 名称。

当命名你的URL 模式时，请确保使用的名称不会与其它应用中名称冲突。如果你的URL 模式叫做`comment`，而另外一个应用中也有一个同样的名称，当你在模板中使用这个名称的时候不能保证将插入哪个URL。

在URL 名称中加上一个前缀，比如应用的名称，将减少冲突的可能。我们建议使用`myapp-comment` 而不是`comment`。

#### 12.8.5   命名空间模式

即使不同的APP使用相同的URL名称，URL的命名空间模式也可以让你唯一反转命名的URL。

举个例子：

project中的urls.py

```
from django.conf.urls import url, include
 
urlpatterns = [
    url(r'^app01/', include('app01.urls', namespace='app01')),
    url(r'^app02/', include('app02.urls', namespace='app02')),
]
```

app01中的urls.py

```
from django.conf.urls import url
from app01 import views
 
app_name = 'app01'
urlpatterns = [
    url(r'^(?P<pk>\d+)/$', views.detail, name='detail')
]
```

app02中的urls.py

```
from django.conf.urls import url
from app02 import views
 
app_name = 'app02'
urlpatterns = [
    url(r'^(?P<pk>\d+)/$', views.detail, name='detail')
]
```

现在，我的两个app中 url名称重复了，我反转URL的时候就可以通过命名空间的名称得到我当前的URL。

**语法：**

'命名空间名称:URL名称'

模板中使用：

```
{% url 'app01:detail' pk=12 pp=99 %}
```

views中的函数中使用

```
v = reverse('app01:detail', kwargs={'pk':11})
```

 这样即使app中URL的命名相同，我也可以反转得到正确的URL了。　

### 12.9   Django模型

ORM优缺点：

ORM优点：

```python
ORM解决的主要问题是对象和关系的映射。它通常将一个类和一张表一一对应，类的每个实例对应表中的一条记录，类的每个属性对应表中的每个字段。 
ORM提供了对数据库的映射，不用直接编写SQL代码，只需操作对象就能对数据库操作数据。
让软件开发人员专注于业务逻辑的处理，提高了开发效率。
```

ORM缺点：

```python
ORM的缺点是会在一定程度上牺牲程序的执行效率。
ORM的操作是有限的，也就是ORM定义好的操作是可以完成的，一些复杂的查询操作是完成不了。
ORM用多了SQL语句就不会写了，关系数据库相关技能退化...
```

ORM与DB的对应关系

```python
ORM                     DB
类                      数据表
对象                    数据行
属性                    字段
```





#### 12.9.1   ORM的字段和参数

```python
AutoField    主键
IntegerField  整数
CharField    字符串
BooleanField  布尔值
TextField    文本
DateTimeField DateField  日期时间
    auto_now_add=True    # 新增数据的时候会自动保存当前的时间
    auto_now=True        # 新增、修改数据的时候会自动保存当前的时间
DecimalField   十进制的小数
	max_digits       小数总长度   5
    decimal_places   小数位长度   2
```

参数：

auto_now_add=True 

auto_now=True 

null=True        数据库中字段是否可以为空

blank=True    form表单填写时可以为空

default        字段的默认值

db_index    创建索引

unique=True     唯一

choices=((0, '女'), (1, '男')     可填写的内容和提示

- 创建模型

定义person模型，包含first_name和last_name。

```python
from django.db import models
 
class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```

first_name和last_name是模型的字段，每个字段被指定为一个类属性，每个属性映射到一个数据库列。

上面person模型将会像这样创建一个数据库表：

```python
create table myapp_person("id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL);
```

- 说明：
  - 表myapp_person的名称是自动生成的，如果你要自定义表名，需要在model的Meta类中指定 db_table 参数，强烈建议使用小写表名，特别是使用MySQL作为数据库时。
  - id字段是自动添加的，如果你想要指定自定义主键，只需在其中一个字段中指定 primary_key=True 即可。如果Django发现你已经明确地设置了Field.primary_key，它将不会添加自动ID列。
  - 本示例中的CREATE TABLE SQL使用PostgreSQL语法进行格式化，但值得注意的是，Django会根据配置文件中指定的数据库类型来生成相应的SQL语句。
  - Django支持MySQL5.5及更高版本。

- 字段

  - 常用 字段

  **AutoField**

  自增的整形字段，必填参数primary_key=True，则成为数据库的主键。无该字段时，django自动创建。

  一个model不能有两个AutoField字段。

  **IntegerField**

  一个整数类型。数值的范围是 -2147483648 ~ 2147483647。

  **CharField**

  字符类型，必须提供max_length参数。max_length表示字符的长度。

  **DateField**

  日期类型，日期格式为YYYY-MM-DD，相当于Python中的datetime.date的实例。

  参数：

  - auto_now：每次修改时修改为当前日期时间。
  - auto_now_add：新创建对象时自动添加当前日期时间。

  auto_now和auto_now_add和default参数是互斥的，不能同时设置。

  **DatetimeField**

  日期时间字段，格式为YYYY-MM-DD HH:MM[:ss[.uuuuuu]][TZ]，相当于Python中的datetime.datetime的实例。

```python
AutoField(Field)
        - int自增列，必须填入参数 primary_key=True
    BigAutoField(AutoField)
        - bigint自增列，必须填入参数 primary_key=True
        注：当model中如果没有自增列，则自动会创建一个列名为id的列
        from django.db import models
        class UserInfo(models.Model):
            # 自动创建一个列名为id的且为自增的整数列
            username = models.CharField(max_length=32)
        class Group(models.Model):
            # 自定义自增列
            nid = models.AutoField(primary_key=True)
            name = models.CharField(max_length=32)
    SmallIntegerField(IntegerField):
        - 小整数 -32768 ～ 32767
  PositiveSmallIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
        - 正小整数 0 ～ 32767
    IntegerField(Field)
        - 整数列(有符号的) -2147483648 ～ 2147483647
  PositiveIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
        - 正整数 0 ～ 2147483647
    BigIntegerField(IntegerField):
        - 长整型(有符号的) -9223372036854775808 ～ 9223372036854775807
    BooleanField(Field)
        - 布尔值类型
    NullBooleanField(Field):
        - 可以为空的布尔值
    CharField(Field)
        - 字符类型
        - 必须提供max_length参数， max_length表示字符长度
    TextField(Field)
        - 文本类型
    EmailField(CharField)：
        - 字符串类型，Django Admin以及ModelForm中提供验证机制
    IPAddressField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供验证 IPV4 机制
    GenericIPAddressField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供验证 Ipv4和Ipv6
        - 参数：
            protocol，用于指定Ipv4或Ipv6， 'both',"ipv4","ipv6"
            unpack_ipv4， 如果指定为True，则输入::ffff:192.0.2.1时候，可解析为192.0.2.1，开启此功能，需要protocol="both"
    URLField(CharField)
        - 字符串类型，Django Admin以及ModelForm中提供验证 URL
    SlugField(CharField)
        - 字符串类型，Django Admin以及ModelForm中提供验证支持 字母、数字、下划线、连接符（减号）
    CommaSeparatedIntegerField(CharField)
        - 字符串类型，格式必须为逗号分割的数字
    UUIDField(Field)
        - 字符串类型，Django Admin以及ModelForm中提供对UUID格式的验证
    FilePathField(Field)
        - 字符串，Django Admin以及ModelForm中提供读取文件夹下文件的功能
        - 参数：
                path,                      文件夹路径
                match=None,                正则匹配
                recursive=False,           递归下面的文件夹
                allow_files=True,          允许文件
                allow_folders=False,       允许文件夹
    FileField(Field)
        - 字符串，路径保存在数据库，文件上传到指定目录
        - 参数：
            upload_to = ""      上传文件的保存路径
            storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
    ImageField(FileField)
        - 字符串，路径保存在数据库，文件上传到指定目录
        - 参数：
            upload_to = ""      上传文件的保存路径
            storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
            width_field=None,   上传图片的高度保存的数据库字段名（字符串）
            height_field=None   上传图片的宽度保存的数据库字段名（字符串）
    DateTimeField(DateField)
        - 日期+时间格式 YYYY-MM-DD HH:MM[:ss[.uuuuuu]][TZ]
    DateField(DateTimeCheckMixin, Field)
        - 日期格式      YYYY-MM-DD
    TimeField(DateTimeCheckMixin, Field)
        - 时间格式      HH:MM[:ss[.uuuuuu]]
    DurationField(Field)
        - 长整数，时间间隔，数据库中按照bigint存储，ORM中获取的值为datetime.timedelta类型
    FloatField(Field)
        - 浮点型
    DecimalField(Field)
        - 10进制小数
        - 参数：
            max_digits，小数总长度
            decimal_places，小数位长度
    BinaryField(Field)
        - 二进制类型
```

自定义一个char类型字段：

```python
class MyCharField(models.Field):
    """
    自定义的char类型的字段类
    """
    def __init__(self, max_length, *args, **kwargs):
        self.max_length = max_length
        super(MyCharField, self).__init__(max_length=max_length, *args, **kwargs)
 
    def db_type(self, connection):
        """
        限定生成数据库表的字段类型为char，长度为max_length指定的值
        """
        return 'char(%s)' % self.max_length
```

使用自定义char类型字段：

```python
class Class(models.Model):
    id = models.AutoField(primary_key=True)
    title = models.CharField(max_length=25)
    # 使用自定义的char类型的字段
    cname = MyCharField(max_length=25)#char类型
```



#### 12.9.2   表的参数

```python
class Meta:
    db_table = "person"  # 表名

    verbose_name = '个人信息'

    verbose_name_plural = '个人信息'

    index_together = [
        ("name", "age"),  # 应为两个存在的字段
    ]
    #
    unique_together = (("name", "age"),)   # 应为两个存在的字段
```

#### 12.9.3   ORM查询（13条）必知必会

- 返回queryset
  - all()对象列表
  - filter()过滤筛选
  - exclude()什么什么之外 排除此选项
  - values()拿到所有的字段和字段的值
  - values_list()拿到指定的字段的值
  - order_by()排序  负号时降序，默认升序
  - reverse()必须排序好的才能反转
  - distinct()去重
- 返回对象
  - get()获取满足添加的一个数据
  - first()取第一个元素 没有则None
  - last()取最后一个元素 没有则None
- 返回数字
  - count()计数
- 返回布尔值
  - exists()查询数据是否存在

#### 12.9.4   单表双下划线

```
import os

os.environ.setdefault('DJANGO_SETTINGS_MODULE','orm_prictice.settings')
import django

django.setup()
from app01 import models
#pk__gt greater than  大于
#pk__lt less than  大于
#pk__gte greater than  equal 大于等于
#pk__lte less than equal 大于等于
#pk__range[2,3]    两边都包含
#pk__in[2,3]    在列表内的
#name__contains  包含内容
#name__icontains  包含内容,忽略大小写
#name__startswith  以什么开头
#name__istartswith  以什么开头忽略大小写
#name__endswith  以什么结尾
#name__iendswith  以什么结尾忽略大小写
#birth__year='2019'  筛选年
#value__isnull=True or False  判断某个库的value是否为空的项
ret = models.Person.objects.filter(pk__gt=1)
ret = models.Person.objects.filter(name__contains='a')
ret = models.Person.objects.filter(birth__year='2019')
ret = models.Person.objects.filter(phone__isnull=True)
# ret = models.Person.objects.all()
print(ret)
```

#### 12.9.5   外键的操作

```python
import os

os.environ.setdefault('DJANGO_SETTINGS_MODULE','orm_prictice.settings')
import django

django.setup()
from app01 import models

#基于对象的查询
book_obj = models.Book.objects.get(title='桃花侠大战菊花怪')
#正向查询
# print(book_obj.pub)
#反向查询
pub_obj = models.Publisher.objects.get(pk=1)
# print(pub_obj.book_set.all())#类名小写_set 没有指定relate_name时
# print(pub_obj.book.all())#relate_name='book'从新定义了关联的name为book

#基于字段的查询
ret = models.Book.objects.filter(title='桃花侠大战菊花怪')
#查询老男孩出版的书
ret = models.Book.objects.filter(pub__name='清华出版社')

ret = models.Publisher.objects.filter(book__title='桃花侠大战菊花怪')
print(ret)
```

```python
class Publisher(models.Model):
    name = models.CharField(max_length=32, verbose_name="名称")

    def __str__(self):
        return self.name


class Book(models.Model):
    title = models.CharField(max_length=32)
    pub = models.ForeignKey(Publisher, related_name='books',related_query_name='xxx',on_delete=models.CASCADE)

    def __str__(self):
        return self.title
```



### 12.10   Django表查询操作

#### 12.10.1   多对多

```python
class Book(models.Model):
    title = models.CharField(max_length=32)
    pub = models.ForeignKey(Publisher,on_delete=models.CASCADE,related_name='books',related_query_name='book')
    def __str__(self):
        return self.title
class Author(models.Model):
    name = models.CharField(max_length=32,)
    books = models.ManyToManyField(Book,related_name='author')
    def __str__(self):
        return self.name
```

```python
import os

os.environ.setdefault('DJANGO_SETTINGS_MODULE','orm_prictice.settings')
import django

django.setup()

from app01 import models
#基于对象的正向查询
# mjj = models.Author.objects.get(pk=1)
# print(mjj.books.all())

#基于对象的反向查询
# book_obj = models.Book.objects.filter(title='嘻嘻哈哈').first()
# print(book_obj.author_set.all())
# print(book_obj.author.all())#定义了related_name=‘author’3
#查作者
# ret = models.Author.objects.filter(books__title='桃花豆豆啊')
# print(ret)
#查作者
# ret = models.Book.objects.filter(author__name='MJJ')
# print(ret)



#关系管理对象的方法
mjj = models.Author.objects.get(pk=1)
#all() 所关联的所有对象
print(mjj.books.all())
print(mjj)
# set 设置多对多的关系 []
# mjj.books.set([1,2,3])
mjj.books.set(models.Book.objects.filter(pk__in=[1,2,3]))

#add 添加多对多的关系 /(id,id)  (对象,对象)
mjj.books.add('4',5)

#remove 删除多对多的关系
# mjj.books.remove(4,5)
mjj.books.remove(*models.Book.objects.filter(pk__in=[4,5]))

#clear() 清除所有的多对多关系
# mjj.books.clear()

#create() 创建多对多关系
# obj = mjj.books.create(title='跟MJJ学前端',pub_id=1)
# print(obj)

# book_obj = models.Book.objects.get(pk=1)
# obj = book_obj.author.create(name='taibai')
# print(obj)


pub_obj = models.Publisher.objects.get(pk=1)
pub_obj.books.set(models.Book.objects.filter(pk__in=[4,5]))#不能用id
print(pub_obj.books.all())

# pub_obj.books.add(*models.Book.objects.filter(pk__in=[1,2]))
# pub_obj.books.remove(*models.Book.objects.filter(pk__in=[1,2]))
# pub_obj.books.clear()
pub_obj.books.create(title='用Python去养猪')
```



#### 12.10.2   聚合分组

```python
from app01 import models

from django.db.models import Max, Min, Avg, Sum, Count


ret = models.Book.objects.filter(pk__gt=3).aggregate(Max('price'),avg=Avg('price'))
print(ret)


# 分组
# 统计每一本书的作者个数
ret = models.Book.objects.annotate(count=Count('author')) # annotate 注释


# 统计出每个出版社的最便宜的书的价格
# 方式一
ret = models.Publisher.objects.annotate(Min('book__price')).values()
# 方式二
ret = models.Book.objects.values('pub_id').annotate(min=Min('price'))
# ret = models.Book.objects.values('pub__name').annotate(Min('price'))
# for ret in ret:
#     print(ret)

# 统计不止一个作者的图书
# ret = models.Book.objects.annotate(count=Count('author')).filter(count__gt=1)
# print(ret)

# 查询各个作者出的书的总价
ret = models.Author.objects.annotate(Sum('books__price')).values()
print(ret)
```



#### 12.10.3   F和Q

```python
from django.db.models import F

# 比较两个字段的值
ret=models.Book.objects.filter(sale__gt=F('kucun'))

# 只更新sale字段
models.Book.objects.all().update(sale=100)

# 取某个字段的值进行操作
models.Book.objects.all().update(sale=F('sale')*2+10)
```

- Q(条件)：|或、&与、~非

```python
from django.db.models import Q

ret = models.Book.objects.filter(Q(Q(pk__gt=3) | Q(pk__lt=2)) & Q(price__gt=50))
print(ret)
```



#### 12.10.4   事物

```python
from django.db import transaction

try:
	with transaction.atomic():
        # 进行一系列的ORM操作           					
       models.Publisher.objects.create(name='xxxxx')
       models.Publisher.objects.create(name='xxx22')

except Exception as e :
    print(e)
```



### 12.11   Cookie和Session

#### 12.11.1  Cookie

由来：

```python
大家都知道HTTP协议是无状态的。
无状态的意思是每次请求都是独立的，它的执行情况和结果与前面的请求和之后的请求都无直接关系，它不会受前面的请求响应情况直接影响，也不会直接影响后面的请求响应情况。
一句有意思的话来描述就是人生只如初见，对服务器来说，每次的请求都是全新的。
状态可以理解为客户端和服务器在某次会话中产生的数据，那无状态的就以为这些数据不会被保留。会话中产生的数据又是我们需要保存的，也就是说要“保持状态”。因此Cookie就是在这样一个场景下诞生。
```

什么是Cookie：保存在浏览器本地上一组组键值对

```python
Cookie具体指的是一段小信息，它是服务器发送出来存储在浏览器上的一组组键值对，下次访问服务器时浏览器会自动携带这些键值对，以便服务器提取有用信息。
```

Cookie的原理：

```python
Cookie的工作原理是：由服务器产生内容，浏览器收到请求后保存在本地；当浏览器再次访问时，浏览器会自动带上Cookie，这样服务器就能通过Cookie的内容来判断这个是“谁”了。
```

Cookie的应用：1.登陆    2.保存浏览习惯  3.简单的投票

Django中操作cookie

- 获取cookie

  ```python
  request.COOKIES['key']
  request.get_signed_cookie('key', default=RAISE_ERROR, salt='', max_age=None)
  ```

  get_signed_cookie方法的参数：

  - default: 默认值
  - salt: 加密盐
  - max_age: 后台控制过期时间

- 设置cookie

  ```python
  rep = HttpResponse(...)
  rep ＝ render(request, ...)
  
  rep.set_cookie(key,value,...) #    set-cookie:  key=value
  rep.set_signed_cookie(key,value,salt='加密盐',...)
  ```

  参数：

  - key, 键
  - value='', 值
  - max_age=None, 超时时间
  - expires=None, 超时时间(IE requires expires, so set it if hasn't been already.)
  - path='/', Cookie生效的路径，/ 表示根路径，特殊的：根路径的cookie可以被任何url的页面访问
  - domain=None, Cookie生效的域名
  - secure=False, https传输
  - httponly=False 只能http协议传输，无法被JavaScript获取（不是绝对，底层抓包可以获取到也可以被覆盖）

- 删除cookie

  ```python
  def logout(request):
      rep = redirect("/login/")
      rep.delete_cookie("user")  # 删除用户浏览器上之前设置的user的cookie值
      return rep
  ```

cookie版登陆校验

```python
def check_login(func):
    @wraps(func)
    def inner(request, *args, **kwargs):
        next_url = request.get_full_path()
        if request.get_signed_cookie("login", salt="SSS", default=None) == "yes":
            # 已经登录的用户...
            return func(request, *args, **kwargs)
        else:
            # 没有登录的用户，跳转刚到登录页面
            return redirect("/login/?next={}".format(next_url))
    return inner


def login(request):
    if request.method == "POST":
        username = request.POST.get("username")
        passwd = request.POST.get("password")
        if username == "xxx" and passwd == "dashabi":
            next_url = request.GET.get("next")
            if next_url and next_url != "/logout/":
                response = redirect(next_url)
            else:
                response = redirect("/class_list/")
            response.set_signed_cookie("login", "yes", salt="SSS")
            return response
    return render(request, "login.html")
```

#### 12.11.2   Session

Session的定义：保存在服务器上一组组键值对（必须依赖cookie）

为什么要有session：1.cookie保存在浏览器本地，不够安全。2.cookie大小个数收到限制。

Session的由来：

```python
Cookie虽然在一定程度上解决了“保持状态”的需求，但是由于Cookie本身最大支持4096字节，以及Cookie本身保存在客户端，可能被拦截或窃取，因此就需要有一种新的东西，它能支持更多的字节，并且他保存在服务器，有较高的安全性。这就是Session。

问题来了，基于HTTP协议的无状态特征，服务器根本就不知道访问者是“谁”。那么上述的Cookie就起到桥接的作用。

我们可以给每个客户端的Cookie分配一个唯一的id，这样用户在访问时，通过Cookie，服务器就知道来的人是“谁”。然后我们再根据不同的Cookie的id，在服务器上保存一段时间的私密资料，如“账号密码”等等。

总结而言：Cookie弥补了HTTP无状态的不足，让服务器知道来的人是“谁”；但是Cookie以文本的形式保存在本地，自身安全性较差；所以我们就通过Cookie识别不同的用户，对应的在Session里保存私密的信息以及超过4096字节的文本。

另外，上述所说的Cookie和Session其实是共通性的东西，不限于语言和框架。
```

Django中的Session相关方法

```python
# 获取、设置、删除Session中数据
request.session['k1']
request.session.get('k1',None)
request.session['k1'] = 123
request.session.setdefault('k1',123) # 存在则不设置
del request.session['k1']
request.session.pop['k1']
request.session.delete() #删除session的数据，不删除cookie
request.session.flush() #删除session的数据，删除cookie


# 所有 键、值、键值对
request.session.keys()
request.session.values()
request.session.items()
request.session.iterkeys()
request.session.itervalues()
request.session.iteritems()

# 会话session的key
request.session.session_key

# 将所有Session失效日期小于当前日期的数据删除
request.session.clear_expired()

# 检查会话session的key在数据库中是否存在
request.session.exists("session_key")

# 删除当前会话的所有Session数据
request.session.delete()
　　
# 删除当前的会话数据并删除会话的Cookie。
request.session.flush() 
    这用于确保前面的会话数据不可以再次被用户的浏览器访问
    例如，django.contrib.auth.logout() 函数中就会调用它。

# 设置会话Session和Cookie的超时时间
request.session.set_expiry(value)
    * 如果value是个整数，session会在些秒数后失效。
    * 如果value是个datatime或timedelta，session就会在这个时间后失效。
    * 如果value是0,用户关闭浏览器session就会失效。
    * 如果value是None,session会依赖全局session失效策略。
```

Session版登陆验证：

```python
from functools import wraps


def check_login(func):
    @wraps(func)
    def inner(request, *args, **kwargs):
        next_url = request.get_full_path()
        if request.session.get("user"):
            return func(request, *args, **kwargs)
        else:
            return redirect("/login/?next={}".format(next_url))
    return inner


def login(request):
    if request.method == "POST":
        user = request.POST.get("user")
        pwd = request.POST.get("pwd")

        if user == "alex" and pwd == "alex1234":
            # 设置session
            request.session["user"] = user
            # 获取跳到登陆页面之前的URL
            next_url = request.GET.get("next")
            # 如果有，就跳转回登陆之前的URL
            if next_url:
                return redirect(next_url)
            # 否则默认跳转到index页面
            else:
                return redirect("/index/")
    return render(request, "login.html")


@check_login
def logout(request):
    # 删除所有当前请求相关的session
    request.session.delete()
    return redirect("/login/")


@check_login
def index(request):
    current_user = request.session.get("user", None)
    return render(request, "index.html", {"user": current_user})
```

Django中的Session配置：Django中默认支持Session，其内部提供了5种类型的Session供开发者使用。

SESSION_SAVE_EVERY_REQUEST = False

from django.conf import global_settings

```python
1. 数据库Session
SESSION_ENGINE = 'django.contrib.sessions.backends.db'   # 引擎（默认）

2. 缓存Session
SESSION_ENGINE = 'django.contrib.sessions.backends.cache'  # 引擎
SESSION_CACHE_ALIAS = 'default'                            # 使用的缓存别名（默认内存缓存，也可以是memcache），此处别名依赖缓存的设置

3. 文件Session
SESSION_ENGINE = 'django.contrib.sessions.backends.file'    # 引擎
SESSION_FILE_PATH = None                                    # 缓存文件路径，如果为None，则使用tempfile模块获取一个临时地址tempfile.gettempdir() 

4. 缓存+数据库
SESSION_ENGINE = 'django.contrib.sessions.backends.cached_db'        # 引擎

5. 加密Cookie Session
SESSION_ENGINE = 'django.contrib.sessions.backends.signed_cookies'   # 引擎

其他公用设置项：
SESSION_COOKIE_NAME ＝ "sessionid"                       # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串（默认）
SESSION_COOKIE_PATH ＝ "/"                               # Session的cookie保存的路径（默认）
SESSION_COOKIE_DOMAIN = None                             # Session的cookie保存的域名（默认）
SESSION_COOKIE_SECURE = False                            # 是否Https传输cookie（默认）
SESSION_COOKIE_HTTPONLY = True                           # 是否Session的cookie只支持http传输（默认）
SESSION_COOKIE_AGE = 1209600                             # Session的cookie失效日期（2周）（默认）
SESSION_EXPIRE_AT_BROWSER_CLOSE = False                  # 是否关闭浏览器使得Session过期（默认）
SESSION_SAVE_EVERY_REQUEST = False                       # 是否每次请求都保存Session，默认修改之后才保存（默认）
```

### 12.12   csrf装饰器和ajax

#### 12.12.1   csrf跨站请求伪造

- csrf装饰器

  ```python
  from django.views.decorators.csrf import csrf_exempt,csrf_protect，ensure_csrf_cookie
  csrf_exempt   某个视图不需要进行csrf校验
  csrf_protect  某个视图需要进行csrf校验
  ensure_csrf_cookie  确保生成csrf的cookie
  ```

- csrf功能

1.csrf中间件中执行process_request：

​	1.从cookie中获取到csrftoken的值

​	2.csrftoken的值放到request.META

2.执行process_view

​	1.查询视图函数是否使用csrf_exempt装饰器，使用了就不进行csrf的校验

​	2.判断请求方式：

​		1.如果是'GET','HEAD','OPTIONS','TRACE',不惊醒csrf校验

​		2.其他的请求方式（post,input）进行csrf校验：

​			a.获取cookie中csrftoken的值，获取csrfmiddlewaretoken的值，能获取到----》request_csrf_token         获取不到----》获取请求头中X_csrftoken的值---》request_csrf_tokem      比较上述request_csrf_token和cookie中csrftoken的值，比较成功接收请求，比较不成功拒绝请求。

#### 12.12.2   ajax

12.12.2.1   ajax准备知识：

​	什么是json？

- JSON 指的是 JavaScript 对象表示法（JavaScript Object Notation）
- JSON 是轻量级的文本数据交换格式
- JSON 独立于语言 *
- JSON 具有自我描述性，更易理解

JSON 使用 JavaScript 语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。

![img](https://images2018.cnblogs.com/blog/867021/201804/867021-20180407213606833-782897022.jpg)

合格的json对象：

```python
["one", "two", "three"]
{ "one": 1, "two": 2, "three": 3 }
{"names": ["张三", "李四"] }
[ { "name": "张三"}, {"name": "李四"} ]　
```

不合格的json对象：

```python
{ name: "张三", 'age': 32 }  　　　　　　 // 属性名必须使用双引号
[32, 64, 128, 0xFFF] 　　　　　　　　　　  // 不能使用十六进制值
{ "name": "张三", "age": undefined }    // 不能使用undefined
{ "name": "张三",
  "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
  "getName":  function() {return this.name;}  // 不能使用函数和日期对象
}
```

- stringify与parse方法

  JavaScript中关于json对象和字符串转换的两个方法：

  JSON.parse():用于将一个json字符串转换为JavaScript对象

  ```python
  JSON.parse('{"name":"alex"}');
  JSON.parse('{name:"alex"}') ;      // 错误
  JSON.parse('[18,undefined]') ;     // 错误
  ```

  JSON.stringfy():用于将JavaScript值转换为json字符串

  ```python
  JSON.stringify({"name":"alex"})
  ```

- JSON和XML的比较

  JSON 格式于2001年由 Douglas Crockford 提出，目的就是取代繁琐笨重的 XML 格式。

  JSON 格式有两个显著的优点：书写简单，一目了然；符合 JavaScript 原生语法，可以由解释引擎直接处理，不用另外添加解析代码。所以，JSON迅速被接受，已经成为各大网站交换数据的标准格式，并被写入ECMAScript 5，成为标准的一部分。

  XML和JSON都使用结构化方法来标记数据，下面来做一个简单的比较。

  用XML表示中国部分省市数据如下：

  ```python
  <?xml version="1.0" encoding="utf-8"?>
  <country>
      <name>中国</name>
      <province>
          <name>黑龙江</name>
          <cities>
              <city>哈尔滨</city>
              <city>大庆</city>
          </cities>
      </province>
  </country>
  ```

  用json表示：

  ```python
  {
      "name": "中国",
      "province": [{
          "name": "黑龙江",
          "cities": {
              "city": ["哈尔滨", "大庆"]
          }
      }]
  }
  ```

  由上面的两端代码可以看出，JSON 简单的语法格式和清晰的层次结构明显要比 XML 容易阅读，并且在数据交换方面，由于 JSON 所使用的字符要比 XML 少得多，可以大大得节约传输数据所占用得带宽。

12.12.2.2   ajax

ajax简介：AJAX（Asynchronous Javascript And XML）翻译成中文就是“异步的Javascript和XML”。即使用Javascript语言与服务器进行异步交互，传输的数据为XML（当然，传输的数据不只是XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。（这一特点给用户的感受是在不知不觉中完成请求和响应过程）

AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。

- 同步交互：客户端发出一个请求后，需要等待服务器响应结束后，才能发出第二个请求；
- 异步交互：客户端发出一个请求后，无需等待服务器响应结束，就可以发出第二个请求。

示例：

页面输入两个整数，通过AJAX传输到后端计算出结果并返回。

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AJAX局部刷新实例</title>
</head>
<body>

<input type="text" id="i1">+
<input type="text" id="i2">=
<input type="text" id="i3">
<input type="button" value="AJAX提交" id="b1">

<script src="/static/jquery-3.2.1.min.js"></script>
<script>
  $("#b1").on("click", function () {
    $.ajax({
      url:"/ajax_add/",
      type:"GET",
      data:{"i1":$("#i1").val(),"i2":$("#i2").val()},
      success:function (data) {
        $("#i3").val(data);
      }
    })
  })
</script>
</body>
</html>

HTML部分代码
```

```python
def ajax_demo1(request):
    return render(request, "ajax_demo1.html")


def ajax_add(request):
    i1 = int(request.GET.get("i1"))
    i2 = int(request.GET.get("i2"))
    ret = i1 + i2
    return JsonResponse(ret, safe=False)
```

```
urlpatterns = [
    ...
    url(r'^ajax_add/', views.ajax_add),
    url(r'^ajax_demo1/', views.ajax_demo1),
    ...   
]
```

ajax常见应用场景：

搜索引擎根据用户输入的关键字，自动提示检索关键字。

还有一个很重要的应用场景就是注册时候的用户名的查重。

其实这里就使用了AJAX技术！当文件框发生了输入变化时，使用AJAX技术向服务器发送一个请求，然后服务器会把查询到的结果响应给浏览器，最后再把后端返回的结果展示出来。

- 整个过程中页面没有刷新，只是刷新页面中的局部位置而已！
- 当请求发出后，浏览器还可以进行其他操作，无需等待服务器的响应！

![img](https://images2015.cnblogs.com/blog/877318/201610/877318-20161025165534625-1155566124.png)

当输入用户名后，把光标移动到其他表单项上时，浏览器会使用AJAX技术向服务器发出请求，服务器会查询名为lemontree7777777的用户是否存在，最终服务器返回true表示名为lemontree7777777的用户已经存在了，浏览器在得到结果后显示“用户名已被注册！”。

- 整个过程中页面没有刷新，只是局部刷新了；
- 在请求发出后，浏览器不用等待服务器响应结果就可以进行其他操作；

ajax的优点：

1.AJAX使用JavaScript技术向服务器发送异步请求；

2.AJAX请求无须刷新整个页面；

3.因为服务器响应内容不再是整个页面，而是页面中的部分内容，所以AJAX性能高； 

- 发请求的方式

1.地址栏输入地址 GET

2.form表单 GET/POST

3.a标签  GET

- ajax：使用js的技术发请求和接收响应     特点：1.异步 2.局部刷新  3.传输的数据量少

- 最基本的jQuery发送ajax请求示例：

  ```python
  <!DOCTYPE html>
  <html lang="zh-CN">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>ajax test</title>
    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
  </head>
  <body>
  <button id="ajaxTest">AJAX 测试</button>
  <script>
    $("#ajaxTest").click(function () {
      $.ajax({
        url: "/ajax_test/",
        type: "POST",
        data: {username: "Q1mi", password: 123456},
        success: function (data) {
          alert(data)
        }
      })
    })
  </script>
  </body>
  </html>
  ```

  views.py

  ```python
  def ajax_test(request):
      user_name = request.POST.get("username")
      password = request.POST.get("password")
      print(user_name, password)
      return HttpResponse("OK")
  ```

  $.ajax参数

  data参数中的键值对，如果值值不为字符串，需要将其转换成字符串类型。

  ```python
  $("#b1").on("click", function () {
      $.ajax({
        url:"/ajax_add/",
        type:"GET",
        data:{"i1":$("#i1").val(),"i2":$("#i2").val(),"hehe": JSON.stringify([1, 2, 3])},
        success:function (data) {
          $("#i3").val(data);
        }
      })
    })
  ```

js实现ajax

```python
var b2 = document.getElementById("b2");
  b2.onclick = function () {
    // 原生JS
    var xmlHttp = new XMLHttpRequest();
    xmlHttp.open("POST", "/ajax_test/", true);
    xmlHttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    xmlHttp.send("username=q1mi&password=123456");
    xmlHttp.onreadystatechange = function () {
      if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
        alert(xmlHttp.responseText);
      }
    };
  };　
```

ajax请求设置csrf_token

方式一：通过获取隐藏的input标签中的csrfmiddlewaretoken值，放置在data中发送。

```python
$.ajax({
  url: "/cookie_ajax/",
  type: "POST",
  data: {
    "username": "Q1mi",
    "password": 123456,
    "csrfmiddlewaretoken": $("[name = 'csrfmiddlewaretoken']").val()  // 使用jQuery取出csrfmiddlewaretoken的值，拼接到data中
  },
  success: function (data) {
    console.log(data);
  }
})
```

方式二：通过获取返回的cookie中的字符串 放置在请求头中发送。

注意：需要引入一个jquery.cookie.js插件。

```python
$.ajax({
  url: "/cookie_ajax/",
  type: "POST",
  headers: {"X-CSRFToken": $.cookie('csrftoken')},  // 从Cookie取csrftoken，并设置到请求头中
  data: {"username": "Q1mi", "password": 123456},
  success: function (data) {
    console.log(data);
  }
})
```

自己写一个getcookie方法：

```python
function getCookie(name) {
    var cookieValue = null;
    if (document.cookie && document.cookie !== '') {
        var cookies = document.cookie.split(';');
        for (var i = 0; i < cookies.length; i++) {
            var cookie = jQuery.trim(cookies[i]);
            // Does this cookie string begin with the name we want?
            if (cookie.substring(0, name.length + 1) === (name + '=')) {
                cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
                break;
            }
        }
    }
    return cookieValue;
}
var csrftoken = getCookie('csrftoken');
```

每一次都这么写太麻烦了，可以使用$.ajaxsetup()方法为ajax请求统一设置

```python
function csrfSafeMethod(method) {
  // these HTTP methods do not require CSRF protection
  return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
}

$.ajaxSetup({
  beforeSend: function (xhr, settings) {
    if (!csrfSafeMethod(settings.type) && !this.crossDomain) {
      xhr.setRequestHeader("X-CSRFToken", csrftoken);
    }
  }
});
```

注意：

如果使用从cookie中取csrftoken的方式，需要确保cookie存在csrftoken值。

如果你的视图渲染的HTML文件中没有包含 {% csrf_token %}，Django可能不会设置CSRFtoken的cookie。

这个时候需要使用ensure_csrf_cookie()装饰器强制设置Cookie。

```python
django.views.decorators.csrf import ensure_csrf_cookie


@ensure_csrf_cookie
def login(request):
    pass
```









- jquery发ajax请求

  ```python
  $.ajax({
      url: '/calc/',
      type: 'post',
      data: {
          a: $("[name='i1']").val(),
          b: $("[name='i2']").val(),
      },
      success: function (res) {
          $("[name='i3']").val(res)
      },
      error:function (error) {
          console.log(error)
      }
  })
  ```

- 上传文件

  ```python
  <input type="file" id="f1">
  <button id="b1">上传</button>
  
  
  $('#b1').click(function () {
          var  formobj =  new FormData();
  
          formobj.append('file',document.getElementById('f1').files[0]);
          // formobj.append('file',$('#f1')[0].files[0]);
          formobj.append('name','alex');
  
          $.ajax({
              url: '/upload/',
              type: 'post',
              data:formobj ,
              processData:false,  // 
              contentType:false,
              success: function (res) {
                  $("[name='i3']").val(res)
              },
          })
      })
  ```

- ajax通过csrf的校验：

前提条件：确保有csrftoken的cookie

在页面中使用{% csrf_token %}

加装饰器 ensure_csrf_cookie

from django.views.decorators.csrf import csrf_exempt,csrf_protect,ensure_csrf_cookie

1.给data中添加csrfmiddlewaretoken的值

```python
data: {
    'csrfmiddlewaretoken':$('[name="csrfmiddlewaretoken"]').val(),
    a: $("[name='i1']").val(),
    b: $("[name='i2']").val(),
},
```

2.加请求头

```python
headers:{
    'x-csrftoken':$('[name="csrfmiddlewaretoken"]').val(),
},
```

3.使用文件





















































