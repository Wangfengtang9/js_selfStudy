# DOM

浏览器已经为我们提供 文档节点 对象这个对象是window属性

可以在页面中直接使用，文档节点代表的是整个网页

## 1、事件

 事件，就是用户和浏览器之间的交互行为，

比如：点击按钮，鼠标移动、关闭窗口。。。

**（1）**我们可以在事件对应的属性中设置一些js代码，这样当事件被触发时，这些代码将会执行

> 这种写法我们称为结构和行为耦合，不方便维护，不推荐使用	

~~~js
<button id="btn" onmousemove="alert('讨厌，你点我干嘛！');">我是一个按钮</button>
<button id="btn">我是一个按钮</button>
~~~

**（2）**可以为按钮的对应事件绑定处理函数的形式来响应事件，

这样当事件被触发时，其对应的函数将会被调用

~~~js
//获取按钮对象
var btn = document.getElementById("btn");
//绑定一个单击事件
//像这种为单击事件绑定的函数，我们称为单击响应函数
btn.onclick = function(){
		alert("你还点~~~");
};
~~~
## 2、文档的加载

### onload事件会在整个页面加载完成之后才触发

为window绑定一个onload事件：该事件对应的响应函数将会在页面加载完成之后执行，这样可以确保我们的代码执行时所有的DOM对象已经加载完毕了

~~~js
<script type="text/javascript">
window.onload = function(){
                    //获取id为btn的按钮
                    var btn = document.getElementById("btn");
                    //为按钮绑定一个单击响应函数
                    btn.onclick = function(){
                        alert("hello");
                    };
};
</script>
<button id="btn">点我一下</button>
~~~

>浏览器在加载一个页面时，是按照自上向下的顺序加载的，读取到一行就运行一行,如果将script标签写到页面的上边，在代码执行时，页面还没有加载，页面没有加载DOM对象也没有加载，会导致无法获取到DOM对象
>
>将js代码编写到页面的下部就是为了，可以在页面加载完毕以后再执行js代码

## 3、节点

 （1）文档节点（document）：整个HTML文档

 （2）元素节点（Element）：HTML文档中的HTML标签

 （3）文本节点（Element）：HTML标签中的文本内容

（4） 属性节点（Element）：元素的属性

## 4、dom节点查询

### （1）获取元素节点

> 通过document对象调用

1）getElementById()：通过id属性获取一个元素节点对象

**2） getElementsByTagName()**：通过标签名获取**一组**元素节点对象

这个方法会给我们返回一个类数组对象，所有查询到的元素都会封装到对象中

即使查询到的元素只有一个，也会封装到数组中返回

~~~js
// 获取tr中的a，getElementsByTagName是获取的数组，要取第一个，加上[0]，而querySelector获取的是标签为a的第一个对象
（1） var a = tr.getElementsByTagName('a')[0]
（2）var a = tr.querySelector('a')
~~~

3）getElementsByName()：通过name属性获取一组元素节点对象

### （2）获取元素节点的子节点

> 通过具体的元素节点调用

1）方法

getElementsByTagName()：返回当前节点的指定标签名后代节点

2）属性

- childNodes ：表示当前节点的所有子节点

  childNodes属性会获取包括文本节点在内的所有节点，根据DOM标签标签间空白也会当成文本节点

  > children属性可以获取当前元素的所有子元素

- firstChild：表示当前节点的第一个子节点

- lastChild： 表示当前节点的最后一个子节点

### （3）获取父节点和兄弟节点

 通过具体的节点调用

1）parentNode属性，表示当前节点的父节点

2）previousSibling属性，表示当前节点的前一个兄弟节点 （也可能获取到空白的文本）

3）nextSibling属性，表示当前节点的后一个兄弟节点

### （4）使用CSS选择器进行查询

**1）document.querySelector()**

 需要一个选择器的字符串作为参数，可以根据一个CSS选择器来查询一个元素节点对象

使用该方法总会返回唯一的一个元素，如果满足条件的元素有多个，那么它只会**返回第一个**

**2）document.querySelectorAll()**

该方法和querySelector()用法类似，不同的是它会将符合条件的元素封装到一个数组中返回

 即使符合条件的元素只有一个，它也会**返回数组** 

### （5）innerHTML、innerText

（1）innerHTML用于获取元素内部的HTML代码的

对于自结束标签，这个属性没有意义

如果需要读取元素节点属性，直接使用 元素.属性名，例子：元素.id 元素.name 元素.value

注意：class属性不能采用这种方式，读取class属性时需要使用 元素.className

（2）innerText该属性可以获取到元素内部的文本内容

它和innerHTML类似，不同的是它会自动将html去除

>返回#bj的文本值
>
>（1）bj.innerHTML
>
>（2）bj.firstChild.nodeValue 
>
>元素节点的firstChild来获取文本节点
>
>文本节点可以通过nodeValue属性获取和设置文本节点的内容

### （6）其他属性

1）document.documentElement保存的是html根标签

2）根据元素的class属性值查询一组元素节点对象，

getElementsByClassName()可以根据class属性值获取一组元素节点对象，

>获取页面中的所有的div
>
>var divs = document.getElementsByTagName("div");

### （7）公共函数

定义一个函数，专门用来为指定元素绑定单击响应函数

参数：

idStr 要绑定单击响应函数的对象的id**属性值**，

fun 事件的回调**函数**，当单击元素时，该函数将会被触发

~~~js
function myClick(idStr , fun){
                var btn = document.getElementById(idStr);
                btn.onclick = fun;
}
//设置#username的value属性值
myClick("btn10",function(){
    //获取id为username的元素
    var um = document.getElementById("username");
    um.value = "今天天气真不错~~~";
});

~~~

>//为id为btn01的按钮绑定一个单击响应函数
>var btn01 = document.getElementById("btn01");
>btn01.onclick = function(){
>    //查找#bj节点
>    var bj = document.getElementById("bj");
>    alert(bj.innerHTML);
>    };

## 8、案例

### （1）切换图片

1）获取两个按钮，分别为两个按钮绑定单击响应函数，

2）获取img标签，点击按钮是否能切换图片（切换图片就是修改img的src属性）

3）先看是否图片能两张切换，再看图片是否能多张切换，最后图片循环切换

4）创建一个数组，用来保存图片的路径

5）创建一个变量，来保存当前正在显示的图片的索引，切换到上一张，索引自减（index--），切换到下一张是index自增（index++）

6）循环图片，用if函数判断，第一张图片切换上一张是第5张图片，同理，最后一张图片切换图片是第一张

7）给图片添加提示信息，在p标签内写上文字，再分别在单击响应函数里添加，当点击按钮以后，重新设置信息

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0; padding: 0;
        }
        #outer {
            width: 500px;
            background-color: pink;
            text-align: center;
            margin: 50px auto;
            padding: 8px;
        }
    </style>

    <script>
        window.onload = function () {
            //获取两个按钮
            var prev = document.getElementById('prev')
            var next = document.getElementById('next')

            //获取img标签
            var img =document.getElementsByTagName('img')[0]
            //创建一个数组，用来保存图片的路径
            imgArr = ['./img/1.jpg', './img/2.jpg', './img/3.jpg', './img/4.jpg', './img/5.jpg']
        
            //创建一个变量，来保存当前正在显示的图片的索引
            var index = 0
            
            var info = document.getElementById('info')

            //分别为两个按钮绑定单击响应函数
            prev.onclick = function () {
                index--
                if (index < 0) {
                    index = imgArr.length - 1
                }
                img.src = imgArr[index]
                info.innerHTML = `一共${imgArr.length}张图片，当前第${index + 1}张`

            }
            next.onclick = function () {
                index++
                if (index > imgArr.length - 1) {
                    index = 0
                }
                //切换图片就是修改img的src属性
                //要修改一个元素的属性 元素.属性 = 属性值
                img.src = imgArr[index]
                info.innerHTML = `一共${imgArr.length}张图片，当前第${index + 1}张`
            }
        }
    </script>
</head>
<body>
    <div id="outer">
        <p id="info">一共5张图片，当前第1张</p>
        <img src="./img/1.jpg" alt="没有了">
        <button id="prev">上一张</button>
        <button id="next">下一张</button>
    </div>
</body>
</html>
~~~

### （2）全选

通过多选框的checked属性可以来获取或设置多选框的选中状态

1）全选按钮

2）全不选按钮

3）反选按钮：点击按钮以后，选中的变成没选中，没选中的变成选中

4）提交按钮：点击按钮以后，将所有选中的多选框的value属性值弹出

5）全选/全不选 多选框：当它选中时，其余的也选中，当它取消时其余的也取消

- 在事件的响应函数中，响应函数是给谁绑定的this就是谁

  1.以函数的形式调用时，this永远都是window

  2.以方法的形式调用时，this就是调用方法的那个对象

- 如果四个多选框全都选中，则checkedAllBox也应该选中
- 如果四个多选框没都选中，则checkedAllBox也不应该选中

~~~js

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>全选练习</title>
<script>
    window.onload = function() {
        var checkedAllBtn = document.getElementById('checkedAllBtn')
        var checkedNoBtn = document.getElementById('checkedNoBtn')
        //获取四个多选框items
        var items = document.getElementsByName('items')
        var checkedRevBtn = document.getElementById('checkedRevBtn')
        var sendBtn = document.getElementById('sendBtn')
        var checkedAllBox = document.getElementById('checkedAllBox')
        // 1、全选
        checkedAllBtn.onclick = function() {
            checkedAllBox.checked = true
            for(var i = 0; i < items.length; i++) {
                items[i].checked = true
            }
        }
        // 2、全不选
        checkedNoBtn.onclick = function() {
            checkedAllBox.checked = false
            for(var i = 0; i < items.length; i++) {
                items[i].checked = false
            }
        }
        // 3、反选
        checkedRevBtn.onclick = function() {
            checkedAllBox.checked = !checkedAllBox.checked
            for(var i = 0; i < items.length; i++) {
                items[i].checked = !items[i].checked
            }
        }
        // 4、提交
        sendBtn.onclick = function() {
            for(var i = 0; i < items.length; i++) {
                if (items[i].checked) {
                    console.log(items[i].value);
                }
            }
        }
        // 5、全选 / 全不选
        checkedAllBox.onclick = function() {
            for(var i = 0; i < items.length; i++) {
                // items[i].checked = checkedAllBox.checked
                items[i].checked = this.checked
            }
        }
        // 为4个多选框绑定单机响应函数
        for(var i = 0; i < items.length; i++) {
            items[i].onclick = function() {
                // 先将checkedAllBox设置成选中状态
                checkedAllBox.checked = true

                // 判断多选框是否多选
                for (var j = 0; j < items.length; j++) {
                    // 只要有1个没选中则不是全选
                    if(!items[j].checked) {
                        checkedAllBox.checked = false
                        // 一旦进入判断，则已经得出结果，不用再继续执行循环
                        break
                    }
                }
            }
        }
    }
</script>
</head>
<body>

	<form method="post" action="">
		你爱好的运动是？<input type="checkbox" id="checkedAllBox" />全选/全不选 
		<br />
		<input type="checkbox" name="items" value="足球" />足球
		<input type="checkbox" name="items" value="篮球" />篮球
		<input type="checkbox" name="items" value="羽毛球" />羽毛球
		<input type="checkbox" name="items" value="乒乓球" />乒乓球
		<br />
		<input type="button" id="checkedAllBtn" value="全　选" />
		<input type="button" id="checkedNoBtn" value="全不选" />
		<input type="button" id="checkedRevBtn" value="反　选" />
		<input type="button" id="sendBtn" value="提　交" />
	</form>
</body>
</html>
~~~

## 9、dom增删改

### （1）appendChild()

向一个父节点中添加一个新的子节点

用法：父节点.appendChild(子节点);

### （2）insertBefore()

可以在指定的子节点前插入新的子节点

语法：父节点.insertBefore(新节点,旧节点);

### （3）replaceChild()

可以使用指定的子节点替换已有的子节点

语法：父节点.replaceChild(新节点,旧节点);

### （4）removeChild()

可以删除一个子节点

语法：

1）父节点.removeChild(子节点);

**2）子节点.parentNode.removeChild(子节点);**

### （5）创建元素节点、文本节点

**1）document.createElement()**

可以用于创建一个元素节点对象，

它需要一个标签名作为参数，将会根据该标签名创建元素节点对象，并将创建好的对象作为返回值返回

**2）document.createTextNode()**

可以用来创建一个文本节点对象，

需要一个文本内容作为参数，将会根据该内容创建文本节点，并将新的节点返回

### （6）创建一个"广州"节点,添加到#city下

1）创建广州节点 <li>广州</li>，创建li元素节点，创建文本节点

2）添加到city下

~~~js
myClick('btn01', function () {
                    //创建广州节点 <li>广州</li>
                    var li =  document.createElement('li')
                    var gzText = document.createTextNode('广州')
                    //将gzText设置li的子节点
                    li.appendChild(gzText)
                    //添加到city下
                    var city = document.getElementById('city')
                    city.appendChild(li)
})
（改进）
myClick('btn07', function () {
                    //创建一个li
                    var li =  document.createElement('li')
                    //向li中设置文本
                    li.innerHTML = '广州'
                    var city = document.getElementById('city')
                    city.appendChild(li)
})
~~~

## 10、表格案例

### （1）思路：

**1）点击超链接以后，删除一个员工的信息**

2）获取所有超链接，为每个超链接都绑定一个单击响应函数

3）因为删除tr的响应函数是公共代码，所以可以提取出来，封装，调用函数（注意不加括号）

4）点击‘删除’，删除的是这一行，所以找tr，再removeChild

5）删除之前弹出一个提示框，有取消和确定的按钮，实现不同的功能

**6）添加员工的功能 ：点击按钮以后，将员工的信息添加到表格中**

7）先获取新成员信息，再创建元素tr，往里面添加内容

8）为新添加的a再绑定一次单击响应函数

9）使之加到tbody当中

### （2）添加文本内容的方式：

~~~js
//需要做出的效果
<tr>
        <td>Tom</td>
        <td>tom@tom.com</td>
        <td>5000</td>
        <td><a href="javascript:;">Delete</a></td>
</tr>
~~~

1）原始方法：创建tr，再先创建td元素和内容，再将内容追加到td元素中，再将td追加到tr中

~~~js
// 创建元素
var tr = document.createElement('tr')

var nameTd = document.createElement('td')
var emailTd = document.createElement('td')
var salaryTd = document.createElement('td')
var aTd = document.createElement('td')

// 创建内容
var nameText = document.createTextNode(empName)
var emailText = document.createTextNode(email)
var salaryText = document.createTextNode(salary)
var aText = document.createTextNode('Delete')

// 元素和内容绑定
nameTd.appendChild(nameText)
emailTd.appendChild(emailText)
salaryTd.appendChild(salaryText)

// 创建一个a
var a = document.createElement('a')
a.href = 'javascript:;'
aTd.appendChild(a)
a.appendChild(aText)

// 将td添加到tr中
tr.appendChild(nameTd)
tr.appendChild(emailTd)
tr.appendChild(salaryTd)
tr.appendChild(aTd)

// 为a添加点击事件
a.onclick = delA
~~~

2）常用方法：只创建一个tr，往tr中添加

~~~js
// 创建元素
var tr = document.createElement('tr')

tr.innerHTML = `
<tr>
    <td>${empName}</td>
    <td>${email}</td>
    <td>${salary}</td>
    <td><a href="javascript:;">Delete</a></td>
</tr>
`
// 为tr中的a添加点击事件
// var a = tr.getElementsByTagName('a')[0]
var a = tr.querySelector('a')
a.onclick = delA

 整个tbody里面内容都会发生改变，所以不推荐
// tbody.innerHTML += `
// 	<tr>
// 		<td>${empName}</td>
// 		<td>${email}</td>
// 		<td>${salary}</td>
// 		<td><a href="javascript:;">Delete</a></td>
// 	</tr>
// `
~~~

> 点击超链接以后，超链接会跳转页面，这个是超链接的默认行为，
>
> 但是此时我们不希望出现默认行为，可以通过在响应函数的最后return false来取消默认行为

## 11、使用dom操作css

### （1）通过JS修改元素的样式：

语法：元素.style.样式名 = 样式值

> 注意：如果CSS的样式名中含有-，这种名称在JS中是不合法的比如background-color，
>
> 需要将这种样式名修改为驼峰命名法，去掉-，然后将-后的字母大写=>(backgroundColor)

我们通过style属性设置的样式都是内联样式，而内联样式有较高的优先级，所以通过JS修改的样式往往会立即显示，但是如果在样式中写了!important，则此时样式会有最高的优先级，	即使通过JS也不能覆盖该样式，此时将会导致JS修改样式失效，所以尽量不要为样式添加!important

### （2）读取样式：

#### 语法：元素.style.样式名

通过style属性设置和读取的都是内联样式,无法读取样式表中的样式

### （3）获取当前元素的样式：

1）元素.currentStyle.样式名   （IE浏览器）

#### 2）getComputedStyle()   

需要两个参数，

第一个：要获取样式的元素，

第二个：可以传递一个伪元素，一般都传null

该方法会返回一个对象，对象中封装了当前元素对应的样式

可以通过对象.样式名来读取样式

~~~js
getComputedStyle(box1,null).backgroundColor
~~~

如果获取的样式没有设置，则会获取到真实的值，而不是默认值

比如：没有设置width，它不会获取到auto，而是一个长度

> 变量没找到会报错，属性没找到是undefined

**通过currentStyle和getComputedStyle()读取到的样式都是只读的，**

**不能修改，如果要修改必须通过style属性**

#### （3）getStyle()方法

定义一个函数，用来获取指定元素的当前的样式

参数：

obj 要获取样式的元素

name 要获取的样式名

~~~js
获取当前元素的样式，定义一个函数，调用
function getStyle(obj, name) {
            return getComputedStyle(obj , null)[name]
 }
getStyle(box1, 'left')
~~~

~~~js
处理兼容性问题
function getStyle(obj , name){
          if(window.getComputedStyle){
            //正常浏览器的方式，具有getComputedStyle()方法
            return getComputedStyle(obj , null)[name];
          }else{
            //IE8的方式，没有getComputedStyle()方法
            return obj.currentStyle[name];
          }
          //return window.getComputedStyle?getComputedStyle(obj , null)[name]:obj.currentStyle[name];			
}
~~~

## 12、其他样式操作的属性

### （1）clientWidth、clientHeight

这两个属性可以获取元素的**可见**宽度和高度

这些属性都是不带px的，返回都是一个数字，可以直接进行计算

会获取元素宽度和高度，包括内容区和内边距

这些属性都是只读的，不能修改

### （2）offsetWidth、offsetHeight

获取元素的整个的宽度和高度，包括内容区、内边距和边框

### （3）offsetParent

可以用来获取当前元素的定位父元素

会获取到离当前元素最近的开启了定位的祖先元素

如果所有的祖先元素都没有开启定位，则返回body

### （4）offsetLeft：

当前元素相对于其定位父元素的水平偏移量

### （5）offsetTop： 

当前元素相对于其定位父元素的垂直偏移量

### （6）scrollWidth、scrollHeight

可以获取元素整个滚动区域的宽度和高度

### （7）scrollLeft：可以获取水平滚动条滚动的距离

### （8）scrollTop：可以获取垂直滚动条滚动的距离

### （9）当满足scrollHeight - scrollTop == clientHeight，说明垂直滚动条滚动到底了

scrollTop 是小数，scrollHeight 和 clientHeight是整数

parseInt(info.scrollTop)

### （10）案例

当垂直滚动条滚动到底时使表单项可用

1）onscroll：该事件会在元素的滚动条滚动时触发

2）disabled属性可以设置一个元素是否禁用，

如果设置为true，则元素禁用

如果设置为false，则元素可用

# 事件

## 13、事件对象

当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为**实参**传递进响应函数,

在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标  键盘哪个按键被按下  鼠标滚轮滚动的方向。。。

~~~js
对象.onmousemove = function(event){}
~~~

> onmousemove：该事件将会在鼠标在元素中移动时被触发

clientX可以获取鼠标指针的水平坐标，cilentY可以获取鼠标指针的垂直坐标

### 1）clientX和clientY于获取鼠标在当前的可见窗口的坐标

### 2）pageX和pageY可以获取鼠标相对于当前页面的坐标

> 解决事件对象的兼容性问题：event = event || window.event;

## 14、案例-鼠标跟随盒子移动

（1）使用事件对象，获得鼠标坐标

（2）设置div的偏移量，要开启box1的绝对定位，鼠标才能跟着盒子移动

（3）将鼠标坐标与div偏移量相同

（4）div的偏移量是相对于整个页面，所以给页面添加onmousemove，而不是给box1添加

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1 {
            width: 100px;
            height: 100px;
            background-color: pink;
            /* 开启box1的绝对定位 */
            position: absolute;
            /* top: 0; left: 0; */
        }
    </style>
    <script>
        window.onload = function () {
            // 使div可以跟随鼠标移动
            var box1 = document.getElementById('box1')
            document.onmousemove = function (e) {
                // 获得鼠标坐标
                var x = e.pageX
                var y = e.pageY
                console.log(`x= ${x},y = ${y}`)
                // 设置div的偏移量
                box1.style.left = x +'px'
                box1.style.top = y +'px'
              //如果要鼠标坐标用clientX/clientX，要设置滚动条距离
                // var sl = document.documentElement.scrollLeft
                // var st = document.documentElement.scrollTop
                // var x = e.clientX
                // var y = e.clientY
                // box1.style.left = x + sl +'px'
                // box1.style.top = y + st +'px'
            }
        }
    </script>
</head>
<body style="height: 1000px ;width: 2000px">
    <div id="box1"></div>
</body>
</html>
~~~

## 15、事件冒泡（Bubble）

所谓的冒泡指的就是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发

在开发中大部分情况冒泡都是有用的,如果不希望发生事件冒泡可以通过事件对象来取消冒泡

### 取消冒泡：event.cancelBubble = true;

可以将事件对象的cancelBubble设置为true，即可取消冒泡

## 16、事件委派

为每一个超链接都绑定一个单击响应函数，这里我们为每一个超链接都绑定了一个单击响应函数，这种操作比较麻烦，而且这些操作只能为已有的超链接设置事件，而新添加的超链接必须重新绑定

我们希望，只绑定一次事件，即可应用到多个的元素上，即使元素是后添加的，我们可以尝试将其绑定给元素的共同的祖先元素

事件委派是指将事件统一绑定给元素的共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素，从而通过祖先元素的响应函数来处理事件。

事件委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能

 target：event中的target表示的触发事件的对象

### e.target

## 17、事件绑定

使用 对象.事件 = 函数 的形式绑定响应函数，它只能同时为一个元素的一个事件绑定一个响应函数，不能绑定多个，如果绑定了多个，则后边会覆盖掉前边的

### （1）addEventListener()

通过这个方法也可以为元素绑定响应函数

 参数：

1.事件的字符串，不要on

2.回调函数，当事件触发时该函数会被调用

3.是否在捕获阶段触发事件，需要一个布尔值，一般都传false

使用addEventListener()可以同时为一个元素的相同事件同时绑定多个响应函数，这样当事件被触发时，响应函数将会按照函数的绑定顺序执行

~~~js
btn01.addEventListener("click",function(){
  				alert(1);
},false);
~~~

### （2）attachEvent()

参数：

1.事件的字符串，要on

2.回调函数

这个方法也可以同时为一个事件绑定多个处理函数，不同的是它是后绑定先执行，执行顺序和addEventListener()相反

~~~js
btn01.attachEvent("onclick",function(){
  alert(1);
});
~~~

### （3）bind函数

定义一个函数，用来为指定元素绑定响应函数

参数：

obj 要绑定事件的对象

eventStr 事件的字符串(不要on)

callback 回调函数

>addEventListener()中的this，是绑定事件的对象
>
>attachEvent()中的this，是window
>
>需要统一两个方法this

~~~js
function bind(obj , eventStr , callback){
          if(obj.addEventListener){
                //大部分浏览器兼容的方式
                obj.addEventListener(eventStr , callback , false);
          }else{
                   //this是谁由调用方式决定
                    //callback.call(obj)
            		//IE8及以下
                obj.attachEvent("on"+eventStr , function(){
                      //在匿名函数中调用回调函数
                      callback.call(obj);
                });
          }
}
~~~

## 18、事件传播

### （1）捕获阶段

在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件（由外向内传播的）

### （2）目标阶段

事件捕获到目标元素，捕获结束开始在目标元素上触发事件

### （3）冒泡阶段

事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件（由内向外传播）

> 如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为true
>
> 一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是false

## 19、案例-鼠标拖拽

拖拽box1元素的流程：

（1）当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown

（2）当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove

- 获得鼠标坐标
- 设置div的偏移量

（3）当鼠标松开时，被拖拽元素固定在当前位置 onmouseup

- 取消onmousemove事件
- 取消onmouseup事件 

>（1）onmousedown按下事件中实现onmousemove移动和onmouseup松开事件
>
>（2）当我们拖拽一个网页中的内容时，浏览器会默认去搜索引擎中搜索内容，此时会导致拖拽功能的异常，这个是浏览器提供的默认行为，如果不希望发生这个行为，则可以通过return false来取消默认行为
>
>（3）鼠标按下时，开始拖拽鼠标始终在元素左上角，我们希望点哪儿鼠标就在哪儿，即鼠标和图片元素的相对位置是不变的
>
>div的偏移量 鼠标.pageX- 元素.offsetLeft
>
>div的偏移量 鼠标.pageY - 元素.offsetTop

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
        }
        #box2 {
            width: 100px; height: 100px;
            background-color: skyblue;
            position: absolute;
            left: 200px; top: 200px;
        }
    </style>
    <script>
        window.onload = function () {
            // 1、鼠标按下
            var box1 = document.getElementById('box1')
            box1.onmousedown = function (e) {
                console.log('开始拖拽')
             //div的偏移量
                var ol = e.pageX - box1.offsetLeft
                var ot = e.pageY - box1.offsetTop
                // 2、鼠标移动
                document.onmousemove = function (e) {
                    console.log('鼠标移动');
                    var x = e.pageX
                    var y = e.pageY
                    box1.style.left = x - ol + 'px'
                    box1.style.top = y - ot + 'px'
                }
                // 3、鼠标松开
                document.onmouseup = function () {
                    document.onmousemove = null
                    document.onmouseup = null
                    console.log('鼠标松开');
                }
            }
            return false;
        }
    </script>
</head>
<body>
    我是一段文字
    <div id="box1"></div>
    <div id="box2"></div>
</body>
</html>
~~~

## 20、滚轮事件

### （1）onmousewheel

鼠标滚轮滚动的事件，会在滚轮滚动时触发

### （2）e.wheelDelta 

可以获取鼠标滚轮滚动的方向

向上滚 120   向下滚 -120，wheelDelta这个值我们不看大小，只看正负

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
        }
    </style>
    <script>
        window.onload = function () {
            var box1 = document.getElementById('box1')
            box1.onmousewheel = function(e) {
                // console.log(e.wheelDelta);
                // 当鼠标滚轮向下滚动时，box1变长
                // 当滚轮向上滚动时，box1变短
                if(e.wheelDelta > 0) {
                    box1.style.height =box1.clientHeight - 10 +'px'
                } else {
                    box1.style.height =box1.clientHeight + 10 +'px'
                }
                return false
            }
        }
    </script>
</head>
<body style="height: 1000px;">
    <div id="box1"></div>
</body>
</html>
~~~

当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动，这是浏览器的默认行为，如果不希望发生，则可以取消默认行为，return false

> 火狐浏览器：
>
> （1）使用 DOMMouseScroll 来绑定滚动事件，注意该事件需要通过addEventListener()函数来绑定
>
> （2）使用event.detail来获取滚动的方向，向上滚 -3  向下滚 3

## 21、键盘事件

键盘事件一般都会绑定给一些可以获取到焦点的对象或者是document

### （1）onkeydown

按键被按下

> 对于onkeydown来说如果一直按着某个按键不松手，则事件会一直触发
>
> 当onkeydown连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常的快,这种设计是为了防止误操作的发生。

### （2）onkeyup

按键被松开

### （3）keyCode

可以通过keyCode来获取按键的编码，通过它可以判断哪个按键被按下

### （4）altKey、ctrlKey、shiftKey

这个三个用来判断alt ctrl 和 shift是否被按下

如果按下则返回true，否则返回false

### （5）练习

1）判断y和ctrl是否同时被按下

~~~js
if(e.keyCode === 89 && e.ctrlKey){
          console.log("ctrl和y都被按下了");
}
~~~

2）文本框不能输入数字

数字按键的编码是 48 - 57

~~~js
// console.log(e.keyCode);
if (e.keyCode >= 48 && e.keyCode <= 57) {
  return false
}
~~~

在文本框中输入内容，属于onkeydown的默认行为，如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中，即 return false

### （6）案例-键盘移动div

使div可以根据不同的方向键向不同的方向移动

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
        }
    </style>
    <script>
        window.onload = function() {
                document.onkeydown = function (e) {
                    // console.log(e.keyCode);
                  // 定义移动速度
                    var speed = 10
                    //按下ctrl加速
                    if (e.ctrlKey) {
                        speed = 300
                    }
                    // 上38 右39 下40 左37
                    switch (e.keyCode) {
                        case 38:
                            box1.style.top = box1.offsetTop - speed + 'px'
                            break
                        case 40:
                            box1.style.top = box1.offsetTop + speed + 'px'
                            break
                        case 37:
                            box1.style.left = box1.offsetLeft - speed + 'px'
                            break
                        case 39:
                            box1.style.left = box1.offsetLeft + speed + 'px'
                            break
                    }
                }
        }
    </script>
</head>
<body>
    <div id="box1"></div>
</body>
</html>
~~~

# BOM

## 22、BOM

浏览器对象模型

BOM可以使我们通过JS来操作浏览器，在BOM中为我们提供了一组对象，用来完成对浏览器的操作

## 23、BOM对象

### （1）Window

代表的是整个浏览器的窗口，同时window也是网页中的全局对象

### （2）Navigator

代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器

**1）**userAgent来判断浏览器的信息

userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，不同的浏览器会有不同的userAgent

> Chrome的userAgent：（navigator.userAgent）
>
> Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36

~~~js
if (/chrome/i.test(navigator.userAgent)) {
            console.log('你是chrome');
}
~~~

**2）**ActiveXObject，通过一些浏览器中特有的对象，来判断浏览器的信息

### （3）Location

代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面

**1）**assign()

用来跳转到其他的页面，作用和直接修改location一样

location.assign("http://www.baidu.com")  =>  location = "http://www.baidu.com";

**2）**reload()

用于重新加载当前页面，作用和刷新按钮一样

如果在方法中传递一个true，作为参数，则会强制清空缓存刷新页面  location.reload(true);  =>   ctrl + F5

**3）**replace()

可以使用一个新的页面替换当前页面，调用完毕也会跳转页面

不会生成历史记录，不能使用回退按钮回退

### （4）History

代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录

由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页，而且该操作只在当次访问时有效

**对象可以用来操作浏览器向前或向后翻页**

**1）**length

属性，可以获取到当成访问的链接数量（history.length）

**2）**back()

可以用来回退到上一个页面，作用和浏览器的回退按钮一样（history.back()）

**3）**forward()

可以跳转下一个页面，作用和浏览器的前进按钮一样（history.forward()）

**4）**go()

可以用来跳转到指定的页面（history.go(-2)）

>它需要一个整数作为参数
>
>1:表示向前跳转一个页面 相当于forward()			2:表示向前跳转两个页面
>
>-1:表示向后跳转一个页面						-2:表示向后跳转两个页面

### （5）Screen

代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息

## 24、定时调用

### （1）setInterval()

定时调用，可以将一个函数，每隔一段时间执行一次

参数：

1）回调函数，该函数会每隔一段时间被调用一次

2）每次调用间隔的时间，单位是毫秒

返回值：

1）返回一个Number类型的数据

2）这个数字用来作为定时器的唯一标识

### （2）clearInterval()

可以用来关闭一个定时器

方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器

### （3）案例1-自动切换图片

（1）创建一个数组来保存图片的路径、创建一个变量用来保存当前图片的索引

（2）判断索引是否超过最大索引

1）if (index > imgArr.length -1) {index = 0 }

**2）**index %= imgArr.length

（3）因btn01,btn02作用域不同，将timer设置为全局变量

> 目前，我们每点击一次按钮，就会开启一个定时器，点击多次就会开启多个定时器，这就导致图片的切换速度过快，并且我们只能关闭最后一次开启的定时器

（4）在开启定时器之前，需要将当前元素上的其他定时器关闭

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var img = document.getElementsByTagName('img')[0]
            imgArr = ["./img/1.jpg", "./img/2.jpg", "./img/3.jpg", "./img/4.jpg", "./img/5.jpg"]
            var index = 0
            // 定义一个变量，用来保存定时器的标识
            var timer
            var btn01 = document.getElementById('btn01')
            btn01.onclick = function () {
				clearInterval(timer);
                timer = setInterval(function() {
                index++
                console.log(index);
                index %= imgArr.length
                img.src = imgArr[index]
            },1000)
            }
            var btn02 = document.getElementById('btn02')
            btn02.onclick = function () {
                clearInterval(timer)
            }
        }
    </script>
</head>
<body>
    <img src="./img/1.jpg" alt="">
    <br>
    <br>
    <button id="btn01">开始</button>
    <button id="btn02">停止</button>
</body>
</html>
~~~

### （4）案例2-键盘移动div

1）创建一个变量表示方向，通过修改dir来影响移动的方向

2）开启一个定时器，来控制div的移动

3）为document绑定一个按键按下的事件

4）当按键松开时，div不再移动

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
        }
    </style>
    <script>
        window.onload = function() {
            //使div可以根据不同的方向键向不同的方向移动
            // 定义移动速度
            var speed = 10
            // 定义移动方向
            var dir 
            setInterval(function() {
                // 上38 右39 下40 左37
                switch (dir) {
                    case 38:
                        box1.style.top = box1.offsetTop - speed + 'px'
                        break
                    case 40:
                        box1.style.top = box1.offsetTop + speed + 'px'
                        break
                    case 37:
                        box1.style.left = box1.offsetLeft - speed + 'px'
                        break
                    case 39:
                        box1.style.left = box1.offsetLeft + speed + 'px'
                        break
                }
            },30)
            document.onkeydown = function (e) {
                if (e.ctrlKey) {
                    speed = 100
                } else {
                    speed = 10
                }
                dir = e.keyCode
            }
            document.onkeyup = function (e) {
                dir = 0
            }
        }
    </script>
</head>
<body>
    <div id="box1"></div>
</body>
</html>
~~~

## 25、延时调用

### （1）setTimeout()

延时调用一个函数不马上执行，而是隔一段时间以后在执行，而且只会执行一次

### （2）clearTimeout()

使用clearTimeout()来关闭一个延时调用

### （3）延时调用和定时调用的区别

定时调用会执行多次，而延时调用只会执行一次

## 26、定时器案例

点击按钮以后，使box1向右移动（left值增大）

点击按钮以后，使box1向左移动（left值减小）

### （1）常规做法

**（  ！）**重复点击按钮，定时函数持续执行，使得速度变快 

=> 在定时函数前，关闭上一个定时器

1）var timer 全局变量，在onload里

2）定义getStyle函数，获得指定元素的样式，=> 当前位置

3）开启定时器，用来执行动画效果

- 获取box1的原来的left值、在旧值的基础上增加速度、将新值设置给box1
- 当元素移动到500px时，使其停止执行动画（达到目标，关闭定时器）
- 判断newValue是否大于500，设置newValue最大值始终为500

4）向左移动，同理

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
        }
    </style>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1')
            var btn01 = document.getElementById('btn01')
			//定义一个变量，用来保存定时器的标识
            var timer 
            //点击按钮以后，使box1向右移动（left值增大）
            btn01.onclick = function () {
                //关闭上一个定时器
                clearInterval(timer)
                //开启一个定时器，用来执行动画效果
                timer = setInterval(function () {
                    var oldValue = parseInt(getStyle(box1, 'left'))
                    var newValue = oldValue + 10
                    // 从0向500移动，使newValue最大值始终为500
                    if (newValue > 500) {
                        newValue = 500
                    }
                    box1.style.left = newValue + 'px'
                    console.log(newValue);
                  //当元素移动到500px时，使其停止执行动画，关闭定时器
                    if (newValue > 500) {
                        clearInterval(timer)
                    }
                },30)
            }
            //点击按钮以后，使box1向左移动（left值减小）
            var btn02 = document.getElementById('btn02')
            btn02.onclick = function() {
                clearInterval(timer)
                timer = setInterval(function() {
                    var oldValue = parseInt(getStyle(box1, 'left'))
                    var newValue = oldValue - 10
                    if (newValue < 0) {
                        newValue = 0
                    }
                    box1.style.left = newValue + 'px'
                    if (newValue < 0) {
                        clearInterval(timer)
                    }
                },30)
            }
        }
    	// 获得指定元素的当前的样式
        function getStyle(obj, name) {
            return getComputedStyle(obj , null)[name]
        }
    </script>
</head>
<body>
    <button id="btn01">点击box1,按钮向右移动</button>
    <button id="btn02">点击box1,按钮向左移动</button>
    <br>
    <br>
    <div id="box1"></div>

    <div style="width: 0; height: 500px;border-left: 1px solid #000;position: absolute; left: 500px; top: 0;"></div>
</body>
</html>
~~~

### （2）封装函数

**1）**var timer全局变量，放在onload外面

**2）**尝试创建一个可以执行简单动画的函数，

参数：

- obj:要执行动画的对象，
- target:执行动画的目标位置，
- speed:移动的速度(正数向右移动，负数向左移动)

**3）**判断newValue，清除定时器，不再移动

- 向左 speed为负值，newValue小于targe
- 向右 speed为正值,newValue大于target

**4）**判断speed正负，获取元素目前的位置（current），放在定时器外面

- 如果从0 向 500移动，则speed为正，
- 如果从800向0移动，则speed为负

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
        }
    </style>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1')
            var btn01 = document.getElementById('btn01')
            //点击按钮以后，使box1向右移动（left值增大）
            btn01.onclick = function () {
                move(box1, 500, 10)
            }
            //点击按钮以后，使box1向左移动（left值减小）
            var btn02 = document.getElementById('btn02')
            btn02.onclick = function() {
                move(box1, 0, 10)
            }
        }
        //定义一个变量，用来保存定时器的标识
        var timer 
        function move(obj, target, speed) {
            //关闭上一个定时器
            clearInterval(timer)
            // 获取当前位置
            var current = parseInt(getStyle(obj, 'left'))
            if (current > target) {
                speed = -speed
            }
            // 开启一个定时器，用来执行动画效果
            timer = setInterval(function() {
                var oldValue = parseInt(getStyle(obj, 'left'))
                var newValue = oldValue + speed
                console.log(newValue);
                // 判断newValue是否大于500
                // 向左，需要判断newValue是否小于target
                // 向右 ，需要判断newValue是否大于target
                if((speed < 0 && newValue < target) || (speed > 0 && newValue > target)){
                    newValue = target
                }
                obj.style.left = newValue + 'px'
                // 当元素移动到指定位置时,关闭定时器
                if (newValue == target) {
                    clearInterval(timer)
                }
            },30)
        }
        function getStyle(obj, name) {
            return getComputedStyle(obj , null)[name]
        }
    </script>
</head>
<body>
    <button id="btn01">点击box1,按钮向右移动</button>
    <button id="btn02">点击box1,按钮向左移动</button>
    <br>
    <br>
    <div id="box1"></div>

    <div style="width: 0; height: 500px;border-left: 1px solid #000;position: absolute; left: 500px; top: 0;"></div>
</body>
</html>
~~~

### （3）执行多种动画效果

上下左右移动、变宽变高

**1）**向执行动画的对象中添加一个timer属性，用来保存它自己的定时器的标识，obj.timer

> 使用全局变量var timer，使不同的定时器之间有干扰，点击盒子1，再点击盒子2，盒子1会停下，所以一个动画的执行会影响另一个，需要自己保存自己的定时器

**2）**新增一个参数，callback:回调函数，这个函数将会在动画执行完毕以后执行

**3）**动画执行完毕，调用回调函数，

callback && callback()：如果回调函数存在，则执行该回调函数。

**4）**将两个函数提取成外部文件，新建一个js文件，使用时引入

~~~js
//尝试创建一个可以执行简单动画的函数
/*
 * 参数：
 * 	obj:要执行动画的对象
 * 	attr:要执行动画的样式，比如：left top width height
 * 	target:执行动画的目标位置
 * 	speed:移动的速度(正数向右移动，负数向左移动)
 *  callback:回调函数，这个函数将会在动画执行完毕以后执行
 */
//定义一个变量，用来保存定时器的标识
// var timer 
function move(obj, attr, target, speed, callback) {
    //关闭上一个定时器
    clearInterval(obj.timer)
    // 获取元素目前的位置
    var current = parseInt(getStyle(obj, attr))
    //判断速度的正负值
    if (current > target) {
        speed = -speed
    }
    // 开启一个定时器，用来执行动画效果
    // 向执行动画的对象中添加一个timer属性，用来保存它自己的定时器的标识
    obj.timer = setInterval(function() {
        var oldValue = parseInt(getStyle(obj, attr))
        var newValue = oldValue + speed
        console.log(newValue);
        // 判断newValue是否大于500
        // 向左，需要判断newValue是否小于target
        // 向右 ，需要判断newValue是否大于target
        if((speed < 0 && newValue < target) || (speed > 0 && newValue > target)){
            newValue = target
        }
        obj.style[attr] = newValue + 'px'
        // 当元素移动到指定位置时,关闭定时器
        if (newValue == target) {
            clearInterval(obj.timer)
            //动画执行完毕，调用回调函数
            callback && callback()
        }
    },30)
}
/*
 * 定义一个函数，用来获取指定元素的当前的样式
 * 参数：
 * 		obj 要获取样式的元素
 * 		name 要获取的样式名
 */
function getStyle(obj, name) {
    return getComputedStyle(obj , null)[name]
}
~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        #box1 {
            width: 100px; height: 100px;
            background-color: pink;
            position: absolute;
            left: 0;
        }
        #box2 {
            width: 100px; height: 100px;
            background-color: skyblue;
            position: absolute;
            left: 0; top: 200px;
        }
    </style>
    <script src="./js/donghua.js"></script>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1')
            var btn01 = document.getElementById('btn01')
            //点击按钮以后，使box1向右移动（left值增大）
            btn01.onclick = function () {
                move(box1, 'left', 500, 10)
            }
            //点击按钮以后，使box1向左移动（left值减小）
            var btn02 = document.getElementById('btn02')
            btn02.onclick = function() {
                move(box1,'left', 0, 10)
            }

            var box2 = document.getElementById('box2')
            //点击按钮以后，使box2向右移动（left值增大）
            var btn03 = document.getElementById('btn03')
            btn03.onclick = function() {
                move(box2,'left', 500, 15)
            }
            //点击测试按钮，上下左右移动
            var btn04 = document.getElementById('btn04')
            btn04.onclick = function() {
                // move(box2,'height' ,500, 20)
                move(box2,'width', 500, 10, function() {
                    move(box2,'height' ,500, 20, function () {
                        move(box2,'top' ,0, 20, function () {
                            move(box2,'width' ,100, 20, function () {
                                move(box2,'height' ,100, 20, function () {
                                    move(box2,'top' ,200, 20, function () {})
                                })
                            })
                        })
                    })
                })
            }
        }
    </script>
</head>
<body>
    <button id="btn01">点击box1,按钮向右移动</button>
    <button id="btn02">点击box1,按钮向左移动</button>
    <button id="btn03">点击box2,按钮向右移动</button>
    <button id="btn04">测试</button>
    <br>
    <br>
    <div id="box1"></div>
    <div id="box2"></div>

    <div style="width: 0; height: 1000px;border-left: 1px solid #000;position: absolute; left: 500px; top: 0;"></div>
</body>
</html>
~~~

## 27、轮播图（难）

## 28、类

通过style属性来修改元素的样式，每修改一个样式，浏览器就需要重新渲染一次页面，

这样的执行的性能是比较差的，而且这种形式当我们要修改多个样式时，也不太方便，我希望一行代码，可以同时修改多个样式

### （1）元素.className = '类名'

我们可以通过修改元素的class属性来间接的修改样式， 这样一来，我们只需要修改一次，即可同时修改多个样式，浏览器只需要重新渲染页面一次，性能比较好，并且这种方式，可以使表现和行为进一步的分离

### （2）定义函数：添加、查找、删除、切换

1）定义一个函数，用来向一个元素中添加指定的class属性值

参数:

- obj 要添加class属性的元素
- cn 要添加的class值

~~~js
function addClass(obj , cn){
				//检查obj中是否含有cn
				if(!hasClass(obj , cn)){
					obj.className += " "+cn;
				}
}
~~~

2）判断一个元素中是否含有指定的class属性值，如果有该class，则返回true，没有则返回false

~~~js
function hasClass(obj , cn){
				//判断obj中有没有cn class
				//创建一个正则表达式
				//var reg = /\bb2\b/;
				var reg = new RegExp("\\b"+cn+"\\b");
				return reg.test(obj.className);
}
~~~

3）删除一个元素中的指定的class属性

~~~js
function removeClass(obj , cn){
				//创建一个正则表达式
				var reg = new RegExp("\\b"+cn+"\\b");
				//删除class
				obj.className = obj.className.replace(reg , "");
}
~~~

4）toggleClass可以用来切换一个类

- 如果元素中具有该类，则删除

- 如果元素中没有该类，则添加

~~~js
function toggleClass(obj , cn){
				//判断obj中是否含有cn
				if(hasClass(obj , cn)){
					removeClass(obj , cn);//有，则删除
				}else{
					addClass(obj , cn);//没有，则添加
				}
}
~~~

> （1）追加类：元素.classList.add('类名')
>
> （2）删除类：元素.classList.remove('类名')
>
> （3）切换类：元素.classList.toggle('类名')
>

## **29、案例-二级菜单**

我们的每一个菜单都是一个div，当div具有collapsed这个类时，div就是折叠的状态，当div没有这个类是，div就是展开的状态

~~~js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        a {
            text-decoration: none;
            color: black;
        }
        .menu {
            width: 120px;
            margin: 0 auto;
            font-size: 14px;
        }
        .menu div {
            background-color: deeppink;
            overflow: hidden;
        }
        .menu h4 {
            padding: 5px;
        }
        .menu a {
            display: block;
            padding: 5px 12px;
            background-color: pink;
            border-bottom: 1px solid #ccc;
        }
        .menu a:hover {
            background-color: lightpink;
        }
        /* 添加的类，使之折叠 */
        .menu .collapsed {height: 25px;}
    </style>
</head>
<body>
    <div class="menu">
        <div class="collapsed">
            <h4>白敬亭</h4>
            <a href="#">1</a>
            <a href="#">2</a>
            <a href="#">3</a>
            <a href="#">4</a>
            <a href="#">5</a>
        </div>
        <div class="collapsed">
            <h4>杨超越</h4>
            <a href="#">1</a>
            <a href="#">2</a>
            <a href="#">3</a>
            <a href="#">4</a>
            <a href="#">5</a>
        </div>
        <div class="collapsed">
            <h4>温霜降</h4>
            <a href="#">1</a>
            <a href="#">2</a>
            <a href="#">3</a>
            <a href="#">4</a>
            <a href="#">5</a>
        </div>
        <div class="collapsed">
            <h4>桑延</h4>
            <a href="#">1</a>
            <a href="#">2</a>
            <a href="#">3</a>
            <a href="#">4</a>
            <a href="#">5</a>
        </div>
    </div>
    <script>
        var h4 = document.querySelectorAll('h4')
        // 定义一个变量，来保存当前打开的菜单
        var openDiv = h4[0].parentNode
        //console.log(openDiv);
        for(var i = 0; i < h4.length; i++){
            h4[i].onclick = function() {
                //console.log(this.parentNode);
                // this代表我当前点击的h4
                var parentDiv = this.parentNode
                // 切换菜单的显示状态
                parentDiv.classList.toggle('collapsed')
                if(openDiv != parentDiv) {
                    // 打开菜单以后，应该关闭之前打开的菜单
                    openDiv.classList.add('collapsed')
                    openDiv = parentDiv
                }
            }
        }
</script>
</body>
</html>
~~~

## 30、JSON

JS中的对象只有JS自己认识，其他的语言都不认识

**对象**：对象作为一种复杂数据类型，表示的是一组无序的键值对儿。而每个键值对儿中的值可以是简单值，也可以是复杂数据类型的值。

**数组**：数组也是一种复杂数据类型，表示一组有序的值的列表，可以通过数值索引来访问其中的值。数组的值也可以是任意类型——简单值、对象或数组。

JSON就是一个特殊格式的字符串，这个字符串可以被任意的语言所识别，并且可以转换为任意语言中的对象，JSON在开发中主要用来数据的交互

JSON和JS对象的格式一样，只不过JSON字符串中的属性名必须加双引号，其他的和JS语法一致

> 对象的属性必须加双引号

~~~js
// 对象字面量
var person = { 
     name: "Nicholas", 
     age: 29 
}; 
// JSON
var object = { 
     "name": "Nicholas", 
     "age": 29 
};
~~~



### （1）JSON分类：

- 对象 {}
- 数组 []

### （2）JSON中允许的值：

字符串、数值、布尔值、null、对象、数组

>将JSON字符串转换为JS中的对象
>
>在JS中，为我们提供了一个工具类，就叫JSON，这个对象可以帮助我们将一个JSON转换为JS对象，也可以将一个JS对象转换为JSON

### （3）JSON --> js对象

JSON.parse()

- 可以将以JSON字符串转换为js对象
- 它需要一个JSON字符串作为参数，会将该字符串转换为JS对象并返回

### （4）JS对象 --> JSON

JSON.stringify()

- 可以将一个JS对象转换为JSON字符串
- 需要一个js对象作为参数，会返回一个JSON字符串


### （5）eval()

这个函数可以用来执行一段字符串形式的JS代码，并将执行结果返回

如果使用eval()执行的字符串中含有{},它会将{}当成是代码块，如果不希望将其当成代码块解析，则需要在字符串前后各加一个()	=>	eval("("+str+")")

**尽量不使用eval()**



