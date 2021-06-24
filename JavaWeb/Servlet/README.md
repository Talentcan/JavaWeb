# servlet
概念：运行在服务器端的小程序
  * servlet就是一个接口（规则），定义了java类被浏览器访问到（被Tomcat识别）的规则。
  * 我们定义一个类，实现servlet接口，复写方法

## servlet快速入门
1.创建javaEE项目  
2.定义一个类，实现servlet接口  
3.实现接口中的抽象方法  
4.配置servlet：在web.xml中配置  
```ruby
<!--  配置servlet，在<web-app>标签中-->
    <servlet>
        <servlet-name>demo1</servlet-name>
        <servlet-class>cn.web.servlet.ServletDemo1</servlet-class>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>demo1</servlet-name>
        <url-pattern>/demo1</url-pattern>
    </servlet-mapping>
```
## 执行原理  
  * 1.当服务器接收到客户端浏览器的请求后，会解析请求URL路径，通过虚拟路径，获得访问的servlet的资源路径
  * 2.查找web.xml文件，是否有对应的\<url-pattern>标签体中的内容
  * 3.如果有则在找到\<servlet-class>全类名，然后使用反射的原理
  * 4.Tomcat会将字节码文件加载进内存，并且创建器对象创建该对象，用class.forName()和class.newInstance()
  * 5.调用其方法



## servlet中的生命周期  
1.被创建：执行init方法，只执行一次  
  * servlet默认情况下，第一次被访问时，servlet被创建
  * 在服务器启动时创建，在\<servlet>标签下用\<load-on-startup>标签，如果标签包裹的值为负数则表示第一次访问时创建，为0或正整数时表示在服务器启动时创建  
  * servlet的init方法，只执行一次，说明一个servlet在内存中只有一个对象，servlet是单例的
    * 多个用户同时访问时，可能存在线程的安全问题
    * 解决：尽量不要在servlet中定义成员变量，可以在service方法中定义成员变量。即使定义了成员变量，也不要对其修改值
2.提供服务：执行service方法，可以执行多次  
  * 每次访问servlet时，service方法都会被调用一次
3.被销毁：执行destroy方法，只执行一次  
  * servlet被销毁时执行，服务器关闭时，servlet被销毁
  * 只有服务器正常关闭时，才会执行destroy方法
  * destroy方法在servlet被销毁前执行，一般用于释放资源



五个方法  
1.public void init(...)：初始化方法，在servlet被创建时执行，只会执行一次  
2.public void service(...)：提供服务方法，每一次servlet被访问时执行，可以执行多次  
3.public void destroy()：销毁方法，在在服务器正常关闭时执行，只执行一次  
4.public ServletConfig getServletConfig()：获取ServletConfig对象，ServletConfig对象是servlet的配置对象  
5.public String getServletInfo()：获取servlet的一些信息，如：版本，作者等  

## servlet3.0注解配置
  * 好处：支持注解配置，可以不需要web.xml。
  * 步骤
    * 1.创建javaEE项目，选择servlet的版本3.0以上，可以不需要web.xml
    * 2.定义一个类，实现servlet接口
    * 3.复写方法
    * 4.在类上使用@WebServlet注解，进行配置
      * @WebServlet("资源路径")

## servlet的体系结构
servlet --- 接口  
    | 实现  
GenericServlet --- 抽象类  
    | 继承  
HttpServlet --- 抽象类  

GenericServlet：将servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象
  * 以后定义servlet类时，可以继承GenericServlet，实现service()方法即可，其余方法如果用到，可以复写。  
HttpServlet：对http协议的一种封装，简化操作
  * 定义类继承HttpServlet
  * 复写doGet/doPost方法

## servlet相关配置
1.urlpartten：servlet访问路径
  * 因为返回值是数组类型的，所以可以设置多个访问路径，即一个servlet可以设置多个访问路径，如@WebServlet({"/路径1","/路径2","/路径3"})
  * 路径的定义规则
    * /xxx
    * /xxx/xxx：多层路径，目录结构，如：@WebServlet("/user/demo3")
    * *.do ：.后面的可以自己设置，如.aaa或.bbb，.前面是项目名，如：@WebServlet("demo3.do")，不加/

## HTTP
概念：Hyper Text Transfer Protocol 超文本传输协议
  * 传输协议：定义了客户端和服务器端通信时发送数据的格式
  * 特点
    * 基于TCP/IP的高级协议
    * 默认端口号是80
    * 基于请求/响应模型的，一次请求对应一次响应
    * 无状态的协议：每次请求之间相互独立的，不能交互数据
  * 历史版本
    * 1.0：每一次请求响应都会建立新的连接
    * 1.1：复用连接，对缓存的支持比较好

请求消息数据格式
1.请求行
  *     请求方式 请求URL 请求协议/版本
  * 如：get /login.html HTTP/1.1
  
  * 请求方式
    * HTTP协议中有7种请求方式，常用的有2种
      * GET
        * 请求参数在请求行中，在URL后
        * 请求的URL长度是有限制的
        * 不太安全，参数会显示
      * POST
        * 请求参数在请求体中
        * 请求的URL长度是没有限制的，一些文件
        * 比较安全，参数在请求体中
2.请求头
  * 请求头名称：请求头值
  * 常见的请求头
    * User-Agent：浏览器告诉服务器，访问时使用的浏览器版本信息
      * 可以在服务器端获取该头的信息，解决浏览器的兼容性问题
    * Referer：http://localhost/login.html 
      * 告诉服务器当前请求从哪里来
      * 作用：防盗链，统计工作
3.请求空行
  * 就是一个空行，用来分开POST请求头和请求体的空行

4.请求体（正文）
  * get方式没有请求体
  * 存放一些请求参数信息
  * 封装POST请求消息的请求参数



响应消息数据格式


客户端和服务器通信的步骤  
1.客户端向服务器发起请求，Tomcat服务器会根据请求URL中的资源路径，创建对应的servletdemo1的对象  
2.Tomcat服务器会创建request和response对象，request对象中封装请求消息数据  
3.Tomcat将request和response两个对象传递给service方法，并且调用service方法  
4.在service方法中，我们可以通过request对象获取请求数据，通过response对象来设置响应消息数据  
5.服务器在给浏览器做出响应之前，会从response对象中拿我们设置的响应消息数据  



## Request
1.request对象和response对象的原理  
  * request对象和response对象是由服务器创建的，我们只是来使用它们  
  * request对象是来获取请求消息，response对象是来设置响应消息  
2.request对象继承体系结构
  * ServletRequest  -- 接口
  *       | 继承
  * HttpServletRequest  -- 接口
  *       | 实现
  * org.apache.catalina.connector.RequestFacade 类(Tomcat)

3. request
  * 获取请求消息数据
    * 获取请求行数据
      * GET /login.html HTTP/1.1
      * 方法
        * 1.获取请求方式：GET
          * String getMethod()
        * 获取虚拟目录（√）
          * String getContextPath()
        * 获取servlet路径
          * String getServletPath()
        * 获取get方式的请求参数
          * String getQueryString()
        * 获取请求的URI（√）
          * String getRequestURI()：/demo1
          * StringBuffer getRequestURL()：http://localhost/demo1
        * 获取协议和版本
          * String getProtocol()
        * 获取客户机的IP地址
          * String getRemoteAddr()
    * 获取请求头数据
      * 方法
        * String getHeader(String name)：通过请求头的名称获取请求头的值  
        * Enumeration<String> getHeaderNames()：获取所有的请求头名称  
    * 获取请求体
      * 请求体：只有POST请求方式，才有请求体，在请求体中封装了POST请求的请求参数
      * 步骤
        * 1.获取流对象
          * BufferedReader getReader()：获取字符输入流，只能操作字符数据
          * ServletInputStream getInputStream()：获取自己输入流，可以操作所有类型数据 
        * 2.从流对象中拿数据
   * 其他功能
     * 1.获取请求参数通用方式：不论是get还是post方法请求方式都可以使用下列方法来获取请求参数
       * String getParameter(String name)：根据参数名称获取参数值，如：username=zs&password=123
       * String[] getParameterValues(String name)：根据参数名称获取参数值的数组，如：hobby=study&hobby=game，同样的参数名称有多个值，用数组存储
       * Enumeration<String> getParameterNames()：获取所有请求的参数名称
       * Map<String,String[]> getParameterMap()：获取所有参数的map集合
       * 中文乱码问题
         * get方式：Tomcat8已经将get方式乱码问题解决了
         * post方式：会存在乱码，可以在获取参数前，设置request的编码，request.setCharacterEncoding("utf-8");
 
     * 2.请求转发
     * 3.共享数据
     * 4.获取ServletContext
 












