# DOM
## DOM简单学习
功能：控制（增删改查）HTML文档的内容  
代码：获取页面标签（元素）对象 Element
  * document.getElementById("id值")：通过元素的id获取元素对象
操作Element对象
  * 修改属性值
    * 1.明确获取的对象是哪一个
    * 2.查看API文档，找其中有哪些属性可以设置
  * 修改标签体内容
    * 属性：innerHTML
    * 1.获取元素对象
    * 2.使用innerHTML属性修改标签体内容

## 事件简单学习
功能：某些组件被执行某些操作后，触发某些代码的执行  
如何绑定事件
  * 1.直接在HTML标签上，指定事件的属性，属性值就是JS代码
    * 事件：onclick --- 单击事件
  * 2.通过JS来获取元素对象，指定事件属性，设置一个函数

```ruby
练习：点击更换内容
<body>
<h1 id="title" class="1">TalentCan</h1>
<script>
    /*
    * 获取内容资源
    * 绑定单击事件
    * 每次点击切换内容
    * */
    var element = document.getElementById("title");
    var flag = false;
    element.onclick = function () {
        if(flag){
            element.innerHTML = "shuaishuaican"
            flag = false;
        }else{
            element.innerHTML = "TalentCan"
            flag = true;
        }
    }
</script>
</body>
```

# BOM
概念：Brower Object Model 浏览器对象模型
  * 将浏览器的各个组成部分封装成对象：window窗口对象，浏览器对象，地址栏对象（Location），历史记录对象（History），显示器屏幕对象（Screen）
  * 其中window窗口对象包括地址栏对象（Location），历史记录对象（History，可以记录访问过的网站，可以访问前一个和后一个网站）
组成
  * window：窗口对象
  * Location：地址栏对象
  * History：历史记录对象
  * Navigator：浏览器对象
  * Screen：显示器屏幕对象

## window：窗口对象
1.创建
2.方法
  * 1.与弹出框有关的方法
    * alert()：显示带有一段消息和一个确认按钮的警告框
    * confirm()：显示带有一段消息以及确认按钮和取消按钮的对话框
      * 会有确认和取消两个按钮，如果用户点击确认按钮，则方法返回true，如果用户点击取消按钮，则方法返回false
    * prompt()：显示可提示用户输入的对话框
      * 返回值：获取用户输入的值
  * 2.与打开关闭有关的方法
    * close()：关闭浏览器窗口
      * 谁调用close方法，就关闭谁
    * open()：打开一个新的浏览器窗口，如果里面没有参数就打开一个空白窗口，如果有参数就是打开参数地址的网页
  ```ruby
  <body>
  <input id="open" type="button" value="打开新窗口">
  <input id="close" type="button" value="关闭新窗口">
  <script>
    var openbtn = document.getElementById("open");
    //接收打开窗口的返回值，作为新窗口对象，用于关闭新窗口
    var newwindow;
    openbtn.onclick = function () {
        newwindow = open("https://www.baidu.com");
    }
    var closebtn = document.getElementById("close");
    closebtn.onclick = function () {
        newwindow.close();
    }
  </script>
  </body>
  ```
  * 3.与定时器有关的方法
    * setTimeout()：在指定的毫秒数后调用函数或计算表达式
      * 参数
        * JS代码或者方法对象
        * 毫秒值
      * 返回值：唯一标识，用于取消定时器
    * clearTimeout()：取消由setTimeout()方法设置的timeout
    * setInterval()按照指定的周期（以毫秒计）来调用函数或计算表达式
      * 参数
        * JS代码或者方法对象
        * 毫秒值
      * 返回值：唯一标识，用于取消定时器 
    * clearInterval()取消由setInterval()设置的timeout
  ```ruby
  //一次性计时器
  var time = setTimeout("fun();",3000);
  clearTimeout(time);
  //setTimeout(fun(),3000);
  function fun(){
      alert('boom~~');
  }
  //循环计时器
  var time2 = setInterval(fun,3000);
  clearInterval(time2);
  ```
```ruby
//轮播图案例
<body>
    <img id="img" src="imgs/轮播图1.png" width="100%">
</body>
<script>
    /*
    * 分析：
    * 1.在页面上使用imgs标签展示图片
    * 2.定义一个方法，修改图片对象的src
    * 3.定义一个定时器，每隔几秒调用一次方法
    * */
    var num = 1;
    //修改图片src属性
    function fun() {
        num++;
        if(num > 3)
            num = 1;
        //获取img对象
        var img = document.getElementById("img");
        img.src = "imgs/轮播图"+num + ".png";
    }
    //定义定时器
    setInterval(fun,3000);
</script>
```
3.属性  
  * 1.获取其他BOM对象
    * Location：地址栏对象
    * History：历史记录对象，直接调用，如：var h1 = window.history;或 var h2 = history;因为window可以省略
    * Navigator：浏览器对象
    * Screen：显示器屏幕对象
  * 2.获取DOM对象
    * document：window.document.getElementById();==document.getElementById();因为window可以省略
4.特点
  * window对象不需要创建可以直接使用window使用。window.方法名();
  * window引用可以省略。方法名();

## Location：地址栏对象
1.创建（获取）
  * window.location
  * location
2.方法
  * reload()：重新加载当前文档，刷新页面
3.属性
  * href：设置或返回完整的URL，设置或返回浏览器窗口的路径
```ruby
<body>
    <input type="button" id="btn" value="刷新">
    <input type="button" id="gobaidu" value="去百度">
</body>
<script>
    var id = document.getElementById("btn");
    btn.onclick = function () {
        location.reload();
    }
    var href = location.href;
    alert(href);

    var id = document.getElementById("gobaidu");
    gobaidu.onclick = function () {
        location.href = "https://www.baidu.com";
    }
</script>
```
```ruby
//自动跳转到首页
<head>
    <meta charset="UTF-8">
    <title>自动跳转</title>
    <style>
    //设置字体的颜色和位置
        p{
            text-align: center;
        }
        span{
            color: red;
        }
    </style>
</head>
<body>
<p>
    <span id="span">5</span>秒之后，自动跳转到首页
</p>
</body>
<script>
    /*
    * 分析
    * 1.显示页面效果
    * 2.倒计时读秒效果实现
    *   2.1定义一个方法，获取span标签，修改span标签体内容，时间
    *   2.2定义一个定时器，1秒执行一次该方法
    * 3.在方法中判断时间小于0，则跳转到百度首页
    * */
    var id = document.getElementById("span");
    var num = 5;
    function showtime() {
        num--;
        if(num<=0){
            location.href = "https://www.baidu.com";
        }
        id.innerHTML = num + "";

    }
    setInterval(showtime,1000);
</script>
```
## History：历史记录对象
1.创建（获取）
  * window.history
  * history
2.方法
  * back()：加载history列表中前一URL
  * forward()：加载history列表中下一个URL
  * go(参数)：加载history列表中某一个具体页面
    * 正数：前进几个历史记录
    * 负数：后退几个历史记录
3.属性
  * length：返回当前窗口历史列表的URL数量
```ruby
<body>
    <input type="button" id="btn1" value="获取历史记录个数">
    <a href="轮播图.html">轮播图</a>
    <input type="button" id="forward" value="前进">
</body>
<script>
    var id1 = document.getElementById("btn1");
    btn1.onclick = function () {
        var length = history.length;
        alert("历史记录的个数为" + length);
    }
    var forward = document.getElementById("forward");
    forward.onclick = function () {
        // history.forward();
        history.go(1);
    }
</script>

//在轮播图案例中添加后退按钮
<input type="button" id="back" value="后退">
var back = document.getElementById("back");
    back.onclick = function () {
        // history.back();
        history.go(-1);
    }
```
# DOM
概念：document object model 文档对象模型
  * 将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CURD的动态操作
W3C DOM标准被分为3个不同的部分
  * 核心DOM：针对任何结构化文档的标准模型
    * Document：文档对象
    * Element：元素对象
    * Attribute：属性对象
    * Text：文本对象
    * Comment：注释对象
    * Node：节点对象，其他5个的父对象
  * XMLDOM：针对XML文档的标准模型
  * HTMLDOM：针对HTML文档的标准模型

## 核心DOM模型
1.Document：文档对象
  * 创建（获取）：在HTML DOM模型中可以使用window对象来获取
    * window.document
    * docunment
  * 方法：可以去查XML DOM的方法，因为HTML DOM中的方式是对核心DOM的方法进行了修改
    * 获取element对象
      * getElementById()：根据id属性值获取元素对象。id属性值一般唯一
      * getElementByTagName()：根据元素名称获取元素对象们。返回值是一个数组
      * getElementByClassName()：根据class属性值获取元素对象们。返回值是一个数组
      * getElementByName()：根据name属性值获取元素对象们。返回值是一个数组
    * 创建其他DOM对象
      * createAttribute(name)
      * createComment(name)
      * createText(name)
      * createElement(name)
  * 属性
2.Element：元素对象
  * 创建/获取：通过
  * 方法
    * removeAttribute()：删除属性
    * setAttribute()：设置属性
3.Node：节点对象，其他5个的父对象
  * 特点：所有DOM对象都可以被认为是一个节点
  * 方法
    * CURD DOM树
      * appendChild()：向节点的子节点列表的结尾添加新的子节点
      * removeChild()：删除（并返回）当前节点的指定子节点
      * replaceChild()：用新节点替换一个子节点
```ruby
    <style>
        div{
            border:1px red solid;
        }
        #div1{
            width: 300px;
            height: 300px;
        }
        #div2{
            width: 200px;
            height: 200px;
        }
        #div3{
            width: 200px;
            height: 200px;
        }
    </style>
</head>
<body>
<div id="div1">
    div1
    <div id="div2">div2</div>
</div>
<!--<input type="button" id="remove" value="删除节点">-->
<a href="javascript:void(0);" id="remove">删除节点</a>
<!--
超链接功能
1.可以被点击
2.点击后跳转到href指定的URL
在上面的删除功能中，如果href的值为空，会跳转到当前页面，就会刷新，div2又会被重新加载出来，就想没有删一样
所以要实现：保留1功能，去掉2功能
实现方式：href = "javascript:void(0);"
-->
<a href="javascript:void(0);" id="add">删除节点</a>
<!--<input type="button" id="add" value="添加节点">-->
</body>
<script>
    var remove = document.getElementById("remove");
    remove.onclick = function () {
        var div1 = document.getElementById("div1");
        var div2 = document.getElementById("div2");
        div1.removeChild(div2);
    }
    var add = document.getElementById("add");
    add.onclick = function () {
        var div1 = document.getElementById("div1");
        var div3 = document.createElement("div");
        div3.setAttribute("id","div3");
        div1.appendChild(div3);
    }
</script>
```
  * 属性
    * parentNode：返回节点的父节点
```ruby
//案例：动态表格，可以添加删除数据
<head>
    <meta charset="UTF-8">
    <title>动态表格</title>
    <style>
        div{
            text-align: center;
            margin: 50px;
        }
        table{
            border: 1px solid;
            margin: auto;
            width: 500px;
        }
        td,th{
            text-align: center;
            border: 1px solid;
        }
    </style>
</head>
<body>
<div>
    <input type="text" id="id" placeholder="请输入编号">
    <input type="text" id="name" placeholder="请输入姓名">
    <input type="text" id="gender" placeholder="请输入性别">
    <input type="button" value="添加" id="btn_add">
</div>
<table>
    <caption>学生信息表</caption>

    <tr>
        <th>编号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>操作</th>
    </tr>

    <tr>
        <td>1</td>
        <td>帅帅灿</td>
        <td>男</td>
        <td><a href="javascript:void(0);" onclick="delTr(this);">删除</a></td>
    </tr>

</table>
</body>
<script>
    /**
     * 分析
     * 1.添加
     *   1.1给添加按钮绑定单击事件
     *   1.2获取文本框的内容
     *   1.3创建td，并设置td的文本为文本框的内容
     *   1.4创建tr,将td添加到tr中
     *   1.5获取table，将tr添加到table中
     * 2.删除
     *   2.1确定点击的是哪一个超链接：<a href="javascript:void(0);" onclick="delTr(this)">删除</a>
     *   2.2删除：removeChild()：通过父节点删除子节点
     *
     */
    //添加
    document.getElementById("btn_add").onclick = function () {
        var id = document.getElementById("id").value;
        var name = document.getElementById("name").value;
        var gender = document.getElementById("gender").value;

        //创建td，并设置内容
        var td_id = document.createElement("td");
        var text_id = document.createTextNode(id);
        td_id.appendChild(text_id);
        var td_name = document.createElement("td");
        var text_name = document.createTextNode(name);
        td_name.appendChild(text_name);
        var td_gender = document.createElement("td");
        var text_gender = document.createTextNode(gender);
        td_gender.appendChild(text_gender);
        var td_a = document.createElement("td");
        var ele_a = document.createElement("a");
        ele_a.setAttribute("href","javascript:void(0);");//添加属性
        ele_a.setAttribute("onclick","delTr(this);");//添加属性
        var text_a = document.createTextNode("删除");
        ele_a.appendChild(text_a);//添加文本
        td_a.appendChild(ele_a);//添加超链接

        //创建tr，并将td添加到tr中
        var tr = document.createElement("tr");
        tr.appendChild(td_id);
        tr.appendChild(td_name);
        tr.appendChild(td_gender);
        tr.append(td_a);

        //获取table，将tr添加到table中
        var table = document.getElementsByTagName("table")[0];
        table.appendChild(tr);
    }
    //删除
    function delTr(obj) {
        var table = obj.parentNode.parentNode.parentNode;
        var tr = obj.parentNode.parentNode;
        table.removeChild(tr);
    }
</script>
```
## HTML DOM
1.标签体的设置和获取：innerHTML
```ruby
<body>
<div id="div1">div</div>
</body>
<script>
    var div = document.getElementById("div1");
    var innerHTML = div.innerHTML;
    //alert(innerHTML);
    //div标签替换为文本输入框
    div.innerHTML = "<input type='text'>";
    //div标签中追加一个文本输入框
    div.innerHTML += "<input type='text'>";
</script>

//在上一个动态表格的案例中
//使用innerHTML添加
document.getElementById("btn_add").onclick = function () {
    var id = document.getElementById("id").value;
    var name = document.getElementById("name").value;
    var gender = document.getElementById("gender").value;
    //获取table
    var table = document.getElementsByTagName("table")[0];
    table.innerHTML += "<tr>\n" +
        "        <td>" + id + "</td>\n" +
        "        <td>" + name + "</td>\n" +
        "        <td>" + gender + "</td>\n" +
        "        <td><a href=\"javascript:void(0);\" onclick=\"delTr(this);\">删除</a></td>\n" +
        "    </tr>"
}
```
2.使用html元素对象的属性  
3.控制元素样式
  * 使用元素的style属性来设置
```ruby
<body>
<div id="div1">div</div>
</body>
<script>
    var div = document.getElementById("div1");
    div.onclick = function () {
        div.style.border = "1px solid red";
        div.style.width = "200px";
        //原来是font-size的要变成fontSize
        div.style.fontSize = "20px";
    }
</script>
```
  * 提前定义好类选择器的样式，通过元素的className属性来设置其class属性值
```ruby
<style>
    .d1{
        border: 1px solid red;
        width: 100px;
        height: 100px;
    }
    .d2{
        border: 2px solid blue;
        width: 200px;
        height: 200px;
    }
</style>
<body>
<div id="div2">div2</div>
</body>
<script>
    var div2 = document.getElementById("div2");
    div2.onclick = function () {
        div2.className = "d2";
    }
</script>
```

