# <a name="apex-workflow"></a>21. APEX Workflow

With APEX 23.2, workflows are directly integrated into APEX. With **APEX Workflow**, business processes can be created and executed using a graphical editor. Users who want to model processes using **Business Process Model and Notation (BPMN 2.0)** will find a suitable extension with the closely related **Flows for APEX** extension by MT - IT Solutions. More information can be found at the link [https://flowsforapex.org/](https://flowsforapex.org/).

In the following chapter, we use workflows to create a demo version of a simplified restaurant table reservation. The demo is based on the blog post **Simplify Business Process Management Using APEX Workflow** by Ananya Chatterjee. [Link to the blog](https://blogs.oracle.com/apex/post/simplify-business-process-management-using-apex-workflow-create-doctor-appointment-application)

## <a name="starting-point-use-case-and-flow-chart"></a>21.1 Starting Point Use Case and Flow-Chart

As a starting point for the task in this chapter, we assume that a restaurant wants to implement a simple booking form via the website. In the form, guests can submit a reservation request for a table. In the next step, the system first checks whether a table is available for the desired number of people at the desired time. If not, an email is immediately sent to the guest with a rejection of the appointment. If a table is available, the request is passed on to a restaurant staff member. The staff member decides whether to accept the reservation. If declined, a rejection is again sent by email; if accepted, the reservation is saved and the guest is informed of the successful reservation by email.

- The following **Flow-Chart** visualizes this use case.

![](../../assets/Chapter-21/APEX_Workflows_01.png)

## <a name="workflow-setting-up-required-elements"></a>21.2 Setting Up Required Elements

- The required tables and packages have already been installed via the **script for the tutorial** in Chapter 1.

- For the APP, you need a user named **COOK**, who will later be responsible for processing reservation requests. Create a corresponding user.

- Click on the **Administration** icon in the top right and select **Manage Users and Groups**.

- Click on **Create User**.

- Enter the following:
  - Name: COOK
  - Email Address: test@abc.com
  - Password: 12345678
  - Confirm Password: 12345678
  - Require Change of Password on First Use: No

- Then create a new APP using the **App Builder** and **Create**. Give the app the title **MT Tutorial - Dinner Reservation**.

![](../../assets/Chapter-21/APEX_Workflows_02.jpg)

## <a name="creating-the-workflow"></a>21.3 Creating the Workflow

- The next step is the actual task. First, we create a **Workflow**.

- Return to the **Application Builder** of the new app and click on **Shared Components**.

![](../../assets/Chapter-21/APEX_Workflows_03.jpg)

- In the Shared Components, select **Workflows** under **Workflows and Automations**.

![](../../assets/Chapter-21/APEX_Workflows_04.jpg)

- Create a new workflow by clicking on **Create**. You will then be directed to the **Workflow Editor**. An initial basic workflow is already visible in the center of the **Diagram Builder**.

![](../../assets/Chapter-21/APEX_Workflows_05.jpg)

- Set the name of the workflow to **Dinner Reservation** and the **Static ID** to **DINNERRSVRT**. Set the Title to: **Workflow for Guest &GUEST_NAME. &GUEST_LAST_NAME.**.

![](../../assets/Chapter-21/APEX_Workflows_06.jpg)

- Set the **Workflow Version** to **1.0**.

![](../../assets/Chapter-21/APEX_Workflows_07.jpg)

- Currently, an error occurs because the automatically created activity has not yet been defined. To save, delete the activity. Right-click on the **Activity** on the left column and select **Delete**. Alternatively, you can also select the activity in the editor and click on the symbol with the three dots.

![](../../assets/Chapter-21/APEX_Workflows_08.jpg)

- The **Start of the Activity**, the **Arrow**, and the **Endpoint** remain. Drag the **Arrowhead** in the editor to the **Endpoint** and then save.

![](../../assets/Chapter-21/APEX_Workflows_09.jpg)

- Next, create a series of **Input Parameters** that provide data to the workflow. Right-click again on the workflow and select **Create Parameter**.

![](../../assets/Chapter-21/APEX_Workflows_10.jpg)

- Give the first parameter the **Static ID: GUEST_NAME**, the **Label: Guest Name**. It is a **Data Type: VARCHAR2**.

![](../../assets/Chapter-21/APEX_Workflows_11.jpg)

- Create the following additional parameters:

  | | |  
  |--|--|
  | **GUEST_LAST_NAME** | *VARCHAR2*|
  | **GUEST_EMAIL** | *VARCHAR2* |
  | **GUEST_COUNT** | *NUMBER*|  
  | **REQUEST_START_DATE** | *TIMESTAMP*|
  | **REQUEST_END_DATE** | *TIMESTAMP*|
  | | |

- The parameters **REQUEST_START_DATE** and **REQUEST_END_DATE** receive the format mask **DD.MM.YYYY HH24:MI** under **Session State Format Mask**.

![](../../assets/Chapter-21/APEX_Workflows_12.jpg)

- Now link the table **T_RESTAURANT_STAFF** under **Additional Data** with Workflow 1.0. This will later ensure that the created tasks can be assigned to corresponding handlers. Additionally, the columns of the table are available as bind variables for the workflow. Choose the column **RST_ID** as the **Primary Key Column**.

![](../../assets/Chapter-21/APEX_Workflows_13.jpg)

- Besides the input parameters, you also need changeable variables in the workflow that can be used in the process. To do this, next create **Workflow Variables**. Right-click again on Workflow 1.0 and select **Create Variable**.

![](../../assets/Chapter-21/APEX_Workflows_14.jpg)

- Name the first variable **Static ID: RESERVATION_ID** and **Label: Reservation ID**. The **Data Type** is **NUMBER**. A value will be assigned to the variable only at a later time, so the **Value** is initially **Null**.

![](../../assets/Chapter-21/APEX_Workflows_15.jpg)

- Now create the variable **TABLE_ID** following the same scheme: **Static ID: TABLE_ID**, **Label: Table ID**, and **Data Type** is **NUMBER**. Also set **Value** to **Null** here.

![](../../assets/Chapter-21/APEX_Workflows_16.jpg)

- The next variable to create is **AVAILABILITY**. It is of type **BOOLEAN**. Under **True Value**, enter **AVAIL** and under **False Value**, enter **UNAVAIL**. These are the two possible return values of a function that will be integrated into the workflow later. Then save the workflow through **Save**.

![](../../assets/Chapter-21/APEX_Workflows_17.jpg)

## <a name="creating-task-for-reservation-request"></a>21.4 Creating Task for Reservation Request

- The next step is to create the task for confirmation (or rejection) of the reservation request. Switch to **Shared Components** and then to **Task Definitions**. Click on **Create** to create a new task.

![](../../assets/Chapter-21/APEX_Workflows_18.jpg)

- In the dialog window for creating the **Task Definition**, name the task **Reservation Request** and set the **Subject: Reservation for Guest &GUEST_NAME. &GUEST_LAST_NAME.**. The **Static ID** is **RESERVATION_REQUEST**. Click on **Create**.

![](../../assets/Chapter-21/APEX_Workflows_19.jpg)

- Next, set the **Action Source** to **SQL Query**. Enter the following query in the field for the query:

```sql
  select * from t_restaurant_staff where rst_id = :APEX$TASK_PK
  ```

![](../../assets/Chapter-21/APEX_Workflows_20.jpg)

- Add a new row to the table **Participants**. The **Participant Type** is **Potential Owner**, the **Value Type** is **Expression**, and the **Value** is **:RST_NAME**. This refers to the corresponding column in the staff table **T_RESTAURANT_STAFF** who will be allowed to handle tasks.

![](../../assets/Chapter-21/APEX_Workflows_21.jpg)

- Parameters are also provided for the task. Add the following rows to the parameter table:

  | | | |  
  |--|--|--|
  | **NAME_GUEST** | Name Guest | *String* |
  | **LAST_NAME_GUEST** | Last Name Guest | *String* |
  | **COUNT_GUEST** | Count Guest | *String*|  
  | **RESERVATION_DATE_START** | Reservation Date Start | *String* |
  | **RESERVATION_DATE_END** | Reservation Date End | *String* |
  | | | |

![](../../assets/Chapter-21/APEX_Workflows_22.jpg)

- Confirm the additions to the task via the **Apply Changes** button. You will first return to the **Task Definitions**. But switch back to the **Reservation Request** task and create a new page under **Task Details Page**. Give the page the number **11**.

![](../../assets/Chapter-21/APEX_Workflows_22b.jpg)

## <a name="completion-of-the-workflow"></a>21.5 Completion of the Workflow

- The next step continues with work on the workflow. Therefore, go back to **Workflows** in **Shared Components** and click on **Dinner Reservation**.

![](../../assets/Chapter-21/APEX_Workflows_23.jpg)

- In **Workflow 1.0** under **Activities**, right-click to create a new activity.

![](../../assets/Chapter-21/APEX_Workflows_24.jpg)

- Name the new activity **Check Availability** and set the type to **Invoke API**. Choose the package **DINNER_RESERVATION_DEMO** and from it the function **CHECK_AVAILABILITY**.

![](../../assets/Chapter-21/APEX_Workflows_25.jpg)

- Pass the result of the function to the parameter **Function Result**, specifically in **Item** through the **Version Variable** **Availability**.

![](../../assets/Chapter-21/APEX_Workflows_26.jpg)

![](../../assets/Chapter-21/APEX_Workflows_27.jpg)

- For the parameters **pi_guest_count**, **pi_start_date**, and **pi_end_date**, set **Value** to type **Item** and then to the following **Workflow Parameters** and **Format Masks**:

  | Parameter | Item | Format Mask |
  | --- | --- | --- |  
  | **pi_guest_count** | GUEST_COUNT | |
  | **pi_start_date** | REQUEST_START_DATE | DD.MM.YYYY HH24:MI |
  | **pi_end_date** | REQUEST_END_DATE | DD.MM.YYYY HH24:MI |
  | | | |

![](../../assets/Chapter-21/APEX_Workflows_28a.jpg)

![](../../assets/Chapter-21/APEX_Workflows_28.jpg)

![](../../assets/Chapter-21/APEX_Workflows_29.jpg)

- Connect the arrow from the start of the workflow to the activity.

![](../../assets/Chapter-21/APEX_Workflows_30.jpg)

- To handle the result of the query activity, a **Switch** is needed. Create one, for example by dragging it into the diagram builder.

![](../../assets/Chapter-21/APEX_Workflows_31.jpg)

- The new **Name** of the Switch will be **Decide availability**. Under **Condition**, choose the **Condition Type: Workflow Variable = Value** and the **Workflow Variable: AVAILABILITY** and the value **AVAIL**, which the function returns if a table for the desired number of people is available on the desired date.

![](../../assets/Chapter-21/APEX_Workflows_32.jpg)

- Now connect the two activities **Check availability** and **Decide availability** with each other. You can draw a new arrow and connect to the target activity via the plus sign.

![](../../assets/Chapter-21/APEX_Workflows_33.jpg)

- Next, the first possible result of the check follows: The case where the check shows that **no table** is available. In this case, an email will be sent informing the requestor that no table is available. Create a **Send E-Mail Activity** for this.

![](../../assets/Chapter-21/APEX_Workflows_34.jpg)

- The name of this activity becomes **Send Mail unavailable**. In the **To-field**, enter the parameter with the guest's email using **&GUEST_EMAIL.**. Set the email subject in the **Subject** field to **Your reservation: No table available**. In the **Body Plain Text** field, enter the following email text:

```
Dear &GUEST_NAME. &GUEST_LAST_NAME., 

Unfortunately, there is no table available at the requested time. Please try another time!

With kind regards
The Restaurant Team
```
![](../../assets/Chapter-21/APEX_Workflows_35.jpg)

- Connect the switch with the email activity via an arrow.

![](../../assets/Chapter-21/APEX_Workflows_36.jpg)

- Choose the arrow and set the connection under **Name** to the title **Unavailable**. The **Condition** in this case is **FALSE**, as the email should be sent when the check shows that no table is available.

![](../../assets/Chapter-21/APEX_Workflows_37.jpg)

- Create another **Workflow End** and connect it with the mail-send activity. You can then save the workflow temporarily.

![](../../assets/Chapter-21/APEX_Workflows_38.jpg)

- Now we continue with the case where the initial check shows that a table is available. For this case, an employee should decide whether to accept the reservation. To do this, first create a **Human Task - Create** activity. Give the activity the name **Create Reservation Request**, under **Definition** select the previously created task **Reservation Request**. Set the **Details Primary Key Item** to **RST_ID**. Choose **TASK_OUTCOME** for **Outcome** and **APPROVER** for **Owner**.

![](../../assets/Chapter-21/APEX_Workflows_39.jpg)

- Next, set the **Parameters** of this activity to the following values:

  | Name | Type | Item |
  | --- | --- | --- |  
  | **Count Guest** | Item | *GUEST_COUNT*|
  | **Last Name Guest** | Item | *GUEST_LAST_NAME*| 
  | **Name Guest** | Item | *GUEST_NAME*|  
  | **Reservation Date Start** | Item | *REQUEST_START_DATE*|
  | **Reservation Date End** | Item | *REQUEST_END_DATE*|
  | | | |

![](../../assets/Chapter-21/APEX_Workflows_40.jpg)

- Connect the switch **Decide availability** with the activity **Create Reservation Request** via a new arrow. Name this connection **Available** and set the **Condition** to when **True**.

![](../../assets/Chapter-21/APEX_Workflows_41.jpg)

- To process the decision from the task, another **Switch** is needed. Create a new switch and give it the name **Decide Reservation approved**. The **Switch-Type** is **Check Workflow Variable**. The variable to be compared with in **Compare Variable** is set as **TASK_OUTCOME**.

![](../../assets/Chapter-21/APEX_Workflows_42.jpg)

- Connect **Create Reservation Request** with **Decide Reservation approved** via an arrow.

![](../../assets/Chapter-21/APEX_Workflows_43.jpg)

- Since an email should also be sent in case of a reservation rejection by the employee, connect **Decide Reservation approved** with **Send Mail unavailable**. Set the name to **Rejected**, the **Operator** to **Is Equal to**, and the **Value** to the result **REJECTED** from the Human Task. Then you can save again temporarily.

![](../../assets/Chapter-21/APEX_Workflows_44.jpg)

- In case of an approval, the next action retrieves a free table number to be assigned to the reservation. Add an **Invoke API** activity. Name it **Get free table**. The related package is again **DINNER_RESERVATION_DEMO**, and the **Function** is **GET_FREE_TABLE_ID**.

![](../../assets/Chapter-21/APEX_Workflows_45.jpg)

- **Function Result** of the activity is passed under **Item** to the variable **TABLE_ID**.

![](../../assets/Chapter-21/APEX_Workflows_46.jpg)

- Set the remaining parameters as follows (similar to **Check availability**).

  | Parameter | Item | Format Mask |
  | --- | --- | --- |  
  | **pi_guest_count** | GUEST_COUNT | |
  | **pi_start_date** | REQUEST_START_DATE | DD.MM.YYYY HH24:MI |
  | **pi_end_date** | REQUEST_END_DATE | DD.MM.YYYY HH24:MI |
  | | | |

- Connect the switch **Decide Reservation approved** with the **Get free table** activity. Set the connection name to **Approved**, the operator to **Is Equal to**, and the value to **APPROVED**.

![](../../assets/Chapter-21/APEX_Workflows_47.jpg)

- Now all the information is available to save the approved reservation. Create another **Invoke API** activity. Name it **Set reservation**. The package is **DINNER_RESERVATION_DEMO**, and the **Function** is **SET_RESERVATION**.

![](../../assets/Chapter-21/APEX_Workflows_48.jpg)

- The result of the function under **Function Result** in the **Parameters** is set to the variable **RESERVATION_ID**. Set the remaining parameters as follows:

  | Parameter | Item | Format Mask |
  | --- | --- | --- |  
  | **pi_dining_table_id** | TABLE_ID | |
  | **pi_guest_count** | GUEST_COUNT | |
  | **pi_guest_name** | GUEST_NAME | |
  | **pi_guest_last_name** | GUEST_LAST_NAME | |
  | **pi_guest_email** | GUEST_EMAIL | |
  | **pi_start_date** | REQUEST_START_DATE | DD.MM.YYYY HH24:MI |
  | **pi_end_date** | REQUEST_END_DATE | DD.MM.YYYY HH24:MI |
  | | | |

- The **pi_workflow_id** expects the current workflow's ID. The workflow ID can also be passed to the procedure via a **Static Value**. Enter **&APEX$WORKFLOW_ID.** here. Connect **Get free table** and **Set reservation**.

![](../../assets/Chapter-21/APEX_Workflows_49.jpg)

- After saving, the customer should then be informed by email that the reservation has been accepted. Add the corresponding **Send E-Mail** activity next and name it **Send confirmation**. In the **To** field, enter **&GUEST_EMAIL.**. The subject will be **Reservation Confirmation**. Use the following **Body Plain Text**:

```
Dear &GUEST_NAME. &GUEST_LAST_NAME., 

Hereby we confirm your reservation! We are looking forward to your stay on the following date: &REQUEST_START_DATE.!

With kind regards
The Restaurant Team
```

![](../../assets/Chapter-21/APEX_Workflows_50.jpg)

- Now connect the activities to each other and integrate the free **Workflow End** as the endpoint of the workflow. Then save the workflow.

![](../../assets/Chapter-21/APEX_Workflows_51.jpg)

## <a name="workflow-creating-the-app-pages"></a>21.6 Creating the App Pages

- With the completed workflow, proceed with building the actual app. First, switch to **Shared Components** and **Static Application Files**.

![](../../assets/Chapter-21/APEX_Workflows_52.jpg)

Add a new file in the **images/** folder with the attached image **reservation_bckgrnd.jpg**.

![](../../assets/Chapter-21/APEX_Workflows_53.jpg)

- The reference created in **Reference** to the file **#APP_FILES#images/reservation_bckgrnd.jpg** will be needed soon. First, switch to page 1 of your application in the **Page Designer** and insert the following code in the **Inline CSS** of the page, where the part after **APP_FILES** is the reference to the file:

```css
body {
    background: url(#APP_FILES#images/reservation_bckgrnd.jpg) no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
}
```
![](../../assets/Chapter-21/APEX_Workflows_54.jpg)

- Add a new region named **Book a table** to the Body of the page. Set the **Column Span** to **5**.

![](../../assets/Chapter-21/APEX_Workflows_55.jpg)

- Create the following **Page Items** in the new region:

  | Name | Type | Label |
  | --- | --- | --- |  
  | **P1_GUEST_NAME** | Text Field | Guest Name |
  | **P1_GUEST_LAST_NAME** | Text Field | Guest Last Name|
  | **P1_GUEST_EMAIL** | Text Field | Guest Email |
  | **P1_GUEST_COUNT** | Select List | Guest Count |
  | **P1_START_DATE** | Date Picker | Start Date & Time |
  | **P1_END_DATE** | Date Picker | End Date & Time |
  | | | |

![](../../assets/Chapter-21/APEX_Workflows_56.jpg)

- Set the value **Value Required** for the page items **P1_GUEST_NAME, P1_GUEST_LAST_NAME, P1_GUEST_EMAIL, P1_START_DATE, and P1_END_DATE**.

![](../../assets/Chapter-21/APEX_Workflows_56b.jpg)

- Populate the new select list **P1_GUEST_COUNT** with **Static Values** from 1 to 8. Disable **Display Extra Values** and **Display Null Value**. Set **Warn on Unsaved Changes** to **Ignore**.

![](../../assets/Chapter-21/APEX_Workflows_57.jpg)

![](../../assets/Chapter-21/APEX_Workflows_57b.jpg)

- Add a **Button** to the region named **Request_reservation** and labeled **Request Reservation**. Enable **Hot** and use **Template Options** to set the **Style** to **Simple**. The **Behavior** is **Submit Page**.

![](../../assets/Chapter-21/APEX_Workflows_58.jpg)

- For the purpose of the demo, add another configuration option for the employee to decide on the reservation. Add a new page item **P1_APPROVER** to the page. Set the **Column Span** to **5** as well. Under **List of Value**, use the following **SQL Query**:

```sql
select rst_name as d, rst_id as r from tutowf_staff_vw
```
![](../../assets/Chapter-21/APEX_Workflows_59.jpg)

- Disable **Display Extra Values** and **Display Null Value**, and set the **Default** to **Static** with the value **1**.

![](../../assets/Chapter-21/APEX_Workflows_59a.jpg)

- Name the next page item **P1_TODAY** and set the type to **Hidden**.

![](../../assets/Chapter-21/APEX_Workflows_60.jpg)

- Create a computation for the page item. Use the following **SQL Query (return single value)**:

```sql
select to_char(systimestamp, 'DD.MM.YYYY HH24:MI') from dual
```

![](../../assets/Chapter-21/APEX_Workflows_61.jpg)

- Enable **Show Time** for the page item **P1_START_DATE**. Choose **Item** for **Minimum Date** and set the **Minimum Item** to **P1_TODAY**. Enter **DD.MM.YYYY HH24:MI** in **Format Mask**.

![](../../assets/Chapter-21/APEX_Workflows_62.jpg)

- Enable **Show Time** for the page item **P1_END_DATE** as well. Here, choose **P1_START_DATE** for **Minimum Item**. Also enter **DD.MM.YYYY HH24:MI** in **Format Mask**.

![](../../assets/Chapter-21/APEX_Workflows_63.jpg)

- Switch to the Processing tab on the page and create a new process named **Submit Reservation Workflow**, with **Type** set to **Workflow**, and the **Definition** is our workflow **Dinner Reservation**. The **Details Primary Key Item** is **P1_APPROVER** - this assigns the task to the employee selected in the page item. Enter a **Success Message**: **Reservation request successfully submitted!**. The Error Message is **Something went wrong**. The **Server-side Condition** is **When Button Pressed** and the Button is **Request_reservation**.

![](../../assets/Chapter-21/APEX_Workflows_64.jpg)

- Set the **Parameters** as follows, with **Type** as **Item** for each:

  | Parameter | Item |
  | -- | -- |  
  | **Guest Count** | *P1_GUEST_COUNT* |   
  | **Guest Email** | *P1_GUEST_EMAIL* |
  | **Guest Last Name** | *P1_GUEST_LAST_NAME* |
  | **Guest Name**| *P1_GUEST_NAME* |
  | **Request Start Date** | *P1_END_DATE* |
  | **Request End Date** | *P1_START_DATE* |
  | | |
 
 ![](../../assets/Chapter-21/APEX_Workflows_65.jpg)

 - Create a new **Branch** under **After Processing** named **Go to Page 1**. The **Behavior** is **Type Page or URL (Redirect)**.
 
  ![](../../assets/Chapter-21/APEX_Workflows_66.jpg)
 
 - Set the target to Page 1. The cache of page 1 should be cleared. Then save the page.

![](../../assets/Chapter-21/APEX_Workflows_67.jpg)

- Switch to the App Builder and create a new page in your application as Page 2, a **Calendar page**.

![](../../assets/Chapter-21/APEX_Workflows_68.jpg)

- The title of the page will be **Reservations**, and the view used is **TUTOWF_RESERVATION_VW**. Use **Navigation** and set the **Parent Navigation Menu Entry** to **Home**.

![](../../assets/Chapter-21/APEX_Workflows_69.jpg)

- Select the following settings:

  | | |  
  |--|--|
  | **Display Column** | *RES_GUEST_LAST_NAME*|
  | **Start Date Column** | *RES_START_DATE* | 
  | **End Date Column** | *RES_END_DATE*|  
  | **Show Time** | *Yes*|
  | | |

![](../../assets/Chapter-21/APEX_Workflows_70.jpg)

- On the new page 2, select the **Region** **Reservations**. Under **Attributes**, set the **Primary Key Column** to **ID**. Under **Supplemental Information**, enter the following text:

```
Table &RES_DINING_TABLE_ID.: &RES_GUEST_NAME. &RES_GUEST_LAST_NAME. with &RES_GUEST_COUNT. guests.
```
![](../../assets/Chapter-21/APEX_Workflows_71.jpg)

## <a name="workflow-creating-a-unified-task-list"></a>21.7 Creating a Unified Task List

- Now create another new page, a **Unified Task List**. Through this task list, restaurant staff can view incoming reservation requests and decide.

![](../../assets/Chapter-21/APEX_Workflows_72.jpg)

- Name the page **Incoming Reservations**, set the **Report Context** to **My Tasks**. In navigation, choose **Create a new entry** under the Parent Entry **Home**.

![](../../assets/Chapter-21/APEX_Workflows_73.jpg)

## <a name="creating-the-workflow-console"></a>21.8 Creating the Workflow Console

- Create another page in the **App Builder** - you will need the **Workflow Console** to get an overview of the initiated workflows.

![](../../assets/Chapter-21/APEX_Workflows_74.jpg)

- Name the new page **20** and **Workflows**. The **Report Context** is **Initiated by me**. A detail page is created directly with the console. Name this **Form Page** as **21** and **Reservation Workflow Details**. In navigation, you can again choose **Home** as a new **Parent Navigation Menu Entry**.

![](../../assets/Chapter-21/APEX_Workflows_75.jpg)

## <a name="workflow-customizing-application-logo"></a>21.9 Customizing the Application Logo

- To further refine the app, set a new icon under **Shared Components**, **Application Definition**, and **User Interface**.

![](../../assets/Chapter-21/APEX_Workflows_76.jpg)

- Choose the icon that resembles a calendar and save the change.

![](../../assets/Chapter-21/APEX_Workflows_77.jpg)

- Start the app and in the **Theme Roller** under **Customize** set the theme to **Vita - Dark**.

![](../../assets/Chapter-21/APEX_Workflows_78.jpg)

- Save the settings.

![](../../assets/Chapter-21/APEX_Workflows_79.jpg)

- With this step, the application is complete! The next section takes you on a brief exploration tour through the reservation demo.

## <a name="workflow-tour-through-the-new-app"></a>21.10 Tour Through the New App

- Start the tour by logging in with your account. Visit the reservation form and make an entry similar to the following (preferably using your own email address). Submit the complete entry.

![](../../assets/Chapter-21/APEX_Workflows_80.jpg)

- Then log out and log back in as the user **COOK**.

![](../../assets/Chapter-21/APEX_Workflows_81.jpg)

- On the **Incoming Reservations** page, you should now see the test reservation you just made.

![](../../assets/Chapter-21/APEX_Workflows_82.jpg)

- Clicking on the title will lead to the reservation details.

![](../../assets/Chapter-21/APEX_Workflows_83.jpg)

- Approve the reservation either from the detail or overview page. Then switch to the **Reservations** page. The test reservation should now be visible in the calendar.

![](../../assets/Chapter-21/APEX_Workflows_84.jpg)

- Log out the user and log back in with your own username. On the **Workflows** page, you get an overview of the created workflows. It should now contain the completed workflow from the test reservation.

![](../../assets/Chapter-21/APEX_Workflows_85.jpg)

- Clicking on the title of the workflow opens the **Reservation Workflow Details** page. Here you see the workflow process and can view the contents of variables and parameters.

![](../../assets/Chapter-21/APEX_Workflows_86.jpg)

- Meanwhile, the email confirming the reservation might have reached you. It should look something like this.

![](../../assets/Chapter-21/APEX_Workflows_87.jpg)

- With this, you have successfully completed the introduction to APEX Workflow. We hope this chapter has given you a glimpse into the possibilities of APEX Workflow!