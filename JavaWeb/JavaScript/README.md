# JavaScript
概念：JavaScript是客户端脚本语言。运行在客户端浏览器中，每一个浏览器都有JavaScript的解析引擎。   
功能：可以增强用户和HTML页面的交互过程，可以来控制HTML元素，让页面有一些动态的效果，增强用户的体验  
JavaScript = ECMAScript + JavaScript自己特有的东西（BOM + DOM）  
ECMAScript：客户端脚本语言的标准  
1.基本语法
  * 与HTML的结合方式
    * 内部JS
      * 定义<script>标签，标签体内就是JS代码
    * 外部JS
      * 定义<script>标签，通过src属性引入外部写好的JS文件
    * 注意
      * <script>标签可以定义在HTML页面中的任何地方，但是定义的位置会影响执行顺序
      * <script>标签可以定义多个
  * 注释
    * 单行注释：//注释内容
    * 多行注释：/* 注释内容 */
  * 数据类型
    * 原始数据类型（基本数据类型）
      * number：数字，整数/小数/NaN(not a number 一个不是数字的数字类型)
      * string：字符串，单引号和双引号都可以
      * boolean：布尔类型，true/false
      * null：一个对象为空的占位符
      * undefined：未定义，如果一个变量没有给初始化值，则会被默认赋值为undefined
    * 引用数据类型：对象
  * 变量：
    * 变量：一小块存储数据的内存空间
    * java语言是强类型的语言，而JavaScript是弱类型的语言
      * 强类型：在开辟变量存储空间时定义了空间将来存储的数据的数据类型，只能用来存储固定类型的数据
      * 弱类型：在开辟变量存储空间时不定义空间将来存储的数据的数据类型，可以用来存储任意类型的数据
    * 语法
      * var 变量名 = 初始化值 ;
    ```ruby 
    //定义变量
    var a = 3;
    a = "abc";
    document.write(a + "</br>");
    //定义number类型
    var num1 = 5;
    var num2 = 5.3;
    var num3 = NaN;
    //输出到页面上
    document.write(num1 + "</br>");
    document.write(num2 + "</br>");
    document.write(num3 + "</br>");
    //定义string
    var str1 = "abc";
    var str2 = 'abc';
    document.write(str1 + "</br>");
    document.write(str2 + "</br>");
    //定义Boolean类型
    var flag = true;
    document.write(flag + "</br>");
    //定义null和undefined
    var obj1 = null;
    var obj2 = undefined;
    var obj3;
    document.write(obj1 + "</br>");
    document.write(obj2 + "</br>");
    document.write(obj3 + "</br>");
    ```
  * 运算符
  * 流程控制语句
2.基本对象





