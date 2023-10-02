[Home ](../../README.md)  

# Exercise 2: Create the OnlineShop Application

## Introduction

In this exercise, you will use the package `Z_ONLINESHOP_###`that you have created earlier. 
Here you will create a database table where you will define all important fields for the OnlineShop application.  

This RAP business object (BO) represents an online shop, where you can order laptops or other articles you need as an employee. <!--After an article such as a laptop is ordered, a purchase requisition can be created by pressing a button in your application which will trigger an action in your RAP BO.-->  

We will start our implementation by building a simple managed RAP business object and we will add the business logic to call the released RAP API in SAP S/4HANA afterwards.

You will use an ADT wizard to generate all the needed development RAP artefacts of your UI service. This includes the data model, projection view, service definition and service binding. Afterwards you will check your _OnlineShop_ application with the SAP Fiori elements preview. 

> **Reminder:**   
> Don't forget to replace all occurences of the placeholder **`###`** with your group ID in the exercise steps below.  
> You can use the ADT function **Replace All** (**Ctrl+F**) for the purpose.    


## Exercise 2.1: Create database table

Create a database table![table](../../images/adt_tabl.png) to store the _OnlineShop_ data.   
A OnlineShop entity defines general data, such as the product name or the quantity that is ordered. Once the order is checked out the number of the purchase requisition that will be created by using our released API will be stored as well.   

> Hint: 
> The tasks are also desribed in the following tutorial (step 2). Just replace the names with those that are mentioned in this how to guide.  
> https://developers.sap.com/tutorials/abap-environment-rap100-generate-ui-service.html

   1. Right-click on your ABAP package **`Z_ONLINESHOP_###`** and select **New** > **Other ABAP Repository Object** from the context menu.
         
   2. Search for **database table**, select it, and click **Next >**.
   
   3. Maintain the required information (`###` is your group ID) and click **Next >**.
      - Name: **`ZONLINESHOP_###`**  
      - Description: _**`Persistence for online shop`**_                  

   4. Select your transport request, and click **Finish** to create the database table.
   
   5. Replace the default code with the code snippet provided below and replace all occurences of the placeholder **`###`** with your group ID using the **Replace All** function (**Ctrl+F**).    
 
      > **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="../../images/copyrawcontents.png" alt="table" width="30px"> appearing in the upper-right corner to copy it. 
      
<pre lang="ABAP">
@EndUserText.label : 'Persistence for online shop'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #RESTRICTED
define table zonlineshop_XXX {
  key client            : abap.clnt not null;
  key order_uuid        : sysuuid_x16 not null;
  order_id              : abap.char(10) not null;
  product               : abap.char(40) not null;
  quantity              : abap.int4;
  purchase_requisition  : abap.char(10);
  overall_status        : abap.char(40);
  created_by            : abp_creation_user;
  created_at            : abp_creation_tstmpl;
  last_changed_by       : abp_lastchange_user;
  last_changed_at       : abp_lastchange_tstmpl;
  local_last_changed_at : abp_locinst_lastchange_tstmpl;

}
</pre>
       
   6. Save ![save icon](../../images/adt_save.png) and activate ![activate icon](../../images/adt_activate.png) the changes.
   
## Exercise 2.2: Generate the transactional UI service

Create your OData V4 based UI service with the built-in RAP generator.   
The generated business service will be transactional, draft-enabled, and enriched with UI semantics for the generation of the Fiori elements app.

> Hint: 
> The tasks are also desribed in the following tutorial (step 2). Just replace the names with those that are mentioned in this how to guide.  
> https://developers.sap.com/tutorials/abap-environment-rap100-generate-ui-service.html


   1. In the **Project Explorer** (**Dictionary**) right-click your database table ![table](../../images/adt_tabl.png)**`ZONLINESHOP_###`** and select **Generate ABAP Repository Objects** from the context menu.        
   
   2. Maintain the required information  (`###` is your group ID) and click **Next >**:
        - Generator: **`ABAP RESTful Application Programming Model: UI Service`**
        
   3. Maintain the required information on the **Configure Generator** dialog to provide the name of your data model and generate them.         

      For that, navigate through the wizard tree (_Business Objects_, _Data Model_, etc...), maintain the artefact names provided in the table below, 
      and press **Next >**.
 
      Verify the maintained entries and press **Next >** to confirm. 

      > ℹ **Info about Naming Conventions**     
      > The main aspects of the naming conventions of SAP S/4HANA's Virtual Data Model (VDM) are used in this exercise.  
      > More information on VDM can be found on the SAP Help portal: **[Here](https://help.sap.com/docs/SAP_S4HANA_CLOUD/0f69f8fb28ac4bf48d2b57b9637e81fa/8a8cee943ef944fe8936f4cc60ba9bc1.html)**.
 
  
      
      | **RAP Layer**          |  **Artefacts**           | **Artefact Names**                                       |     
      |:---------------------- |:------------------------ |:-------------------------------------------------------- |
      | **Business Object**    |                          |                                                          |                        
      |                        |  **Data Model**          |  Data Definition Name:   **`ZR_ONLINESHOP_###`**    |
      |                        |                          |  Alias Name:             **`onlineshop`**                    |   
      |                        |  **Behavior**            |  Implementation Class:   **`ZBP_R_ONLINESHOP_###`**   |
      |                        |                          |  Draft Table Name:       **`ZDONLINESHOP_###`**          |
      | **Service Projection** (BO Projection)  |         |  Name:                   **`ZC_ONLINESHOP_###`**    |   
      | **Business Services**  |                          |                                                          |          
      |                        |  **Service Definition**  |  Name:         **`ZUI_ONLINESHOP_###`**               |
      |                        |  **Service Binding**     |  Name:         **`ZUI_ONLINESHOP_O4_###`**            |
      |                        |                          |  Binding Type: **`OData V4 - UI`**                       |
                       
      
   4. Select a transport request, and click **Finish**. The needed artefacts will be generated.

   5. Go to the **Project Explorer**, select your package ![package](../../images/adt_package.png)**`Z_ONLINESHOP_###`**, refresh it by pressing **F5**, and check all generated ABAP repository objects 


 
## Exercise 2.3: Preview the OnlineShop App using Fiori elements


In this exercise you will publish the local service endpoint of your service binding ![service binding](../../images/adt_srvb.png) and start the _Fiori elements App Preview_.

   1. Open your service binding ![service binding](../../images/adt_srvb.png)**`ZUI_ONLINESHOP_O4_###`** and click **Publish**.

   ![Publish](images/105_publish_service_binding_on_prem.png)
   
   2. Double-click on the entity **`onlineshop`** in the **Entity Set and Association** section to open the _Fiori elements App Preview_.   

   ![Preview](images/107_publish_service_binding_on_prem.png)
   
   3. If prompted, sign in with the user and password provided by the instructors. You should see a Fiori elements application like this

   ![Fiori elements app](images/109_publish_service_binding_on_prem.png)


      
<!--
## Exercise 2.4: Preview the Online Shop App in SAP S/4HANA on premise


> Publishing the local service endpoint of your service binding **in on premise systems** does not work from within ADT. 
> Therefore you have to publish the Service Binding locally using transaction **/IWFND/V4_ADMIN**.

> Hint:
> The screen shots show the steps for the *Travel* app. Please use the names and strings provided in this script in **step 4 & 5** and do NOT enter the names you see on the screen shots.  

<details>
  <summary>Click to expand!</summary>

   1. In the menu click on the button *Run ABAP Development Object as ABAP Application in SAPGUI* or press **Alt+F8**
 
      ![start_transaction](images/100_publish_service_binding_on_prem.png)   
   
   2. Type **/iwfnd/v4_admin** as a search string and double-click on the entry **/IWFND/V4_ADMIN (Transaction)**   
     
      ![v4_admin](images/110_publish_service_binding_on_prem.png)   
   
   3. Click the button **Publish Service Groups** to get a list of service groups that can be published.
 
      ![v4_admin](images/120_publish_service_binding_on_prem.png)  
 
   4. Enter following values to search for the service group of your service and press the button **Get Service Groups**   
      
      System Alias: `LOCAL`  
      Service Group ID: `Z*###*`  

      ![v4_admin](images/130_publish_service_binding_on_prem.png)        

   5. Select the entry `ZUI_ONLINESHOP_O4_###` from the list and press the button **Publish Service Groups**   
 
      ![v4_admin](images/140_publish_service_binding_on_prem.png) 
 
   6. In the following popup enter a meaningful description such as `Online Shop App ###`   
      
      ![v4_admin](images/150_publish_service_binding_on_prem.png) 
 
   7. You are now asked to provide a customizing request. Choose an existing customizing request or create a new one and choose a meaningful description.
 
      ![v4_admin](images/160_publish_service_binding_on_prem.png)   
 
   8. Confirm the success message and press **Enter**. 
 
      ![v4_admin](images/170_publish_service_binding_on_prem.png)    
 
   9. Navigate back to your service binding in the project explorer. Right click on it and choose **Refresh**   
 
      ![v4_admin](images/180_publish_service_binding_on_prem.png)   ** 
 
   10. Check that your service bindings is now published and choose the entity **OnlineShop** and press the button **Preview**   
 
</details>

-->

## Summary 


Now that you've... 
- created an ABAP package,
- created a database table,
- created a transactional UI service,
- published a local service point, and started the _Fiori elements App Preview_ in ADT.

You can continue with the next exercise - **[Exercise 3: Adapt the data model](../ex3/README.md)**.


---
<!--
## Appendix


Find the source code for the database table definition and the data generator class in the [sources](sources) folder. Don't forget to replace all occurences of the placeholder `###` with your group ID.

- ![document](../../images/doc.png) [Table ZONLINESHOP_###](sources/ZONLINESHOP_%23%23%23.txt)
-->
