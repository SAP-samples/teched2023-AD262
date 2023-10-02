# How to connect to an SAP S/4HANA on premise or private cloud system 

This document describes how to create an **ABAP Project** to connect to an SAP S/4HANA on premise or private cloud system.  


1. Click on  **File > New > New ABAP Project**

   ![New ABAP Project](images/100_create_a_new_abap_project.png)

2. In the *System Connection* dialogue click on the link **new system connection**  

   ![System Connection](images/110_create_a_new_abap_project.png)

3. In the *Connection Settings* dialogue choose the connection type **Custom Application Server**  
   
   Then enter the following connection information (The IP address of the application server is provided by the instructors)
   - System ID: S4H
   - Application Server: xxx.xxx.xxx.xxx
   - Instance Number: 00
   
   and **deactivate** the check box **Activate Secure Network Communication (SNC)**
   
   Press Next.   

   ![Connection Settings](images/120_create_a_new_abap_project.png)

4. In the *Logon to System* dialogue enter the following data. The user for you and the password are provided to you by the instructors
    
   - Client: 100
   - User: lowcode###
   - Password: xxxxxxxx
   - Language: EN

   Press Next

   ![Logon to System](images/130_create_a_new_abap_project.png)
   
5. In the *Project Name* screen leave the default value proposed by ADT.
  
   ![Project Name](images/140_create_a_new_abap_project.png)

6. Press **Finish**.   

7. Add `ZLOCAL` to your favorites packages.  

   - Right click on the folder **Favorite Packages** in your newly created ABAP project.   

   ![add_to_favorites](images/99_100_add_zlocal_to_favorites.png)  
   
   - Search for `ZLOCAL`. Select the entry and press **OK**.   
   
   ![add_to_favorites](images/99_110_add_zlocal_to_favorites.png) 
   

Continue to - [Exercise 1: Create an ABAP Package](../ex1/README.md) 
