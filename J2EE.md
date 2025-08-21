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

##### 5) Way to create a servlet?
###### i. Extending GenericServlet
`````
import java.io.*;
import javax.servlet.*;

public class MyFirstServlet extends GenericServlet

{
    public void service(ServletRequest req, ServletResponse resp) throws ServletException, IOException
    {
        resp.setContentType("text/html");
        PrintWriter pw = resp.getWriter();
        pw.println("<html>");
        pw.println("<head><title>My first Servlet</title></head>");
        pw.println("<body>");
        pw.println("<h2>Welcome To Servlet World!</h2>");
        pw.println("</body>");
        pw.println("</html>");
        pw.close();
    }
}
`````
###### ii. Implementing the Servlet Interface
`````
import javax.servlet.*;
import java.io.IOException;
import java.io.PrintWriter;

public class MyServlet implements Servlet {

    private ServletConfig config;

    @Override
    public void init(ServletConfig config) throws ServletException {
        this.config = config;
        System.out.println("Servlet initialized");
    }

    @Override
    public ServletConfig getServletConfig() {
        return config;
    }

    @Override
    public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
 out.println("</body></html>");
    }

    @Override
    public String getServletInfo() {
        return "MyServlet - a basic implementation of the Servlet interface";
    }

    @Override
    public void destroy() {
        System.out.println("Servlet destroyed");
    }
}

`````

###### iii. Extending HttpServlet
`````
import javax.servlet.http.*;
import java.io.*;

public class MyHttpServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");
        PrintWriter out = res.getWriter();
        out.println("Hello from HttpServlet!");
    }
}
`````
##### 6) What is a session?
###### A session stores user data on the server temporarily, starting when the user logs in and ending when they log out or close the browser.
##### 7) Session Management?
###### By default, the HTTP protocol is stateless, i.e., we cannot remember the data from previous to previous transactions.
###### To remember the data across all the transactions, we use the concept of a session.
###### There are 3 ways to perform session tracking.
###### i. Using a hidden field.
`````
// Java program to demonstrate
// Hidden form field method

package GeeksforGeeks;

import java.io.*;
import javax.servlet.*;
import javax.servlet.annotation.WebServlet; // Importing annotation
import javax.servlet.http.*;

// using this annotation we dont need
// xml file for dispathing servlet
@WebServlet("/SecondServlet")

public class SecondServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    {
        try {
            response.setContentType("text/html");
            /*
             The response's character encoding is only set from the given
             content type if this method is called before getWriter is called.
             This method may be called repeatedly to change content type and
             character encoding.
             */
            PrintWriter out = response.getWriter();

            /*
             The Java PrintWriter class ( java.io.PrintWriter ) enables you to
             write formatted data to an underlying Writer . For instance,
             writing int, long and other primitive data formatted as text,
             rather than as their byte values
             */
            // getting value from the query string
            String username = request.getParameter("username");

            // taking the value of username from First servlet using getparameter object
            out.print("WELCOME " + username);

            // out.println is used to print on the client web browser
            out.close();
        }
        catch (Exception e) {
            System.out.println(e);
        }
    }
}
`````

###### ii. Cookies
###### A cookie is a key-value pair sent by the server to the client, which the browser stores and sends back with future requests to the same server.
`````
> Create a Cookie:
Cookie cookie = new Cookie("username", "rahul");
response.addCookie(cookie); // sends cookie to client

> Read Cookies from Request:
Cookie[] cookies = request.getCookies();
if (cookies != null) {
    for (Cookie c : cookies) {
        if (c.getName().equals("username")) {
            String user = c.getValue();
        }
    }
}

> Set Cookie Expiry:
cookie.setMaxAge(60 * 60); // 1 hour

> Delete a Cookie:
cookie.setMaxAge(0); // deletes the cookie
response.addCookie(cookie);

`````
###### types of cookies
###### 1. Session Cookies
###### Stored in: Browser memory (not saved to disk).
###### Expires: When the browser is closed.
###### Use case: Temporary data like login status during a single session.

`````
Cookie sessionCookie = new Cookie("sessionId", "abc123");
// No expiry set → session cookie
response.addCookie(sessionCookie);

`````

###### 2. Persistent Cookies
###### Stored in: Disk (saved by the browser).
###### Expires: After a specified time.
###### Use case: Remembering user preferences, login info across sessions.

`````
Cookie persistentCookie = new Cookie("username", "rahul");
persistentCookie.setMaxAge(60 * 60 * 24 * 7); // 7 days
response.addCookie(persistentCookie);

`````

###### 3. Secure Cookies
###### Sent only over: HTTPS connections.
###### Use case: Sensitive data like authentication tokens.
`````
Cookie secureCookie = new Cookie("authToken", "xyz789");
secureCookie.setSecure(true); // only sent over HTTPS
response.addCookie(secureCookie);

`````

######  4. HttpOnly Cookies
###### Accessible by: Server-side only (not JavaScript).
###### Use case: Prevent XSS attacks by hiding cookies from client-side scripts.
`````
secureCookie.setHttpOnly(true); // not accessible via JavaScript

`````

###### 5. SameSite Cookies (Servlet 4.0+ or via headers)
###### Controls: Cross-site request behavior.
###### Values: Strict, Lax, or None.
###### Use case: CSRF protection.
`````
// Not directly supported in older Servlet APIs; set via response header
response.setHeader("Set-Cookie", "user=rahul; SameSite=Strict");

`````

###### Example
###### servlet1
`````
import jakarta.servlet.*;
import jakarta.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class Servlet1 extends HttpServlet {

    protected void
    processRequest(HttpServletRequest request,
                   HttpServletResponse response)
        throws ServletException, IOException
    {
        response.setContentType("text/html;charset=UTF-8");
        try (PrintWriter out = response.getWriter()) {
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Servlet Servlet1</title>");
            out.println("</head>");
            out.println("<body>");

            // Creating a string to store the name
            String name = request.getParameter("name");
            out.println("<h1> Hello, welcome to " + name
                        + " </h1>");
            out.println(
                "<h1><a href =\"servlet2\">Go to Servlet2</a></h1>");
            // Creating a cookie
            Cookie c = new Cookie("user_name", name);
            response.addCookie(c);

            out.println("</body>");
            out.println("</html>");
        }
    }
}
`````

###### servlet 2
`````
import jakarta.servlet.*;
import jakarta.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class Servlet2 extends HttpServlet {

    protected void
    processRequest(HttpServletRequest request,
                   HttpServletResponse response)
        throws ServletException, IOException
    {
        response.setContentType("text/html;charset=UTF-8");
        try (PrintWriter out = response.getWriter()) {
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Servlet Servlet2</title>");
            out.println("</head>");
            out.println("<body>");

            // Fetching cookies(if found more than one)
            // Array of Cookies
            Cookie[] cookies = request.getCookies();
            boolean f = false;
            String name = "";
            if (cookies == null) {
                out.println(
                    "<h1>You are new user, go to home page and submit your institute's name");
                return;
            }
            else {
                for (Cookie c : cookies) {
                    String tname = c.getName();
                    if (tname.equals("user_name")) {
                        f = true;
                        name = c.getValue();
                    }
                }
            }
            if (f) {
                out.println("<h1> Hello, welcome back "
                            + name + " </h1>");
                out.println("<h2>Thank you!!</h2>");
            }
            else {
                out.println(
                    "<h1>You are new user, go to home page and submit your institute's name");
            }

            out.println("</body>");
            out.println("</html>");
        }
    }
}
`````
###### iii. HttpSession
###### Servlets use the HttpSession interface to manage sessions.
`````
> Session Creation:
HttpSession session = request.getSession(); // creates a new session or returns existing one

> Storing Data in Session:
session.setAttribute("username", "rahul");

> Retrieving Data from Session:
String user = (String) session.getAttribute("username");

> Invalidating a Session (e.g., on logout):
session.invalidate();

`````
###### Example
`````
import javax.servlet.http.*;
import javax.servlet.annotation.WebServlet;
import java.io.*;

@WebServlet("/sessionExample")
public class SessionExampleServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        HttpSession session = request.getSession();
        session.setAttribute("user", "Rahul");

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("Session created. User: " + session.getAttribute("user"));
    }
}

`````
##### 8) Difference between Servlet and JSP

| Feature      |Servlet         | JSP (JavaServer Pages) |
|:-------------|:--------------:|-----------------------:|
| Purpose      | Handles business logic and request processing| Handles presentation logic (HTML + Java) |
| Code Type     | Pure Java code      | HTML with embedded Java code|
| Compilation | Compiled into .class files manually or by server | Translated into a servlet by the server automatically|
| Lifecycle    | Managed by servlet container | Converted to servlet, then managed similarly |
| Best Use Case | Form handling, session management, backend logic | Displaying data, UI templates |


##### 9) What is a Servlet Filter?
###### In Servlets, a Filter is a reusable piece of code that can intercept and process requests and responses before they reach a servlet or after the servlet has processed them.
###### Filters are part of the Java EE (Jakarta EE) specification and are commonly used for tasks like logging, authentication, input validation, and compression.

###### Example
###### javax.servlet.Filter
`````
public interface Filter {
    void init(FilterConfig filterConfig) throws ServletException;
    void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
        throws IOException, ServletException;
    void destroy();
}

`````

###### Example: Logging Filter
`````
import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

@WebFilter("/hello") // applies to /hello servlet
public class LoggingFilter implements Filter {

    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("LoggingFilter initialized");
    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("Request received at: " + new java.util.Date());
        chain.doFilter(request, response); // pass request to next filter or servlet
    }

    public void destroy() {
        System.out.println("LoggingFilter destroyed");
    }
}

`````

###### Common Use Cases
`````
Logging request details
Authentication and authorization
Input validation and sanitization
Compression (e.g., GZIP)
Setting response headers
Caching control
`````

##### 9) Explain the web.xml file in a servlet?
###### In a Servlet-based Java web application, the web.xml file (also called the deployment descriptor) is an XML configuration file located in the WEB-INF directory. It defines how servlets, filters, listeners, and other components are deployed and interact within the web application.

######  Purpose of web.xml
`````
Configure servlets and their URL mappings
Define filters and listeners
Set initialization parameters
Configure session timeout
Handle error pages
Define welcome files
Control security settings
`````
###### Basic Structure of web.xml
`````
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         version="3.1">

    <!-- Servlet Declaration -->
    <servlet>
        <servlet-name>HelloServlet</servlet-name>
        <servlet-class>com.example.HelloServlet</servlet-class>
    </servlet>

    <!-- Servlet Mapping -->
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <!-- Filter Declaration -->
    <filter>
        <filter-name>LoggingFilter</filter-name>
        <filter-class>com.example.LoggingFilter</filter-class>
    </filter>

    <!-- Filter Mapping -->
    <filter-mapping>
        <filter-name>LoggingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- Welcome File -->
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!-- Error Page -->
    <error-page>
        <error-code>404</error-code>
        <location>/error404.jsp</location>
    </error-page>

</web-app>

`````

###### Key Tags in web.xml
`````
> <servlet>           - Declares a servlet class
> <servlet-mapping>   - Maps servlet to a URL pattern
> <filter>            - Declares a filter class
> <filter-mapping>    - Maps filter to a URL pattern
> <welcome-file-list> - Defines default page when app is accessed
> <error-page>        - Custom error handling
> <context-param>     - Application-wide parameters
> <session-config>    - Session timeout configuration
`````

###### Servlet 3.0+ Alternative
###### In modern Java EE (Servlet 3.0+), you can use annotations like @WebServlet, @WebFilter, and @WebListener instead of web.xml.
<img width="300" height="300" alt="webxml" src="https://github.com/user-attachments/assets/52b57b79-0854-4a1a-9e7e-8da977044ef0" />

##### 10) Difference between ServletContext and ServletConfig

