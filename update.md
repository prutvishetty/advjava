import java.sql.*;
import java.io.PrintWriter;
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet("/update3")
public class update3 extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out=response.getWriter();
		
		String url="jdbc:mysql://localhost:3306/demo";
		String username="root";
		String password="";
		try {
			Class.forName("com.mysql.jdbc.Driver");
			Connection conn=DriverManager.getConnection(url,username,password);
			
			
			int usn=Integer.parseInt(request.getParameter("usn"));
			String name=request.getParameter("name");
			
			String sql= "update table2 set name=? where usn=?";
			PreparedStatement ps=conn.prepareStatement(sql);
			ps.setInt(2, usn);
			ps.setString(1, name);
			
            int q=ps.executeUpdate();
			
			if(q>0) {
				out.println("<html><body>successeful</body></html>");
			}
			else {
				out.println("<html><body> it was not successfull </body></html>");
			}
			
			
			
		}catch(ClassNotFoundException | SQLException e) {
			e.printStackTrace();
			
		}
	}

}
