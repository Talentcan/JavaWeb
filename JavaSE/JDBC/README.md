# JDBC
## 概念
java database connectivity，java数据库连接，java语言操作数据库  
JDBC的本质：其实是官方（Sun公司）定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动（JDBC的实现类，各个数据库版本的实现类不同）jar包。我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类。  
![](../JDBC/JDBC.jpg)  

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
      * 方法：static Connection getConnection(String url, String user, String password)
      * 参数：url 指定连接的路径（语法：jdbc:mysql://ip地址(域名):端口号/数据库名称）；user 用户名；password 密码
      * 注意：如果连接的是一个本机mysql服务器，并且mysql服务器默认端口3306，则url可以简写为：kdbc:mysql:///数据库名称

2.Connection：数据库连接对象
  * 功能
    * 获取执行sql的对象
      * Statement createStatement()
      * PreparedStatement prepareStatement(String sql) 
    * 管理事务：
      * 开启事务：void setAutoCommit(boolean autoCommit)，调用该方法设置参数为false，即开启事务
      * 提交事务：void commit()  
      * 回滚事务：void rollback() 

3.Statement：执行sql的对象
  * 功能
    * 执行sql
      * boolean execute(String sql)：可以执行任意的sql，只需了解
      * int executeUpdate(String sql)：执行DML（insert、update、delete等对数据操作）语句、DDL（create、alter、drop等对库和表操作）语句
        * int返回值：受到影响的行数，可以通过这个受到影响的行数判断DML语句是否执行成功，返回值>0的则执行成功，反之则失败
      * ResultSet executeQuery(String sql)：执行DQL（select）语句
```ruby
练习statement：
1.account表 添加一条数据
2.account表 修改数据
3.account表 删除一条数据

1.添加数据，用比较规范的格式，异常捕获，关闭资源
public static void main(String[] args) {
        Connection conn =null;
        Statement stmt = null;
        try{
            //1.注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            //2.定义sql语句
            String sql = "insert into account value(null,'wangwu','2000')";
            //3.获取数据库连接对象
            conn = DriverManager.getConnection
                    ("jdbc:mysql://localhost:3306/db1", "", "");
            //4.获取执行sql的对象statement
            stmt = conn.createStatement();
            //5.执行sql
            int count = stmt.executeUpdate(sql); //count是影响的行数
            //6.处理结果
            if (count > 0)
                System.out.println("成功");
            else
                System.out.println("失败");
        }catch (ClassNotFoundException | SQLException e){
            e.printStackTrace();
        }
        finally{
            //因为前面定义为空，如果try代码块中出错，就会出现空指针异常，所以为了避免空指针异常，应先进行一次判断
            if (stmt != null)
                try{
                    stmt.close();
                }catch (SQLException e){
                    e.printStackTrace();
                }
            if (conn != null)
                try{
                    conn.close();
                }catch (SQLException e){
                    e.printStackTrace();
                }
        }
    }
    
2.修改数据
//只用修改上一个代码的sql语句部分，其余部分不变
String sql = "update account set balance = 1000 where id = 3";

3.删除一条数据
//只用修改上一个代码的sql语句部分，其余部分不变
String sql = "delete from account where id = 3";

表的创建也可以使用executeupdate，但是它影响行的数量为0
```
4.ResultSet：结果集的对象，封装查询结果
  * 方法
    * next()：光标（游标）向下移动一行，一行一行的向下移动，每次获取某一行的某一列
    * getxxx(参数)：获取数据
      * xxx：代表数据类型，如：int getInt();String getString()
      * 参数
        * int：代表列的编号

5.PreparedStatement：执行sql的对象，功能比statement强大





















