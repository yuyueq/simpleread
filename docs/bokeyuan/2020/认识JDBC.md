

## 概念

**<font size=4>所谓英文简写的意思是：Java DataBase Connectivity ，即 Java数据库的连接，用Java语言来操作数据库 </font>**

## 本质

**<font size=4>简单的来说，就是写这个JDBC的公司定义的一套操作关系型数据库的规则，所以由此可知它就像一个接口一样，**
**然后像MySql或者Oracle这些厂商来提供”实现类“——驱动jar包，这样就可以利用Java来进行操作数据库操作</font>**

**java.sql：所有与JDBC访问数据库相关的接口和类**
**javax.sql：数据库扩展包，提供数据库额外的功能。如：连接池**
**数据库的驱动：由各大数据库厂商提供，需要额外去下载，是对JDBC接口实现的类**

## 步骤

**<font size=4>1.导入驱动jar包（在项目中新建一个目录将jar包复制粘贴到该目录下）</font>**

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201016120101928-1915597736.jpg)

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201016120108424-1420466427.jpg)

**<font size=4>2.用java注册驱动</font>**（注：从JDBC3开始，目前已经普遍使用的版本。可以不用注册驱动而直接使用。Class.forName这句话可以省略。建议是写上此语句）

```java
Mysql例: Class.forName("com.mysql.jdbc.Driver");
```

```
Oracle例：Class.forName("oracle.jdbc.driver.OracleDriver");
```

**<font size=4>3.获取数据库的连接对象</font>**

```
例: Connection con =DriverManger.getConnection(url:"jdbc:mysql://locallhost:3306/数据库名",user"",password:"")
	***DriverManger是驱动管理对象***
	功能:1.注册驱动     Class.forName("com.mysql.jdbc.Driver");
		（其实是根据deregisterDriver这个注册驱动的方法来实现的；且从mysql5之后的驱动jar包j会自动进行注册  驱动）
	    2.获取数据库连接
	      .参数：url  user  password
		  .mysql语法：jdbc:mysql://ip地址(域名):端口号/数据库名称
		
	***Connection是数据库连接对象***
		1.获取执行sql的对象
		  .Statement createStatement()
		  .PreparedStaement preparStatement(String sql)
		2.管理事务 
		  .开启事务:setAutoCommit(boolean autoCommit): 调用该方法设置参数为false，即开启事务
		  .提交事务:commit()
		  .回滚事务:rollback()
```

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201016120229274-1158024759.jpg)



**<font size=4>4.定义sql语句</font>**

```
例: String sql =" /*写上你要做的sql语句*/";
```

**<font size=4>5.获取执行sql语句的对象，即Statement</font>**

```
例: Statement stmt = con.createStatement();
	Statement是执行sql的对象
```

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201016120317169-405051343.jpg)



**<font size=4>6.执行sql，接受返回结果</font>**

```
例: int count = stmt.executeUpdate(sql);
  /*执行DML语句（常用）、DDL语句*/
    boolean execute(String sql):可以执行任意的sql （不常用）
    ResultSet excuteQuery(String sql):执行DQL语句；返回结果集对象
```

**<font size=4>7.处理结果</font>**

```
例: System.out.println(count);//受影响的行数，然后根据受影响的行数来判断DML语句是否执行成功
```

**<font size=4>8.释放资源</font>**

```
例: stmt.close();
	con.close();
```

**<font size=4>9.ResultSet和PreparStatement对象</font>**

```
ResultSet是结果集对象，即封装查询结果的
	**boolean next()方法**:游标向下移动一行；返回值为boolean
	**getXxx(参数)方法**:获取数据；Xxx代表数据类型；比如：getInt()、getString()、getDouble()
						通过传参可以进行获取相应的数据；比如：int中的数据就是列的编号，String中的数据就是列的名称
	正确的步骤应该是：1.游标向下移动一行
				   2，判断是否有数据（利用循环简化判断）
				   3.获取数据
PreparStatement是执行sql的对象，功能比父类Statement更为强大
```

## 实例代码

<font size=4>```以下为菜鸟教程中的代码！```</font>

> ```java
> import java.sql.Connection;
> import java.sql.DriverManager;
> import java.sql.ResultSet;
> import java.sql.Statement;
> 
> public class DbUtil {
> 
>  public static final String URL = "jdbc:mysql://localhost:3306/imooc";
>  public static final String USER = "liulx";
>  public static final String PASSWORD = "123456";
> 
>  public static void main(String[] args) throws Exception {
>      //1.加载驱动程序
>      Class.forName("com.mysql.jdbc.Driver");
>      //2. 获得数据库连接
>      Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
>      //3.操作数据库，实现增删改查
>      Statement stmt = conn.createStatement();
>      ResultSet rs = stmt.executeQuery("SELECT user_name, age FROM imooc_goddess");
>      //如果有数据，rs.next()返回true
>      while(rs.next()){
>          System.out.println(rs.getString("user_name")+" 年龄："+rs.getInt("age"));
>      }
>  }
> }
> ```

**<font size=4>进行增删改查</font>**

> ```java
> public class DbUtil {
>  public static final String URL = "jdbc:mysql://localhost:3306/imooc";
>  public static final String USER = "liulx";
>  public static final String PASSWORD = "123456";
>  private static Connection conn = null;
>  static{
>      try {
>          //1.加载驱动程序
>          Class.forName("com.mysql.jdbc.Driver");
>          //2. 获得数据库连接
>          conn = DriverManager.getConnection(URL, USER, PASSWORD);
>      } catch (ClassNotFoundException e) {
>          e.printStackTrace();
>      } catch (SQLException e) {
>          e.printStackTrace();
>      }
>  }
> 
>  public static Connection getConnection(){
>      return conn;
>  }
> }
> 
> //模型
> package liulx.model;
> 
> import java.util.Date;
> 
> public class Goddess {
> 
>  private Integer id;
>  private String user_name;
>  private Integer sex;
>  private Integer age;
>  private Date birthday; //注意用的是java.util.Date
>  private String email;
>  private String mobile;
>  private String create_user;
>  private String update_user;
>  private Date create_date;
>  private Date update_date;
>  private Integer isDel;
>  //getter setter方法。。。
> }
> 
> //---------dao层--------------
> package liulx.dao;
> 
> import liulx.db.DbUtil;
> import liulx.model.Goddess;
> 
> import java.sql.Connection;
> import java.sql.ResultSet;
> import java.sql.SQLException;
> import java.sql.Statement;
> import java.util.ArrayList;
> import java.util.List;
> 
> public class GoddessDao {
>  //增加
>  public void addGoddess(Goddess g) throws SQLException {
>      //获取连接
>      Connection conn = DbUtil.getConnection();
>      //sql
>      String sql = "INSERT INTO imooc_goddess(user_name, sex, age, birthday, email, mobile,"+
>          "create_user, create_date, update_user, update_date, isdel)"
>              +"values("+"?,?,?,?,?,?,?,CURRENT_DATE(),?,CURRENT_DATE(),?)";
>      //预编译
>      PreparedStatement ptmt = conn.prepareStatement(sql); //预编译SQL，减少sql执行
> 
>      //传参
>      ptmt.setString(1, g.getUser_name());
>      ptmt.setInt(2, g.getSex());
>      ptmt.setInt(3, g.getAge());
>      ptmt.setDate(4, new Date(g.getBirthday().getTime()));
>      ptmt.setString(5, g.getEmail());
>      ptmt.setString(6, g.getMobile());
>      ptmt.setString(7, g.getCreate_user());
>      ptmt.setString(8, g.getUpdate_user());
>      ptmt.setInt(9, g.getIsDel());
> 
>      //执行
>      ptmt.execute();
>  }
> 
>  public void updateGoddess(){
>      //获取连接
>      Connection conn = DbUtil.getConnection();
>      //sql, 每行加空格
>      String sql = "UPDATE imooc_goddess" +
>              " set user_name=?, sex=?, age=?, birthday=?, email=?, mobile=?,"+
>              " update_user=?, update_date=CURRENT_DATE(), isdel=? "+
>              " where id=?";
>      //预编译
>      PreparedStatement ptmt = conn.prepareStatement(sql); //预编译SQL，减少sql执行
> 
>      //传参
>      ptmt.setString(1, g.getUser_name());
>      ptmt.setInt(2, g.getSex());
>      ptmt.setInt(3, g.getAge());
>      ptmt.setDate(4, new Date(g.getBirthday().getTime()));
>      ptmt.setString(5, g.getEmail());
>      ptmt.setString(6, g.getMobile());
>      ptmt.setString(7, g.getUpdate_user());
>      ptmt.setInt(8, g.getIsDel());
>      ptmt.setInt(9, g.getId());
> 
>      //执行
>      ptmt.execute();
>  }
> 
>  public void delGoddess(){
>      //获取连接
>      Connection conn = DbUtil.getConnection();
>      //sql, 每行加空格
>      String sql = "delete from imooc_goddess where id=?";
>      //预编译SQL，减少sql执行
>      PreparedStatement ptmt = conn.prepareStatement(sql);
> 
>      //传参
>      ptmt.setInt(1, id);
> 
>      //执行
>      ptmt.execute();
>  }
> 
>  public List<Goddess> query() throws SQLException {
>      Connection conn = DbUtil.getConnection();
>      Statement stmt = conn.createStatement();
>      ResultSet rs = stmt.executeQuery("SELECT user_name, age FROM imooc_goddess");
> 
>      List<Goddess> gs = new ArrayList<Goddess>();
>      Goddess g = null;
>      while(rs.next()){
>          g = new Goddess();
>          g.setUser_name(rs.getString("user_name"));
>          g.setAge(rs.getInt("age"));
> 
>          gs.add(g);
>      }
>      return gs;
>  }
> 
>  public Goddess get(){
>      Goddess g = null;
>      //获取连接
>      Connection conn = DbUtil.getConnection();
>      //sql, 每行加空格
>      String sql = "select * from  imooc_goddess where id=?";
>      //预编译SQL，减少sql执行
>      PreparedStatement ptmt = conn.prepareStatement(sql);
>      //传参
>      ptmt.setInt(1, id);
>      //执行
>      ResultSet rs = ptmt.executeQuery();
>      while(rs.next()){
>          g = new Goddess();
>          g.setId(rs.getInt("id"));
>          g.setUser_name(rs.getString("user_name"));
>          g.setAge(rs.getInt("age"));
>          g.setSex(rs.getInt("sex"));
>          g.setBirthday(rs.getDate("birthday"));
>          g.setEmail(rs.getString("email"));
>          g.setMobile(rs.getString("mobile"));
>          g.setCreate_date(rs.getDate("create_date"));
>          g.setCreate_user(rs.getString("create_user"));
>          g.setUpdate_date(rs.getDate("update_date"));
>          g.setUpdate_user(rs.getString("update_user"));
>          g.setIsDel(rs.getInt("isdel"));
>      }
>      return g;
>  }
> }
> ```

## 关于PreparedStatement

**<font size=5>PreparedSatement的好处</font>**

> 1.prepareStatement()会先将SQL语句发送给数据库预编译。PreparedStatement会引用着预编译后的结果。可以多次传入不同的参数给PreparedStatement对象并执行。减少SQL编译次数，提高效率。
> 2.安全性更高，没有SQL注入的隐患。
> 3.提高了程序的可读性

**<font size=5> 使用PreparedStatement的步骤：</font>**

> 1)编写SQL语句，未知内容使用?占位："SELECT * FROM user WHERE name=? AND password=?";
> 2)获得PreparedStatement对象
> 3)设置实际参数：setXxx(占位符的位置, 真实的值)
> 4)执行参数化SQL语句
> 5)关闭资源

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201016120340972-285314008.jpg)







