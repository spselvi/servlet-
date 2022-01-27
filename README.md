Servlet Interface:
     Servlet interface defines methods that all.It must implement Servlet interface needs to be implemented for creating any servlet (either directly or indirectly). It provides 3 life cycle methods that are used to initialize the servlet.
Method:
public void init(ServletConfig config)-initializes the servlet
public void service(ServletRequest request,ServletResponse response)-provides response for the incoming request.
public void destroy()-is invoked only once and indicates that servlet is being destroyed.
public ServletConfig getServletConfig()-returns the object of ServletCon
public String getServletInfo()-returns information about servlet such as writer, copyright, version etc.
eg:
import java.io.*;  
import javax.servlet.*;  
public class First implements Servlet{  
ServletConfig config=null;  
public void init(ServletConfig config){  
this.config=config;  
System.out.println("servlet is initialized");  
}  
public void service(ServletRequest req,ServletResponse res)  
throws IOException,ServletException{  
res.setContentType("text/html");  
PrintWriter out=res.getWriter();  
out.print("<html><body>");  
out.print("<b>hello simple servlet</b>");  
out.print("</body></html>");  
}  
public void destroy(){System.out.println("servlet is destroyed");}  
public ServletConfig getServletConfig(){return config;}  
public String getServletInfo(){return "copyright 2007-1010";}  
  
}  
HttpServlet class
The HttpServlet class extends the GenericServlet class and implements Serializable interface.http specific methods such as doGet, doPost, doHead, doTrace etc.
public void service(ServletRequest req,ServletResponse res)
protected void service(HttpServletRequest req, HttpServletResponse res)
protected void doGet(HttpServletRequest req, HttpServletResponse res)
protected void doPost(HttpServletRequest req, HttpServletResponse res)
protected void doHead(HttpServletRequest req, HttpServletResponse res)
protected void doOptions(HttpServletRequest req, HttpServletResponse res)
protected void doPut(HttpServletRequest req, HttpServletResponse res)
protected void doTrace(HttpServletRequest req, HttpServletResponse res)
protected void doDelete(HttpServletRequest req, HttpServletResponse res)
Life Cycle of a Servlet :
      Servlet class is loaded
         The servlet class is loaded when the first request for the servlet is received by the web container.
     Servlet instance is created
         The web container creates the instance of a servlet after loading the servlet class. The servlet instance is created only once in the servlet life cycle.
     init method is invoked:
         The web container calls the init method only once after creating the servlet instanc
      service method is invoked
          The web container calls the service method each time when request for the servlet is received
      destroy method is invoked
          The web container calls the destroy method before removing the servlet instance from the service.
Steps to create a servlet example:
      Create a directory structures
          The directory structure defines that where to put the different types of files so that web container may get the information and respond to the client.
      Create a Servlet
          By implementing the Servlet interface
          By inheriting the GenericServlet class
           By inheriting the HttpServlet class
eg:
       import javax.servlet.http.*;  
       import javax.servlet.*;  
       import java.io.*;  
       public class DemoServlet extends HttpServlet{  
       public void doGet(HttpServletRequest req,HttpServletResponse res)  
       throws ServletException,IOException  
       {  
        res.setContentType("text/html"); 
       PrintWriter pw=res.getWriter();  
       pw.println("<html><body>");  
       pw.println("Welcome to servlet");  
        pw.println("</body></html>");  
       pw.close();//closing the stream  
}}
Compile the servlet
      servlet-api.jar	Apache Tomcat
      weblogic.jar	Weblogic
      javaee.jar	Glassfish
      javaee.jar	JBoss
 web.xml file
     <web-app>  
     <servlet>  
     <servlet-name>sonoojaiswal</servlet-name>  
      <servlet-class>DemoServlet</servlet-class>  
     </servlet>  
     <servlet-mapping>  
     <servlet-name>sonoojaiswal</servlet-name>  
    <url-pattern>/welcome</url-pattern>  
</servlet-mapping>  
</web-app>
How web container handles the servlet request:
    maps the request with the servlet in the web.xml file.
    creates request and response objects for this request
    calls the service method on the thread
    The public service method internally calls the protected service method
    The protected service method calls the doGet method depending on the type of request.
    The doGet method generates the response and it is passed to the client.
    After sending the response, the web container deletes the request and response objects. The thread is contained in the thread pool or deleted depends on the server         implementation.
 public service method:
     public void service(ServletRequest req, ServletResponse res)  
        throws ServletException, IOException  
    {  
        HttpServletRequest request;  
        HttpServletResponse response;  
        try  
        {  
            request = (HttpServletRequest)req;  
            response = (HttpServletResponse)res;  
        }  
        catch(ClassCastException e)  
        {  
            throw new ServletException("non-HTTP request or response");  
        }  
        service(request, response);  
    }  
    War File:
       A war (web archive) File contains files of a web project. It may have servlet, xml, jsp, image, html, css, js etc. files.
    Advantage of war file:
       Saves time
   create war file:
       To create war file, you need to use jar tool of JDK.
       c is used to create file, -v to generate the verbose output and -f to specify the arhive file name.
    deploy the war file:
       By server console panel
       By manually having the war file in specific folder of server.
    welcome-file-list in web.xml
       The welcome-file-list element of web-app, is used to define a list of welcome files. Its sub element is welcome-file that is used to define the welcome file.
       welcome-file-list in web.xml
       index.html
       index.htm
       index.jsp
  Creating Servlet Example in Eclipse
      Create a Dynamic web project
      create a servlet
      add servlet-api.jar file
      Run the servlet
 ServletRequest Interface
     ServletRequest is used to provide the client request information to a servlet such as content type, content length, parameter names and values, header informations, attributes etc.
 Methods:
    public String getParameter(String name)
    public String[] getParameterValues(String name)
    public int getContentLength()
    public String getCharacterEncoding()
    public String getContentType()
Example of ServletRequest to display the name of the user:
    <form action="welcome" method="get">  
    Enter your name<input type="text" name="name"><br>  
    <input type="submit" value="login">  
    </form> 
 DemoServ.java
 import javax.servlet.http.*;  
 import javax.servlet.*;  
 import java.io.*;  
 public class DemoServ extends HttpServlet{  
 public void doGet(HttpServletRequest req,HttpServletResponse res)  
 throws ServletException,IOException  
 {  
 res.setContentType("text/html");  
 PrintWriter pw=res.getWriter();  
 String name=req.getParameter("name");//will return value  
 pw.println("Welcome "+name);  
 pw.close();  
}}
RequestDispatcher in Servlet:
   The RequestDispatcher interface provides the facility of dispatching the request to another resource it may be html, servlet or jsp.
Method:
 public void forward(ServletRequest request,ServletResponse response)throws ServletException,java.io.IOException
 
    
