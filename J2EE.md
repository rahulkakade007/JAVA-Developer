### JDBC
##### 1)What is JDBC?
###### JDBC helps our applications to communicate with the DB.
###### It allows a Java program to access a DB, run queries, retrieve, and manipulate the data.
##### 2) JDBC Architecture?
<img width="300" height="300" alt="jdbc_architecture" src="https://github.com/user-attachments/assets/e7c2c60e-553f-43f3-aefb-6fc326260790" />

######  i. Application: It can be a Java application or a servlet that communicates with a data source.
###### ii. JDBC API: It allows Java programs to execute SQL queries and get results from the DB.

``````
Some Key Components of JDBC API
-> Interfaces like Driver, ResultSet, RowSet, PreparedStatement,
   and Connection that help manage different DB tasks.
-> Classes like DriverManager, Types, Blob, and Clob that help manage DB connections.
``````
###### iii. Driver Manager: It plays a crucial role in the JDBC architecture. It uses some DB-specific drivers to connect the application to the DB efficiently. 
###### iv. JDBC Driver: These drivers handle the interaction between the application and the DB.

##### 3) Steps to perform SQL DB using JDBC
###### Step 1: Register the Driver required.
`````
Class.forName("com.mysql.cj.jdbc.Driver");
`````
###### Step 2: Establish the connection
`````
Connection connection = DriverManager.getConnection(
"jdbc:mysql://localhost:3306/your_database",
"your_username",
"your_password");
`````
###### Step 3: Create Statement
`````
Statement statement = connection.createStatement();
`````
###### Step 4: Execute Query
`````
// Execute the query
ResultSet rs = st.executeQuery("select * from students");

// Process the results
        while (rs.next()) {
            String name = rs.getString("name"); // Retrieve name from db
            System.out.println(name); // Print result on console
          // Or System.out.println(rs.getString(2));
        }
`````
###### Step 5: Close connection
`````
// Close the statement and connection
        statement.close();
        connection.close();
`````

##### 4) Types of JDBC Drivers
###### i. Type 1 [JDBC-ODBC-Driver]
<img width="300" height="300" alt="jdbc type1" src="https://github.com/user-attachments/assets/8e9af811-9153-40f5-bd60-b721c899bbd1" />

###### In this, JDBC calls are converted into ODBC calls(open DB connectivity).
###### Further, ODBC would generate the native calls to connect with a specific DB.
###### ii. Type 2 [pure Java + native calls]
<img width="300" height="300" alt="jdbc type 2" src="https://github.com/user-attachments/assets/823f1a65-b294-4563-9ebe-57134ead816d" />

###### In this, JDBC calls are directly converted into native calls.
###### This could not be implemented successfully because of no support given by DB vendors.

###### iii. Type 3 [Network protocol]
<img width="300" height="300" alt="jdbc type 3" src="https://github.com/user-attachments/assets/47c11674-7a22-43dd-a432-c5608a45202f" />

###### In this, JDBC calls are given to an intermediate server, then this server, depending on calls, connects with a specific DB.
###### Drawback: Latency to transform info from JDBC to DB.

###### iv. Type 4 [Thin Driver]
<img width="300" height="300" alt="jdbc type 4" src="https://github.com/user-attachments/assets/2495342f-a2e8-4759-91a6-a764a350efb3" />

###### This driver directly interacts with the DB.
###### It does not require any native DB library.

##### 5) Types of Statements in JDBC
###### i. Statement: It is used for general-purpose access to DB and is useful for executing static SQL statements at runtime.
`````
Statement statement = connection.createStatement();
`````
###### Implementations:
`````
> execute(String SQL): It is used to execute any SQL statements.
> executeUpdate(String SQL): It returns the no of rows affected by SQL statements.
> ResultSet executeQuery(String SQL): It executes the select query and returns an object.
`````
###### ii. PreparedStatement: It is a precompiled SQL statement that can be executed multiple times.
###### It accepts parameterized SQL queries with ? as a placeholder for a parameter, which can be set dynamically.
`````
// SQL Query with parameters
    String query = "SELECT * FROM students WHERE age > ? AND name = ?";

// Create PreparedStatement
   PreparedStatement myStmt = con.prepareStatement(query);

// Set parameters
    myStmt.setInt(1, 20);
    myStmt.setString(2, "Prateek");

// Execute query
    ResultSet myRs = myStmt.executeQuery();

// Display results
    System.out.println("Name\tAge");
    while (myRs.next()) {
    String name = myRs.getString("name");
    int age = myRs.getInt("age");
    System.out.println(name + "\t" + age);
    }
`````

###### iii. CallableStatement: It is used to execute the stored procedure in the DB.
`````
// Create a CallableStatement
   CallableStatement cs = con.prepareCall("{call GetPeopleInfo()}");

// Execute the stored procedure
   ResultSet res = cs.executeQuery();

// Process the results
   while (res.next()) {
     // Print and display elements (Name and Age)
        System.out.println("Name : " + res.getString("name"));
        System.out.println("Age : " + res.getInt("age"));
            }
`````
##### 6) Connection pooling in JDBC?
###### Connection pooling is a technique used to maintain a pool of reusable database connections, which can be shared among multiple clients. This approach significantly improves performance by reducing the overhead of establishing new connections and efficiently managing resources.
##### 7) Explain how to use transactions in JDBC?
###### To use transactions in JDBC, you first disable the auto-commit mode using connection.setAutoCommit(false). Then, you can execute multiple statements and commit the transaction using connection.commit() or rollback using connection.rollback() if an error occurs.
##### 8) Explain the difference between a ResultSet and a ResultSetMetaData?
###### A ResultSet is an object that holds data retrieved from a database query, allowing you to iterate through the results. 
###### ResultSetMetaData provides information about the types and properties of the columns in a ResultSet, such as column names and data types.
#
### Servlet
##### 1) What is a servlet?
###### Servlet is a Java class that helps us build dynamic web applications.
##### 2) What is a dynamic web application?
###### A dynamic web application refers to a website or web-based software that generates content and functionality in real-time based on user input, server-side processing, and data retrieved from a database.
##### 3) States of the Servlet Life Cycle?
<img width="300" height="300" alt="State of servlet life cycle" src="https://github.com/user-attachments/assets/2dd8b30b-45a5-4e96-b238-09955e99cc7e" />

`````
1. Loading a Servlet
The first stage of the Servlet lifecycle involves loading and initializing the Servlet. The Servlet container performs the following operations:
Loading: The Servlet container loads the Servlet class into memory.
Instantiation: The container creates an instance of the Servlet using the no-argument constructor.

2. Initializing a Servlet
After the Servlet is instantiated, the Servlet container initializes it by calling the init(ServletConfig config) method. This method is called only once during the Servlet's life cycle.

3. Handling request
Once the Servlet is initialized, it is ready to handle client requests. The Servlet container performs the following steps for each request:
Create Request and Response Objects
The container creates ServletRequest and ServletResponse objects.
For HTTP requests, it creates HttpServletRequest and HttpServletResponse objects.

Invoke the service() Method
The container calls the service(ServletRequest req, ServletResponse res) method.
The service() method determines the type of HTTP request (GET, POST, PUT, DELETE, etc.) and delegates the request to the appropriate method (doGet(), doPost(), etc).

4. Destroying a Servlet
When the Servlet container decides to remove the Servlet.
`````
##### 4) Servlet Life Cycle Methods?
`````
> For the first time, when the request hits the server, Tomcat will load the servlet in the catalina/tomcat container.
> The first method to be executed is init(). It will create a request and response object.
> Then, the request will be sent to the service(). It will get executed depending on the kind of request (doGet()/doPost()).
> For the subsequent request init() will get skip and request goto service() directly.
> The object created by init() will be reused for subsequent requests. So, the performance of the servlet is good.
> Finally, once destroy() is executed, the servlet's life cycle ends.
`````

##### 5) 
