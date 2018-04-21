# JSP
In this to create JSP-JDBC
/* HTML FIle
<html>
<body>
<h4>Product Details:</h4>
<form action="Register.jsp">
Enter Product Id:<input type="text" name="pid" size="20"><br>
Enter Product name:<input type="text" name="pname" size="20"><br>
Enter price:<input type="text" name="price" size="20"><br>
<input type="submit" value="submit">
</body>
</html>


/* JSP-page */

/ Register.jsp /

<html>
<body>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<%@page import="java.sql.*,java.util.*"%>
<%!
 Connection con=null;
 PreparedStatement pst=null;
public void jspInit()
{
	try{
		Class.forName("com.mysql.jdbc.Driver");
		con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test","root","root");
	}catch(Exception e)
	{
		e.printStackTrace();
	}
}
public void jspDestroy()
{
	try{
		if(con!=null)
		{
			con.close();
			
		}
		if(pst!=null)
		{
			pst.close();
		}
	}catch(Exception e)
	{
		e.printStackTrace();
	}
}
%>
<%
	try
	{
		
	String pid=request.getParameter("pid");
	String pname=request.getParameter("pname");
	double price=Double.parseDouble(request.getParameter("price"));
	pst=con.prepareStatement("insert into product(pid,pname,price)values(?,?,?)");
	pst.setString(1,pid);
	pst.setString(2,pname);
	pst.setDouble(3,price);
	pst.executeUpdate();
	String s1="Record saved";
	}
	catch(Exception e)
	{
		%>
<h1><%=e %></h1>
	<%}
%>

</body>
</html>
