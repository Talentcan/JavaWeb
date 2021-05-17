# DOM
## DOM简单学习
功能：控制（增删盖查）HTML文档的内容  
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

window：窗口对象
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
3.属性
4.特点
  * window对象不需要创建可以直接使用window使用。window.方法名();
  * window引用可以省略。方法名();



















