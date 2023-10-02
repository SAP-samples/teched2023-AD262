# Exercise 2: Create a Process in SAP Build Process Automation based on the Onlineshop Service

In this chapter you will build a whole process in SAP Build Process Automation. It will contain a UI with a form with which users can create requests for products in our onlineshop. Depending on the quantity there will then be an approval step where a manager will have to approve or reject the onlineshop request. If the quantity is low, the request will automatically be approved. In case of an approval an action to create a new onlineshop entry based on the onlineshop service you have built in the S/4HANA system using ABAP Cloud. The result can then be seen in the Fiori elements preview application based on the onlineshop service.

Remember that wherever in this exercise you see `###` to replace it with your **group ID** that was given to you by the instructors.

## Exercise 2.1: Create a new Process in SAP BUild Process Automation

You will create the project for a process.

1. Choose `Lobby`in SAP Build. Press `Create`. Select `Build and Automated Process` and then `Business Process`.

![lobby](images/100.png)

![lobby](images/110.png)

2. Choose `Onlineshop###Process` as your Project Name and press `Create`.

![lobby](images/120.png)

3. The process project is being created and your are prompted to create a process within this project. Choose `Onlineshop####` as a name, leave the identifier as suggested by the system.

![lobby](images/130.png)

## Exercise 2.2: Add a Form to the Process

You will create a UI form for the process, where users can request the order of a product with a quantitiy in the onlineshop.

1. On the canvas of the process, press `+` on the trigger step that the system has already generated for you. Choose `Formss` and `New Form`.

![lobby](images/140.png)

2. Choose `Onlineshop###Form` as a name and press `Create`.

![lobby](images/145.png)

The new form is now embedded into the trigger of the process.

3. On the form choose `Open Editor`.

![lobby](images/150.png)

You can now see a new canvas on which you can place a number of UI elements that make up your form. This is what users will see when they want to request a product in the onlineshop.

4. From the left side pane, choose `Headline 1` and drag it to the Canvas and drop it there. Write `Enter the product and the quantity that you want to order` into the headline. Now choose `Text` and drag and drop it to the canvas. Change the fields label to `Product`. Now choose `Number` and drag and drop it to the canvas. Change the fields label to `Quantity`. Finally, press `Save`.

![lobby](images/155.png)

## Exercise 2.3: Add an Approval step to the Process

You will create a an approval step for the onlineshop request. This is a UI that will pop up in an approver's (e.g. manager) `My Inbox` application, where the approver will see the product and the quantity that was ordered and can approve or reject the request.

1. On the process canvas, press on the `+` after the process trigger, then choose `Approvals` and `New Approval Form`.

![lobby](images/160.png)

2. Choose `Onlineshop###Approval` as a name. Mark the `Based on a Form` checkbox and select the form that you have created in the previous step. Press `Create`

![lobby](images/165.png)

If you hadn't chosen to base the approval on the form, you would get an empty canvas and you could design the approval UI from scratch. However, since approvals usually contain a lot of information that was entered in the original form, it is a good idea to copy the forms UI elements over into the approval and then adjust where needed.

3. Click on the new approval step on the canvas. On the right side pane choose the `General` tab. Place the cursor into the the `Subject` field and write `Approve order of`, then select the `Product` field that is suggested to you from your form. Under `Users` enter the email address of the user that was given to you by the instructor. 

![lobby](images/170.png)

This step determines who gets the approval request in their `My Inbox` application. In a real scenario the reveiver might be determined dynamically and of course the requestor would not be the approver. For yor tests however, you want to see the approval in your inbox, make sure you use the right email address. 

4. Switch to the `Inputs` tab. Assign the `Product` and `Quantity` fields from your form to the corresponding fields of the approval. Press `Save`

![lobby](images/175.png)

This is a general pattern in Process Automation: There are outputs from a previous step, in this case the form that triggers the process and there are inputs for the follow up step like our approvals. Inputs and outputs need to be mapped.

5. On the approval on the canvas press `Open Editor`

![lobby](images/180.png)

6. On the approval UI that now pops up and that contains the fields from your form, change the headline to be `Approval for order`, leave the rest of the fields as they are. `Save` your work

![lobby](images/185.png)

## Exercise 2.4: Add an Action step to the Process

You will now add an action step that uses the action to add a new entry to the onlineshop that you have created in the exercise before. This action is invoked when the request from the form has been successfully approved.

1. Press the `+` of `Approve` to the right of the approval step and choose `Actions` and `Browser Library`.

![lobby](images/190.png)

2. On the dialog search for the action `Onlineshop###Action`that you created before. Choose the `Add new entity to onlineshop` one and close the dialog.

![lobby](images/220.png)

3. On the right hand pane, choose to `Create Destination Variable`. On the following dialog, choose `MyDestination` as an identifier. Press `Create`

![lobby](images/225.png)

![lobby](images/230.png)

This variable will later contain the name of the destination that you have created in an earler exercise.

4. On the right hand pane choose the `Inputs` tab. Map the `product` field to the `Product` of the form and do the same for the `quantity` field from the `Quantity` in the form. `Save` your work.

![lobby](images/235.png)

5. On the canvas, press the `+` on the `Reject` end of the approval and drag and drop it to the `End` step of your process.

![lobby](images/260.png)

This makes sure that if the request is rejected by an approver, the action is not invoked and therefore no new onlineshop entry is created in the S/4HANA backend

## Exercise 2.5: Add an Condition step to the Process

In this exercise you will add a condition step to the process. It will check whether the ordered quantity from the form is equal or less to 1 and if so, bypass the approval step.

1. On the process canvas, press the `+` on the right of your process trigger and choose `Controls` and `Condition`.

![lobby](images/240.png)

2. On the right side pane for the condition, press on the `Open Condition Editor`

![lobby](images/245.png)

3. On the dialog, choose the `Quantity` field from you form in the field on the very left. As a condition in the middler, choose `is greate than` from the list. As a value in the field on the very right, choose `1`. Press `Apply`.

![lobby](images/250.png)

4. On the canvas, choose the `+` on the `Default` branch of the condition and drag and drop it to your action step.

![lobby](images/255.png)

With this the approval step is bypassed when the condition is not met, i.e. when the quantity is 1.

With this, you have finished building the process. 


## Exercise 2.6: Release and Deploy your process

In this part, you will release the project and deploy it to the BTP, so it can be tested and used for onlineshop requests.

1. On your process canvas, first make sure that you `Save` all your work. Once the `Save` button is inactive, press on the `Release` button above

![lobby](images/270.png)

2. Optionally add some comment for the released version. Press `Release`.

![lobby](images/275.png)

Like for the actions before, this freezes the current state of your process. You can of course change the process afterwards, but you can always go back to this frozen, released state.

3. Where the `Release` button was, there is now a `Deploy` button. Press it.

![lobby](images/280.png)

4. On the dialog that now appears, press `Next` for the first step.

![lobby](images/285.png)

This step shows all the artefacts that are part of the deployed process

5. On the `Runtime Variables` step, choose your destination `Onlineshop_###` with the `Set new value` radiobutton selected. Press `Next`

![lobby](images/290.png)

This makes sure that your process action is bound to the destination when it is carried out. The destination is available here because you have registerd it under `Settings` in an earlier step.

6. Press `Deploy` on the `Triggers` step.

![lobby](images/295.png)

## Exercise 2.7: Test your Process

With the process now deployed, you can finally test the whole scenario!

1. On the canvas, click on your form in the trigger step. On the right hand pane, under tab `General` copy the link in the field `From link`

![lobby](images/300.png)

2. Open a new browser window and past the link into it. You should see a form like below. Enter a product name of your liking and a quantiy that is greater than 1, e.g. 2. Press `Submit`

![lobby](images/310.png)

This is how a user will request a product, starting the process.

Next up, let's check whether there is an approval step for this now.

3. On the SAP Build window that contains the Lobby, click on the button on the right for `MyInbox`

![lobby](images/315.png)

4. The `MyInbox` application comes up and it should show an entry that corresponds with the request from the form that you just submitted. Select the entry and look at the approval text, it should contain the ordered product and quantity, that you just submitted. Press `Approve`.

![lobby](images/320.png)

5. Check whether there is a new entry in your Onlineshop Preview Fiori elements app, you might still have the corresponding browser window open. If you need to open it again, go back to your ABAP Development tools and open it again (See [here](../../..//rap/exercises/ex2#exercise-23-preview-the-onlineshop-app-using-fiori-elements) again, how to do that).

![lobby](images/325.png)

6. Now try bring up a new form of the process. This time however, enter a `quantity` of only `1` in your from and submit it.

![lobby](images/330.png)

As the quantity is only 1 and you had added a condition in the process to bypass the approval step and directly carry out the action in your process if this condition is met, you should now see a new entry for the onlineshop in the Fiori elements preview.

7. Check whether there is a new entry in the Onlineshop Preview app, press `Go`.

![lobby](images/335.png)

You should see your new entry!

## Summary

This concludes the workshop!

You have successfully built a new Onlineshop API on an S/4HANA system using ABAP Cloud capabilities. You have then create a new process using SAP Build Process Automation that makes use of this new API. The process contains the entry of an onlineshop request, an approval step as well as calling the API to create a new Onlineshop entry.