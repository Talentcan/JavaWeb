# JDBC
## 概念
java database connectivity，java数据库连接，java语言操作数据库  
JDBC的本质：其实是官方（Sun公司）定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动（JDBC的实现类，各个数据库版本的实现类不同）jar包。我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类。  
![](../JDBC/图片1.jpg)  

## 快速入门
  * 步骤
    * 导入驱动jar包
      *  复制 mysql-connector-java-5.1.37到项目的libs文件夹目录下
      *  文件夹右键-->Add As Library ，这一步操作才是真正将jar包，加入到项目中
    * 注册驱动，让程序知道用的是哪一个版本或哪一个驱动包
    * 获取数据库的连接对象：connection
    * 定义sql语句
    * 获取执行sql语句的对象 statement
    * 执行sql，接受返回的结果
    * 处理结果
    * 释放资源
```ruby
代码实现：
public static void main(String[] args) throws Exception {
        //1.导入驱动jar包
        //2.注册驱动
        Class.forName("com.mysql.jdbc.Driver"); //把这个类文件加载进内存，加载进内存后会自动执行
        //3.获取数据库连接对象
        Connection conn = DriverManager.getConnection
                ("jdbc:mysql://localhost:3306/db1", "", "");
        //4.定义sql语句
        String sql = "update account set balance=500 where id=1";
        //5.获取执行sql的对象statement
        Statement stmt = conn.createStatement();
        //6.执行sql
        int count = stmt.executeUpdate(sql);
        //7.处理结果
        System.out.println(count);
        //8.释放资源
        stmt.close();
        conn.close();
    }
//执行结束后，数据库中的数据被成功修改
```
## 详解各个对象
1.DriverManager：驱动管理对象
  * 功能
    * 注册驱动：告诉程序该使用哪一个数据库驱动jar
      * 方法：static void registerDriver(Driver driver) 向 DriverManager 注册给定驱动程序。  、
      * 写代码使用：Class.forName("com.mysql.jdbc.Driver");
      * 通过查看源码发现：在com.mysql.jdbc.Driver类中存在静态代码块，会自动运行
      ```Ruby
      //源码
      static {
        try {
            java.sql.DriverManager.registerDriver(new Driver());  //注册驱动
        } catch (SQLException E) {
            throw new RuntimeException("Can't register driver!");
        }
      }
      ```
      * 注意：mysql5版本以后，这里可以省略不写，因为在刚刚导入的jar包中，META-INF文件中java.sql.Driver文件中帮我们写了，如果我们没写驱动，它会首先帮我们执行这个文件，自动注册驱动
    * 获取数据库连接

2.Connection：数据库连接对象


3.Statement：执行sql的对象


4.ResultSet：结果集的对象


5.PreparedStatement：执行sql的对象，功能比statement强大
