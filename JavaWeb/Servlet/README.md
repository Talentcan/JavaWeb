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
执行原理  
  * 1.当服务器接收到客户端浏览器的请求后，会解析请求URL路径，通过虚拟路径，获得访问的servlet的资源路径
  * 2.查找web.xml文件，是否有对应的\<url-pattern>标签体中的内容
  * 3.如果有则在找到\<servlet-class>全类名，然后使用反射的原理
  * 4.Tomcat会将字节码文件加载进内存，并且创建器对象创建该对象，用class.forName()和class.newInstance()
  * 5.调用其方法



servlet中的生命周期  
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

servlet3.0
  * 好处：支持注解配置，可以不需要web.xml。
  * 步骤
    * 1.创建javaEE项目，选择servlet的版本3.0以上，可以不需要web.xml
    * 2.定义一个类，实现servlet接口
    * 3.复写方法
    * 4.在类上使用@WebServlet注解，进行配置
      * @WebServlet("资源路径")
































