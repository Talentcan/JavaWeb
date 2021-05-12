# CSS
CSS：用来美化和布局控制，Cascading Style Sheets 层叠样式表
好处  
1.功能强大  
2.将内容展示和样式控制分离
  * 降低耦合度，解耦
  * 让分工协作更容易
  * 提高开发效率
3.CSS使用：CSS和HTML结合使用
  * 1.内联样式：在标签内使用style属性指定CSS代码
  * 2.内部样式：head标签内，定义style标签，style标签内的标签体内容就是CSS代码
  * 3.外部样式：定义CSS资源文件，然后在head标签内，定义link标签，引入外部的资源文件
  * 注意：1,2,3种方式，CSS作用范围越来越大，方式1不常用，方式2,3常用
```ruby
第一种：不推荐使用
<!--内联样式：在标签内使用style属性指定CSS代码-->
<div style="color: red">hello css</div>
第二种
<!--内部样式：head标签内，定义style标签，style标签内的标签体内容就是CSS代码-->
<style>
        div{
            color: pink;
        }
    </style>
<div>hello css</div>
第三种
<!--外部样式：定义CSS资源文件，然后在head标签内，定义link标签，引入外部的资源文件-->
写在外部的CSS文件：
div{
    color: blue;
}
<link rel="stylesheet" href="CSS/a.css"> 
<style>@import "CSS/a.css";</style>//也可以用这种方式
<div>hello css</div>
```
4.CSS的语法
格式
```
选择器{
    属性名1：属性值1；
    属性名2：属性值2；
    ....
}
选择器：筛选具有相似特征的元素
注意：每一对属性需要使用";"隔开，最后一对属性可以不加
```
5.选择器
选择器：筛选具有相似特征的元素
分类
  * 基础选择器
    * id选择器：选择具体的id属性值的元素，建议在一个HTML页面中id值唯一
      * 语法：#id属性值{}
    * 元素选择器：选择具有相同标签名称的元素
      * 语法：标签名称{}
      * 注意：id选择器的优先级高于元素选择器
    * 类选择器：选择具有相同的class属性值的元素
      * 语法：.class属性值{}
      * 注意：类选择器的优先级高于元素选择器
  * 扩展选择器
    * 选择所有元素
      * 语法：*{}
    * 并集选择器
      * 语法：选择器1，选择器2{}
    * 子选择器：筛选选择器1元素下的选择器2元素
      * 语法：选择器1 选择器2{}
    * 父选择器：筛选选择器2的父选择器1
      * 语法：选择器1>选择器2{}
    * 属性选择器：选择元素名称，属性名=属性值的元素
      * 语法：元素名称[属性名 = "属性值"]{}
    * 伪类选择器：选择一些元素所具有的状态
      * 语法：元素：状态{}
      ```
      如：<a>标签的一些的状态
      link：初始化的状态
      visited：被访问过的状态
      active：正在访问状态
      hover：鼠标悬浮状态
      <style>
          a:link{color:pink}
          a:hover{color:green}
          a:active{color:yellow}
          a:visited{color:red}
      </style>
      <a href="#">TalentCan</a>
      ```
6.属性
1.字体、文本
  * font-size：字体大小
  * color：文本颜色
  * text-align：对齐方式
  * line-height：行高

2.背景
  * background：背景，复合属性，可以设置背景图片
  * 可以设置背景图片，如：background：url("图片位置") no-repeat(设置不重复) center;

3.边框
  * border：设置边框，复合属性

4.尺寸
  * width：宽度
  * height：高度

5.盒子模型：控制布局
  * margin：外边距
  * padding：内边距
    * 默认情况下，内边距会影响整个盒子的大小
    * box-sizing：border-box；设置盒子的属性，让width和height就是最终盒子的大小
  * float：浮动，将几个div放在一行中
    * left：
    * right：















