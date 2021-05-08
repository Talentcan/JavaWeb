# 数据库连接池
概念：其实就是一个容器（集合），存放数据库连接的容器。当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问结束后，会将连接对象归还给容器。  

实现
1.标准接口：DataSource   javax.sql包下的
  * 方法
    * 获取连接：getConnection()
    * 归还连接：connection.close()，如果连接对象connection是从连接池中获取的，那么调用connection.close()方法，则不会在关闭连接了，而是归还连接
2.一般我们不用去实现它，有数据库厂商来实现
  * C3P0：数据库连接池实现技术
  * Druid：数据库连接池实现技术，由阿里提供，十分高效

## C3P0数据库连接池实现技术  
步骤  
1.导入jar包 c3p0-0.9.5.2.jar和mchange-commons-java-0.2.12.jar依赖jar包，并且不要忘记导入数据库的驱动jar包  
2.定义配置文件
  * 名称：c3p0.properties 或者 c3p0-config.xml，只能是这两种
  * 路径：直接将文件放在src目录下就可以，可以自动加载
3.创建核心对象：数据库连接池对象 ComboPooledDataSource  
4.获取连接：getConnection  
```ruby
<c3p0-config>
    <!--使用默认的配置读取连接池对象-->
<default-config>
    <!--连接参数-->
    <property name="driverClass">com.mysql.jdbc.Driver</property>
    <property name="jdbcUrl">jdbc:mysql://localhost:3306/db1</property>
    <property nane="user"></property>
    <property name="password"></property>
    <!--连接池参数-->
    <property name="initialPoo1Size">5</property>
    <property name="maxPoo1Size">10</property>
    <property name="checkoutTimeout">3000</property>
</default-config>
<!--如果传参，就是name的值-->
<named-config name="otherc3p0">
    <!--连接参数-->
    <property name="driverClass">com.mysql.jdbc.Driver</property>
    <property name="jdbeUrl">jdbc:mysql://localhost:3306/db1</property>
    <property name="user"></property>
    <property name="password"></property>
    <!--连接池参数-->
    <property name="initia1Poo1size">5</property>
    <property name="maxPoo1Size">8</property>
    <property name="checkoutTimeout">1000</property>
</named-config>
</c3p0-config>

//c3p0演示
public static void main(String[] args) throws SQLException {
        //1.创建数据库连接池对象
        //使用方法中没有传递参数则使用默认配置，如果有参数就调用参数名字的配置
        //DataSource ds = new ComboPooledDataSource();
        DataSource ds = new ComboPooledDataSource("otherc3p0");
        //2.获取连接对象
        for (int i=1 ; i<=8 ; i++){
            Connection conn = ds.getConnection();
            System.out.println(i + " " + conn);
        }
    }
```
## Druid数据库连接池实现技术
步骤
1.导入jar包 druid-1.0.9.jar
2.定义配置文件
  * 是properties文件形式的
  * 可以叫任意名称，可以放在任意目录，需要手动加载
3.加载配置文件，properties  
4.获取数据库连接池对象：通过工厂类来获取：DruidDataSourceFactory  
5.获取连接：getConnection  
```ruby
//配置文件
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/db1
username=
password=
initialSize=5
maxActive=10
maxWait=3000

//druid演示
public static void main(String[] args) throws Exception {
        //1.导入jar包
        //2.定义配置文件
        //3.加载配置文件
        Properties pro = new Properties();
        InputStream res = DruidDemo1.class.getClassLoader().getResourceAsStream("druid.properties");
        pro.load(res);
        //4.获取连接池对象
        DataSource ds = DruidDataSourceFactory.createDataSource(pro);
        //5.获取连接
        Connection conn = ds.getConnection();
        System.out.println(conn);
    }
```

Druid工具类
1.定义一个类JDBCUtils  
2.提供静态代码块加载配置文件，初始化连接池对象  
3.提供方法
  * 获取连接方法：通过数据库连接池获取连接
  * 释放资源
  * 获取连接池的方法
```ruby
//创建工具类
public class JDBCUtils {
    //定义成员变量 DataSource
    private static DataSource ds;
    static {
        try {
            //加载配置文件
            Properties pro = new Properties();
            InputStream res = JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties");
            pro.load(res);
            //4.获取连接池对象
            ds = DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //获取连接
    public static Connection getConnection () throws SQLException {
        return ds.getConnection();
    }
    //释放资源
    public static void close(Statement stmt, Connection conn){
        //可以简化代码，相当于参数只有两个的时候也调用三个参数的方法，只是将第一个参数的值设置为null
        close(null,stmt,conn);
    }

    public static void close(ResultSet rs, Statement stmt, Connection conn){
        if (rs != null)
            try{
                rs.close();
            }catch (SQLException e){
                e.printStackTrace();
            }
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

    //获取连接池的方法
    public static DataSource getDataSource(){
        return ds;
    }
}

//使用工具类
public class DruidDemo2 {
    public static void main(String[] args) {
        //给account表添加一条记录
        Connection conn = null;
        PreparedStatement pstmt = null;
        try {
            //获取连接
            conn = JDBCUtils.getConnection();
            //定义sql
            String sql = "insert into account values(null,?,?)";
            //获取pstmt
            pstmt = conn.prepareStatement(sql);
            //给?赋值
            pstmt.setString(1,"wangwu");
            pstmt.setDouble(2,2000);
            //执行sql
            int count = pstmt.executeUpdate();
            System.out.println(count);
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JDBCUtils.close(pstmt,conn);
        }
    }
```
## Spring JDBC









