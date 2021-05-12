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
```
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
