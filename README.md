/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package project_login;

import java.sql.*;
import javax.swing.*;
import java.awt.event.*;

public class Login implements ActionListener {

    Connection con;
    Statement stmt;
    ResultSet rs;
    
    JFrame f = new JFrame("User Login");
    JLabel l1 = new JLabel("Username");
    JLabel l2 = new JLabel("Password");
    JTextField text1 = new JTextField(20);
    JTextField text2 = new JTextField(24);
    JButton button = new JButton("Login");
    
    
    public Login() {        
        DoConnect();
        frame();
    }
    
    public void DoConnect(){
        
        try{
        String host = "jdbc:derby://localhost:1527/newLogin";
        String uName = "ioana";
        String uPass= "ioana23";
        con = DriverManager.getConnection( host, uName, uPass ); 
        stmt = con.createStatement( );
        
        }
        
        catch ( SQLException err ) {
        System.out.println( err.getMessage( ) );
       }
    }
    
    public void frame() {
        
        f.setSize(800, 300);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setVisible(true);
        
        JPanel p = new JPanel();
        p.add(l1);
        p.add(text1);
        p.add(l2);
        p.add(text2);
        p.add(button);
        
        f.add(p);
        
        button.addActionListener(this);

        
    }
    
    @Override
      public void actionPerformed(ActionEvent ae) {
        //throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        
          try{
                String user = text1.getText().trim();
                String pass = text2.getText().trim();
                //Execute sone SQL and load the records into the resultset
                
                String SQL = "SELECT FIRSTNAME,PASSWORD FROM studentLogin";
                rs = stmt.executeQuery( SQL );
                
               
                
             while(rs.next()){
             //int stuID = rs.getInt("id");
                    String firstName = rs.getString("firstName");
             if(firstName.equals(user)){
                 
                    String password = rs.getString("password");
                 if(password.equals(pass)){
                     System.out.println("You have logged in!!");
                     
                 }
                 
             }           
            
            }         
                           
                
        }
                
        catch ( SQLException err ) {
        System.out.println( err.getMessage( ) );
       }
    }
    
    public static void main(String[] args) {        
        new Login();
    }
}

