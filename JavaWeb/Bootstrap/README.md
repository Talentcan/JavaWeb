# Bootstrap
1.概念
  * Bootstrap是美国Twitter公司的设计师Mark Otto和Jacob Thornton合作基于HTML、CSS、JavaScript 开发的简洁、直观、强悍的前端开发框架，使得 Web 开发更加快捷。
  * 好处
    * 1.定义了很多CSS样式和JS插件，开发时可以直接使用这些插件
    * 2.响应式布局
      * 同一套页面可以兼容不同分辨率的设备  
2.快速入门
  * 下载Boostrap
  * 在项目中复制下载的Boostrap
  * 创建HTML页面，引入必要的资源文件
```ruby
<!doctype html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link rel="stylesheet" href="css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]-->
<!--    <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>-->
<!--    <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>-->
    <!--[endif]-->
</head>
<body>
<h1>你好，世界！</h1>

<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.2.1.min.js" integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
</body>
</html>
```
## 响应式布局
实现：依赖于栅格系统
  * 栅格系统：将一行平均分成12个格子，可以指定元素占几个格子
步骤
  * 1.定义容器：相当于之前的table
    * 容器分类
      * container（固定宽度）：在每种设备上都固定宽度，除了超小屏幕，都会有一定的留白
      * container-fluid（100% 宽度）：每一种设备都是100%宽度
  * 2.定义行：相当于之前的tr，样式：row
  * 3.定义元素：指定该元素在不同的设备下，所占的格子数目，样式：col-设备代号-格子数目
    * 设备代号
      * xs：超小屏幕，手机(<768px)，如：col-xs-12，在手机上占12个格子大小（占满一行）
      * sm：小屏幕 平板 (≥768px)
      * md：中等屏幕 桌面显示器 (≥992px)
      * lg：大屏幕 大桌面显示器 (≥1200px)
  * 注意事项
    * 1.一行中如果格子数目超过12，则超过的部分会自动换行
    * 2.栅格类属性可以向上兼容，即在超小屏幕下一行分3份，在大的屏幕下也是分三份
    * 3.如果真实设备的宽度小于设置的栅格类属性的设备代码的最小值，则会一个元素站满一整行
```ruby
    <style>
        .inner{
            border: 1px solid red;
        }
    </style>
<body>
<!--定义容器-->
<div class="container">
    <div class="row">
<!-- 在大显示器上一行12个格子，在小显示器上一行6个格子-->
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
        <div class="col-lg-1 col-sm-2 inner">hucan</div>
    </div>
</div>
</body>
```

## CSS样式和JS插件
全局CSS样式
  * 按钮：class="btn btn-default"
  * 图片
    * class="img-responsive"：图片在任意尺寸都占100%
    * 图片的形状
  * 表格
  * 表单
组件
  * 导航条
  * 分页条
JS插件
  * 















