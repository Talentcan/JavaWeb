# XML
1.概念：extensible Markup language 可扩展标记语言
  * 可扩展：标签都是自定义的。
  * 功能
    * 存储数据
      * 配置文件
      * 在网络中传输
  * XML和HTML的区别
    * XML的标签都是自定义的，HTML标签是预定义的。
    * XML的语法严格，HTML语法松散
    * XML是存储数据的，HTML是展示数据
2.语法
  * 基本语法：
    * XML的第一行必须定义文档声明：<?xml version="1.0" ?>
    * XML文档中，有且只有一个根标签
    * 属性值必须使用引号（单双引号都可以）引起来
    * 标签必须正确关闭
    * XML标签名称区分大小写
  * 快速入门
  * 组成部分：
    * 文档声明
      * 格式：<?xml 属性列表 ?>
      * 属性列表
        * version：版本号，必须的属性
        * encoding：编码方式，告知解析引擎当前文档使用的字符集，默认值为：ISO-8859-1
        * standlone：是否独立，yes：不依赖其他文件，no：依赖其他文件 
    * 指令：结合CSS：<?xml-stylesheet type="text/css" href="a.css" ?>
    * 标签:标签名称自定义的
    * 属性：id属性值唯一
    * 文本
      *  CDATA区：在该区域中的数据会被原样展示，格式：<![CDATA[ 想要展示的数据 ]]>
  * 约束：规定XML文档的书写规则
    * 作为框架的使用者（程序员）：能够在XML中引入约束文档，能够简单的读懂约束文档
    * 分类
      * DTD：一种简单的约束技术
      * Schema：一种复杂的约束技术
    * DTD
      * 引入dtd文档到XML文档中
        * 内部dtd：将约束规则定义在XML文档中
        * 外部dtd：将约束的规则定义在外部的dtd文件中
          * 本地：<!DOCTYPE 根标签名 SYSTEM "dtd文件的位置">
          * 网络：<!DOCTYPE 根标签名 PUBLIC "dtd文件的名字" "dtd文件的位置URL">
    * Schema：
      * 写Schema：
        * 填写

























