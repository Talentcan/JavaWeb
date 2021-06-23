# web服务器软件
服务器：安装了服务器软件的计算机  
服务器软件：接收用户的请求，处理请求，做出响应  
web服务器软件：在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目。

常见的java相关的web服务器软件
  * javaEE：java语言在企业级开发中使用的技术规范的总和，一共规定了13项大的规范
  * webLogic：Oracle公司，大型的javaEE服务器，支持所有的javaEE的规范，收费
  * webSphere：IBM公司，大型的javaEE服务器，支持所有的javaEE的规范，收费
  * JBOSS：JBOSS公司，大型的javaEE服务器，支持所有的javaEE的规范，收费
  * Tomcat：Apache基金组织，中小型的javaEE服务器，仅仅支持少量的javaEE的规范servlet/jsp，开源，免费。

## Tomcat：web服务器软件
1.下载：https://tomcat.apache.org/
2.安装：将压缩包解压到没有中文和空格的目录下
3.卸载：删除目录
4.启动
  * bin/startup.bat
  * 访问：浏览器中输入：http://localhost:8080 访问自己
  *                   http://别人的ip 访问别人  
  * 启动时可能出现的问题
    * 命令控制窗口一闪而过
      * 原因：没有正确配置JAVA_HOME环境变量
      * 解决方案：正确配置JAVA_HOME环境变
    * 启动报错：端口号被占用
      * 1.找到占用的端口号，并且找到对应的进程，杀死该进程
        * cmd-->netstat ano-->看PID-->在任务管理器中将刚才PID的进程结束
      * 2.修改自身的端口号
        * conf/server.xml中修改Connector port="8080" protocol="HTTP/1.1"中port的值
        * 一般将Tomcat的默认端口号修改为80。80端口号是http协议的默认端口号，在访问时，可以不用输入端口号
5.关闭  
6.配置
  * 部署项目的方式
    * 1.直接将web项目放到webapps目录下即可
      * localhost:8080/项目访问路径/项目资源，项目的访问路径-->虚拟目录：/项目访问路径path
      * 简化部署：将项目打成war包，再把war包放置到webapps目录下，war包会自动解压缩，并且删除的时候将war删除，项目会自动删除
    * 2.配置conf/server.xml文件
      * 在Host标签体中配置
      * 添加标签：ConText docBase="项目存放的路径" path="虚拟目录" />
    * 3.热部署：在conf\Catalina\localhost中创建任意名称的xml文件，在文件中编写 ConText docBase="项目存放的路径" />
      * 虚拟目录：xml文件的名称
静态项目和动态项目
  * 目录结构
    * java动态项目的目录结构
      * 项目的根目录
      *   ----WEB-INF目录
      *     ----web.xml：web项目的核心配置文件
      *     ----classes目录：放置字节码文件的目录
      *     ----lib目录：放置依赖的jar包

将Tomcat集成到IDEA中，并且创建javaEE的项目，部署项目

## IDEA与Tomcat的相关配置
1.IDEA会为每一个Tomcat部署的项目单独建立一份配置文件
  * 查看控制台的log：Using CATALINA_BASE:   "C:\Users\TEDU\.IntelliJIdea2019.2\system\tomcat\_JavaWeb"
2.工作空间项目和Tomcat部署的web项目
  * Tomcat真正访问的是“Tomcat部署的web项目”，“Tomcat部署的web项目”对应着“工作空间项目”的web目录下所有资源
  * WEB-INF目录下的资源不能被浏览器直接访问
3.断点调试：添加断点，然后debug启动























