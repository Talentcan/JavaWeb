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






















