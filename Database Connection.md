**5) DIFFERENT WAYS IN JAVA TO INTERACT WITH THE DB TABLE:**

**To establish a JDBC connection with Oracle or MySQL, you need to follow a specific set of steps.**

**I) LOAD THE DRIVER:**

**First, you need to load the JDBC driver, which acts as a bridge between Java application and the database. You can do this using <code>Class.forName()</code> or by relying on your build system (like Maven or Gradle) to include the necessary driver.</strong>

**For Oracle:**

**Class.forName("oracle.jdbc.driver.OracleDriver");**

**MySQL:**

**Class.forName("com.mysql.cj.jdbc.Driver");**

**II) ESTABLISH THE CONNECTION:**

**You need to use <code>DriverManager.getConnection()</code> to establish a connection with the database, passing the connection URL, username, and password.</strong>

**For Oracle:**

**String url = "jdbc:oracle:thin:@localhost:1521:xe";**

**String user = "oracleUsername";**

**String password = "oraclePassword";**

**Connection connection = DriverManager.getConnection(url, user, password);**

**For MySQL:**

**String url = "jdbc:mysql://localhost:3306/dbName";**

**String user = "mysqlUsername";**

**String password = "mysqlPassword";**

**Connection connection = DriverManager.getConnection(url, user, password);**

**The port defaults to <code>3306</code> for MySQL and <code>1521</code> for Oracle.</strong>

**III) CREATING AND EXECUTING A STATEMENT:**

**After establishing a connection, create a <code>Statement</code> or <code>PreparedStatement</code> to execute queries:</strong>

**Statement stmt = connection.createStatement();**

**ResultSet rs = stmt.executeQuery("SELECT * FROM table_name");**

**DEFINITION:**



* **The <code>Statement</code> object is responsible for sending SQL commands (queries, updates) to the database.</strong>
* <strong><code>Statement stmt</code>: This is the variable <code>stmt</code> of type <code>Statement</code>. It will be used to run SQL queries after the <code>createStatement()</code> method is called.</strong>
* <strong>The <code>executeQuery</code> method of the <code>Statement</code> object is used to execute the SQL query</strong>
* <strong>The result of the query (the data retrieved from the table) is stored in a <code>ResultSet</code> object (<code>rs</code>), which holds the data returned by the SQL query.</strong>

<strong>IV) CLOSE THE RESOURCES:</strong>

**Always close the <code>Connection</code>, <code>Statement</code>, and <code>ResultSet</code> to free up resources:</strong>


```
rs.close();
stmt.close();
connection.close();
```


**V)ERROR HANDLING:**

**You should handle <code>SQLException</code> to catch issues related to the database.</strong>

try {

    // JDBC operations

} catch (SQLException e) {

    e.printStackTrace();

}