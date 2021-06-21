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
        * 填写XML文档的根元素
        * 引入xsi前缀。如：xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        * 引入xsd文件命名空间
        * 为每一个xsd的约束声明一个前缀，作为标识
3.解析：操作XML文档，将文档中的数据读取到内存中
  * 操作XML文档
    * 解析（读取）：将文档中的数据读取到内存中
    * 写入：将内存中的数据保存到XML文档中。持久化的存储
  * 解析XML的方式
    * DOM：将标记语言文档一次性加载进内存，在内存中形成一颗DOM树
      * 优点：操作方便，可以对文档进行CURD的所有操作
      * 缺点：占内存，将DOM文档解析为DOM树可能会大一千到一万倍
    * SAX：逐行读取，读取一行就释放，然后读取下一行，内存中永远只有一行，所以需要基于事件来判断是那个标签的网页内容，基于事件驱动的。
      * 优点：内存占用较少，只有一行
      * 缺点：只能进行读取操作，不能增删改
  * XML常见的解析器：工具包
    * JAXP：Sun公司提供的解析器，支持DOM和sax两种方式，不常使用
    * DOM4J：支持DOM
    * jsoup：是java的HTML解析器
    * pull：Android操作系统内置的解析器，sax方式
  * jsoup的使用
    * 快速入门
      * 步骤
        * 1.导入jar包，jsoup-1.13.1.jar
        * 2.获取document对象
        * 3.获取对应的标签element对象
        * 4.获取数据
      * 对象的使用
        * 1.jsoup：工具类，可以解析HTML或XML文档，返回document
          * parse：解析HTML或XML文档，返回document
            * parse(File in, String chaesetname)：解析XML或HTML文件
            * parse(string html)：解析XML或HTML字符串
            * parese(URL url,int timeoutMillis),通过网络路径获取指定的HTML或XML的文档对象
        * 2.document：文档对象。代表内存中的DOM树
          * 获取element对象
            * getElementById(String id)：根据id属性值获取唯一的element对象
            * getElementsByTag(String tagname)：根据标签名称获取对象集合
            * getElementsByAttribute(String key)：根据属性名称获取原色对象集合
            * getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合
        * 3.elements：元素element对象的集合。可以当做ArrayList<Element>来使用
        * 4.element
          * 获取属性值
            * String attr(String key)：根据属性名称获取属性值
          * 获取文本内容
            * String text()：获取所有子标签里面的纯文本内容
            * String html()：获取标签体的所有内容（包括子标签里面所有的字符串内容）
        * 5.node：节点对象
          * 是document和element的父类
```ruby
public class JsoupDemo1 {
    public static void main(String[] args) throws IOException {
        //获取document对象，根据XML文档获取
        //1.获取XML文档的path路径
        String path = JsoupDemo1.class.getResource("student.xml").getPath();
        //2.解析XML文档，加载文档进内存，获取DOM树--->document
        Document document = Jsoup.parse(new File(path), "UTF-8");
        //3.获取元素对象 element
        Elements elements = document.getElementsByTag("name");
        //element对象是集合类型
        Element element = elements.get(0);
        //4.获取数据
        String name = element.text();
        System.out.println(name);
 
        //parese(URL url,int timeoutMillis),通过网络路径获取指定的HTML或XML的文档对象
        URL url = new URL("https://baike.baidu.com/item/jsoup/9012509?fr=aladdin");
        Document document = Jsoup.parse(url, 10000);
        System.out.println(document);
    }
}
```
* 快速查询方式
  * selector：选择器
    * 使用的方法：elements select(String cssQuery)
    * 语法：参考selector类中定义的语法
   * XPath：XPath即为XML路径语言（XML Path Language），它是一种用来确定XML文档中某部分位置的语言
     * 使用jsoup的xpath需要额外导入jar包，JXDocument
     * 查询参考手册，使用xpath的语法来完成查询



















