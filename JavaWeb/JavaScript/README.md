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
    * 用typeof运算符可以知道变量的数据类型，用法是typeof(变量名);
      * 其中typeof运算符对于null值会返回"Object"。这实际上是JavaScript最初实现中的一个错误，然后被ECMAScript沿用，现在null被认为是对象的占位符，从而解释了这一矛盾，但从技术上来说，它任然是原始值。
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
    * 一元运算符：只有一个运算数的运算符
      * ++，--，+（正号），-（负号）
      * 注意：在JavaScript中，使用正负号进行运算时，如果运算数不是运算符所要求的类型（正负号只能是number类型），那么JavaScript引擎会自动的将运算数进行类型转换
      * 其他类型转number的规则
        * string转number：按照字面值转换，如果字面值不是数字，那么转为NaN（不是数字的数字）,NaN加别的数字也是NaN
        * boolean转number：true转为1，false转为0
      ```ruby 
      var a = +"123" //a=123
      var b = +"abc" //b=NaN
      var f1 = +true; //f1=1
      var f2 = +false; //f2=0
      ```
    * 算数运算符
      * +，-，*，/，%....
    * 赋值运算符
      * =，+=，-=.....
    * 比较运算符
      * <，>，>=，<=，==，===(全等)
      * 比较方式
        * 类型相同：直接比较
          * 字符串：按照字典顺序比较，按位逐一比较，知道得出大小为止
        * 类型不同：先进行类型转换，再进行比较
          * ===：全等于，在比较之前，先判断类型，如果类型不一样，则直接返回false
    * 逻辑运算符
      * &&，||，!
      * 其他类型转boolean：如果其他类型参与逻辑运算
        * number转boolean：0和NaN为假，非0为真
        * string转boolean：除了空字符串（""）为false，其余都是true
        * null和undefined转boolean：都是false
        * 对象转boolean：所有对象都是true
        ```
        //JavaScript中可以这样来定义，简化书写
        //用来判断是否为空字符串，防止空指针异常
        var obj = "";
        if(obj){ //防止空指针异常
          document.write("123");
        }
        //等于
        if(obj != null && obj.length > 0){
          document.write("123");
        }
        ```
    * 三元运算符
      * ? ：
        * 语法：表达式?值1:值2;
        * 判断表达式的值，如果是true则取值1，如果是false则取值2；
  * 流程控制语句
    * 1.if...else...
    * 2.switch
      * 在java中，switch语句中可以接收的数据类型：byte，int，short，char，枚举（1.5后），String（1.7后）
      * 在JavaScript中，switch语句可以接收任意的原始数据类型
    * 3.while
    * 4.do...while...
    * 5.for
  * JavaScript的特殊语法：都不建议使用
    * 1.语句以;号结尾，如果一行只有一条语句则;号可以省略
    * 2.变量的定义使用var关键字，也可以不使用
      * 用和不用的区别：变量的作用范围不一样
        * 用：定义的变量是局部变量
        * 不用：定义的变量是全局变量
```ruby
练习：打印9*9乘法表，在页面展示
<title>9*9乘法表</title>
    <style>
        td{
            border: 1px solid;
        }
    </style>
    
    <script>
        document.write("<table align='center'>");
        for(var i=1 ; i<=9 ; i++){
            document.write("<tr>");
            for (var j=1 ; j<=i ; j++){
                document.write("<td>");
                document.write(i + " * " + j + " = " + i*j);
                document.write("&nbsp;&nbsp;&nbsp;");
                document.write("</td>");
            }
            document.write("</tr>");
        }
        document.write("</table>");
    </script>
```
2.基本对象
  * Function对象：函数（方法）对象
    * 创建
      * 1.var fun = new Function(形式参数列表，方法体);不常用
      * 2.function 方法名称(形式参数列表){方法体} 常用
      * 3.var 方法名 = function(形式参数列表){方法体} 
    * 方法
    * 属性
    * 特点
      * 1.方法定义时，形参的类型不用写，都是var
      * 2.方法是一个对象，如果定义名称相同的方法，会覆盖
    * 调用
      * 方法名称(实际参数列表);
```ruby
//创建方式1
var fun1 = new Function(a,"b","alert(a)");
fun(3,4);
//创建方式2
function fun2(a,b) {
  alert(a+b);
}
fun2(3,4);
//创建方式3
var fun3 = function (a,b) {
  alert(a-b);
}
fun3(5,3);


```
  * Array
  * Boolean
  * Date
  * Math
  * Number
  * String
  * RegExp
  * Global




