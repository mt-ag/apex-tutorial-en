# <a name="apex-workflow"></a>21. APEX Workflow

Since APEX 23.2, workflows are directly integrated into APEX. With **APEX Workflow**, business processes can be created and executed using a graphical editor. Users who want to map processes using **Business Process Model and Notation (BPMN 2.0)** will find the related extension **Flows for APEX** by MT - IT Solutions to be a suitable addition. More information is available at the link [https://flowsforapex.org/](https://flowsforapex.org/).

In the following chapter, we use workflows to create a demo version of a simplified restaurant table reservation. The demo is based on the blog post **Simplify Business Process Management Using APEX Workflow** by Ananya Chatterjee. [Link to the blog](https://blogs.oracle.com/apex/post/simplify-business-process-management-using-apex-workflow-create-doctor-appointment-application)

## <a name="starting-point-use-case-and-flow-chart"></a>21.1 Starting Point Use Case and Flow Chart

As a starting point for the task in this chapter, we assume that a restaurant wants to implement a simple booking form on the website. In the form, guests can submit a reservation request for a table. In the next step, the system first checks whether a table is available for the desired number of people at the requested time. If not, an email is immediately sent to the guest with a rejection of the appointment. If a table is available, the request is passed on to a restaurant employee. The employee decides whether to accept the reservation. If rejected, a rejection email is sent, if accepted, the reservation is saved and the guest is informed of the successful reservation by email.

- The following **Flow-Chart** visualizes this use case.

![](../../assets/Chapter-21/APEX_Workflows_01.png)

## <a name="workflow-setup-of-the-required-elements"></a>21.2 Setup of the Required Elements

- The required tables and packages were already installed via the **Script for the Tutorial** in chapter 1.

- For the APP, you need a user named **KOCH**, who will later be responsible for processing reservation requests. Create an appropriate user.

- Click on the **Administration** icon in the top right and select **Manage Users and Groups**.

- Click **Create User** here.

- Enter the following information:
  - Name: KOCH
  - Email Address: test@abc.com
  - Password: 12345678
  - Confirm Password: 12345678
  - Require Change of Password on First Use: No

- Then create a new APP via the **App Builder** and **Create**. Give the app the title **MT Tutorial - Dinner Reservation**.

![](../../assets/Chapter-21/APEX_Workflows_02.jpg)

## <a name="creating-the-workflow"></a>21.3 Creating the Workflow

- The next step involves the actual work task. First, we create a **Workflow**.

- Switch back to the **Application Builder** of the new app and click on **Shared Components**.

![](../../assets/Chapter-21/APEX_Workflows_03.jpg)

- In Shared Components, choose **Workflows** under **Workflows and Automations**.

![](../../assets/Chapter-21/APEX_Workflows_04.jpg)

- Create a new workflow here by clicking on **Create**. You will then be directed to the **Workflow Editor**. A basic workflow is already visible in the center of the **Diagram Builder**.

![](../../assets/Chapter-21/APEX_Workflows_05.jpg)

- Set the name of the workflow to **Dinner Reservation** and the **Static ID** to **DINNERRSVRT**. Set the title: **Workflow for Guest &GUEST_NAME. &GUEST_LAST_NAME.**

![](../../assets/Chapter-21/APEX_Workflows_06.jpg)

- Set the **Workflow Version** to **1.0**.

![](../../assets/Chapter-21/APEX_Workflows_07.jpg)

- Currently, there is still an error because the automatically created activity has not yet been specified. To save, delete the activity. Right-click on **Activity** in the left column and choose **Delete**. Alternatively, select the activity in the editor and click on the icon with the three dots.

![](../../assets/Chapter-21/APEX_Workflows_08.jpg)

- The **start of the activity**, the **arrow**, and the **endpoint** remain. Drag the **arrowhead** in the editor to the **endpoint** and then save.

![](../../assets/Chapter-21/APEX_Workflows_09.jpg)

- In the next step, create a series of **input parameters** that will be provided to the workflow as data. Right-click on the workflow and choose **Create Parameter**.

![](../../assets/Chapter-21/APEX_Workflows_10.jpg)

- Give the first parameter the **Static ID: GUEST_NAME**, the **Label: Guest Name**. The **Data Type** is **VARCHAR2**.

![](../../assets/Chapter-21/APEX_Workflows_11.jpg)

- Set the following additional parameters:

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

- Now, in Workflow 1.0 under **Additional Data**, link the table **T_RESTAURANT_STAFF**. This ensures later that the created tasks can be assigned to corresponding handlers. Additionally, the columns of the table are available as bind variables for the workflow. Choose **Primary Key Column** as the column **RST_ID**.

![](../../assets/Chapter-21/APEX_Workflows_13.jpg)

- Besides the input parameters, you also need variable variables in the workflow that can be used in the process. Create **Workflow Variables** in the next step. Right-click again on the workflow 1.0 and choose **Create Variable**.

![](../../assets/Chapter-21/APEX_Workflows_14.jpg)

- Give the first variable the **Static ID: RESERVATION_ID** and the **Label: Reservation ID**. The **Data Type** is **NUMBER**. The variable will be assigned a value at a later time, so the **Value** is initially **Null**.

![](../../assets/Chapter-21/APEX_Workflows_15.jpg)

- Now, create the variable **TABLE_ID** following the same pattern: **Static ID: TABLE_ID**, **Label: Table ID** and **Data Type** is **NUMBER**. Set **Value** to **Null** here as well.

![](../../assets/Chapter-21/APEX_Workflows_16.jpg)

- The next variable you create is **AVAILABILITY**. It is of type **BOOLEAN**. Under **True Value**, enter **AVAIL** and under **False Value** enter **UNAVAIL**. These are the two possible return values of a function that will be integrated into the workflow later. Then save the workflow using **Save**.

![](../../assets/Chapter-21/APEX_Workflows_17.jpg)

## <a name="creating-the-task-for-the-reservation-request"></a>21.4 Creating the Task for the Reservation Request

- In the next step, you create the task for confirming (or rejecting) the reservation request. Switch to **Shared Components** and then **Task Definitions**. Click on **Create** to create a new task.

![](../../assets/Chapter-21/APEX_Workflows_18.jpg)

- In the dialog to create the **Task Definition**, give the task the name **Reservation Request** and the **Subject: Reservation for Guest &GUEST_NAME. &GUEST_LAST_NAME.**. The **Static ID** is **RESERVATION_REQUEST**. Then click on **Create**.

![](../../assets/Chapter-21/APEX_Workflows_19.jpg)

- In the next step, set the **Action Source** to **SQL Query**. In the query field, enter the following query:

```sql
  select * from t_restaurant_staff where rst_id = :APEX$TASK_PK
  ```

![](../../assets/Chapter-21/APEX_Workflows_20.jpg)

- Create a new row in the **Participants** table. The **Participant Type** is **Potential Owner**, the **Value Type** is **Expression** and the **Value** is **:RST_NAME**. This refers to the corresponding column in the employee table **T_RESTAURANT_STAFF**, which allows tasks to be handled by those employees.

![](../../assets/Chapter-21/APEX_Workflows_21.jpg) 

- Also, parameters are provided for the task. Add the following rows to the parameter table:

  | | | |  
  |--|--|--|
  | **NAME_GUEST** | Name Guest | *String* |
  | **LAST_NAME_GUEST** | Last Name Guest | *String* | 
  | **COUNT_GUEST** | Count Guest | *String*|  
  | **RESERVATION_DATE_START** | Reservation Date Start | *String* |
  | **RESERVATION_DATE_END** | Reservation Date End | *String* |
  | | | |

![](../../assets/Chapter-21/APEX_Workflows_22.jpg)

- Confirm the additions to the task with the **Apply Changes** button. You will be taken back to **Task Definitions**. Go back to the **Reservation Request** task once more and create a new page under **Task Details Page**. Give the page the number **11**.

![](../../assets/Chapter-21/APEX_Workflows_22b.jpg)

## <a name="completion-of-the-workflow"></a>21.5 Completion of the Workflow

- In the next step, the work on the workflow continues. Switch back to **Workflows** in **Shared Components** and click on **Dinner Reservation**.

![](../../assets/Chapter-21/APEX_Workflows_23.jpg)

- Create a new activity in **Workflow 1.0** under **Activities** with a right-click.

![](../../assets/Chapter-21/APEX_Workflows_24.jpg)

- Give the new activity the name **Check Availability** and the type **Invoke API**. Select the package **DINNER_RESERVATION_DEMO** and from it, the function **CHECK_AVAILABILITY**.

![](../../assets/Chapter-21/APEX_Workflows_25.jpg)

- Pass the result of the function to the parameter **Function Result**, specifically in **Item** via the **Version Variable** **Availability**.

![](../../assets/Chapter-21/APEX_Workflows_26.jpg)

![](../../assets/Chapter-21/APEX_Workflows_27.jpg)

- Set the parameters **pi_guest_count**, **pi_start_date**, and **pi_end_date** to type **Item** under **Value** and then to the following **Workflow Parameters** and **Format Masks**:

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

- To handle the result of the query activity, you now need a **Switch**. Create one, for example by dragging it into the Diagram Builder.

![](../../assets/Chapter-21/APEX_Workflows_31.jpg)

- The new **Name** of the switch will be **Decide availability**. Under **Condition**, choose **Condition Type: Workflow Variable = Value** and the **Workflow Variable: AVAILABILITY** and the value **AVAIL**, which the function outputs when a table is available for the desired number of people at the requested date.

![](../../assets/Chapter-21/APEX_Workflows_32.jpg)

- Connect the two activities **Check availability** and **Decide availability** with each other. You can draw a new arrow and connect it with the target activity using the plus sign.

![](../../assets/Chapter-21/APEX_Workflows_33.jpg)

- We continue with the first possible outcome of the check: the scenario when the check reveals that **no table** is available. In this case, an email is sent informing the requester that no table is available. Create a **Send E-Mail Activity** for this purpose.

![](../../assets/Chapter-21/APEX_Workflows_34.jpg)

- The name of this activity is **Send Mail unavailable**. In the **To** field, enter **&GUEST_EMAIL.** with the parameter containing the guest's email. In the **Subject** field, enter the email subject. Set it to **Your reservation: No table available**. Enter the following mail text in the **Body Plain Text** field:

```
Dear &GUEST_NAME. &GUEST_LAST_NAME.,

unfortunately, there is no table available at the requested time. Please try another time!

With kind regards
The Restaurant Team
```
![](../../assets/Chapter-21/APEX_Workflows_35.jpg)

- Connect the switch with the email activity using an arrow.

![](../../assets/Chapter-21/APEX_Workflows_36.jpg)

- Select the arrow and name the connection **Unavailable**. The **Condition** in this case is **FALSE**, as the email should be sent when the check reveals that no table is available.

![](../../assets/Chapter-21/APEX_Workflows_37.jpg)

- Create another **Workflow End** and connect it with the mail send activity. Then you can save the workflow in between.

![](../../assets/Chapter-21/APEX_Workflows_38.jpg)

- Now let's proceed with the scenario where the initial check shows that a table is available. In this case, a member of staff should decide whether to accept the reservation. First, you create a **Human Task - Create** activity. Give the activity the name **Create Reservation Request**, and in **Definition** choose the task **Reservation Request** you just created. Set **Details Primary Key Item** to **RST_ID**. For **Outcome**, select the automatically created **Variable** **TASK_OUTCOME** and in **Owner** the automatically created **Variable** **APPROVER**.

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

- Connect the switch **Decide availability** with the activity **Create Reservation Request** by adding a new arrow. The connection is named **Available** and the **Condition** when **True**.

![](../../assets/Chapter-21/APEX_Workflows_41.jpg)

- To process the decision from the task, we need a **Switch** again. Create a new switch and name it **Decide Reservation approved**. The **Switch-Type** is **Check Workflow Variable**. The variable compared in **Compare Variable** is set to **TASK_OUTCOME**.

![](../../assets/Chapter-21/APEX_Workflows_42.jpg)

- Connect **Create Reservation Request** with **Decide Reservation approved** using an arrow.

![](../../assets/Chapter-21/APEX_Workflows_43.jpg)

- Since a rejection email should also be sent in case of a reservation denial by the staff, connect **Decide Reservation approved** with **Send Mail unavailable**. Set the name to **Rejected**. The **Operator** is **Is Equal to** and the **Value** is the result **REJECTED** from the human task. Save in between.

![](../../assets/Chapter-21/APEX_Workflows_44.jpg)

- In case of approval, the next activity now determines a free table number assigned to the reservation. Add an **Invoke API** activity. Give it the name **Get free table**. The associated package is **DINNER_RESERVATION_DEMO**, and the **Function** is **GET_FREE_TABLE_ID**.

![](../../assets/Chapter-21/APEX_Workflows_45.jpg)

- The **Function Result** of the activity is transferred to the **Item** variable **TABLE_ID**.

![](../../assets/Chapter-21/APEX_Workflows_46.jpg)

- Set the remaining parameters as follows (analogous to **Check availability**).

  | Parameter | Item | Format Mask |
  | --- | --- | --- |  
  | **pi_guest_count** | GUEST_COUNT | |
  | **pi_start_date** | REQUEST_START_DATE | DD.MM.YYYY HH24:MI |
  | **pi_end_date** | REQUEST_END_DATE | DD.MM.YYYY HH24:MI |
  | | | |

- Connect the switch **Decide Reservation approved** with the **Get free table** activity. Name the connection **Approved**, set the operator to **Is Equal to**, and the value to **APPROVED**.

![](../../assets/Chapter-21/APEX_Workflows_47.jpg)

- Now all the information is available to store the approved reservation. Add another **Invoke API** activity. Name it **Set reservation**. The associated package is **DINNER_RESERVATION_DEMO**, and the **Function** is **SET_RESERVATION**.

![](../../assets/Chapter-21/APEX_Workflows_48.jpg)

- Set the function result under **Function Result** in **Parameters** to the variable **RESERVATION_ID**. Fill in the rest of the parameters as follows:

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

- The **pi_workflow_id** expects the current workflow's Workflow ID. You can also transfer the Workflow ID to the procedure as a **Static Value**. Enter **&APEX$WORKFLOW_ID.** here. Connect **Get free table** and **Set reservation**.

![](../../assets/Chapter-21/APEX_Workflows_49.jpg)

- After saving, the customer is to be informed by email that the reservation has been approved. Add the corresponding **Send E-Mail** activity next, and name it **Send confirmation**. Enter the customer's email in the **To** field - similar to the rejection mail - **&GUEST_EMAIL.** The subject is **Reservation Confirmation**. Use the following **Body Plain Text**:

```
Dear &GUEST_NAME. &GUEST_LAST_NAME.,

hereby we confirm your reservation! We are looking forward to your stay on the following date: &REQUEST_START_DATE.!

With kind regards
The Restaurant Team
```

![](../../assets/Chapter-21/APEX_Workflows_50.jpg)

- Now, connect the activities with each other and integrate the free **Workflow End** as the endpoint of the workflow. Save the workflow afterward.

![](../../assets/Chapter-21/APEX_Workflows_51.jpg)

## <a name="creating-the-app-pages"></a>21.6 Creating the App Pages

- With the created workflow, we now continue building the actual app. First, switch to **Shared Components** and **Static Application Files**.

![](../../assets/Chapter-21/APEX_Workflows_52.jpg)

Add a new file in the folder **images/** with the attached image **reservation_bckgrnd.jpg**.

![](../../assets/Chapter-21/APEX_Workflows_53.jpg)

- The reference in **Reference** to the file **#APP_FILES#images/reservation_bckgrnd.jpg** will be needed shortly. First, switch to page 1 of your application in **Page Designer** and enter the following code in the **Inline CSS** of the page, the part after **APP_FILES** is the reference to the file:

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

- Add a new region in the body with the name **Book a table**. Set the **Column Span** to **5**.

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

- Set the **Value Required** for the Page Items **P1_GUEST_NAME, P1_GUEST_LAST_NAME, P1_GUEST_EMAIL, P1_START_DATE and P1_END_DATE** to on.

![](../../assets/Chapter-21/APEX_Workflows_56b.jpg)

- Populate the new Select-List **P1_GUEST_COUNT** with **Static Values** from 1 to 8. Disable **Display Extra Values** and **Display Null Value**. Set **Warn on Unsaved Changes** to **Ignore**.

![](../../assets/Chapter-21/APEX_Workflows_57.jpg)

![](../../assets/Chapter-21/APEX_Workflows_57b.jpg)

- Add a **Button** to the region with the name **Request_reservation** and the label **Request Reservation**. Enable **Hot** and under **Template Options** set the **Style** to **Simple**. The **Behavior** is **Submit Page**.

![](../../assets/Chapter-21/APEX_Workflows_58.jpg)

- Introduce an additional setting option for the employee in charge of making the reservation decision for demonstration purposes. Add another Page Item **P1_APPROVER** to the page. Also, set the **Column Span** to **5**. Under **List of Value**, set the following **SQL-Query**:

```sql
select rst_name as d, rst_id as r from tutowf_staff_vw
```
![](../../assets/Chapter-21/APEX_Workflows_59.jpg)

- Disable **Display Extra Values** and **Display Null Value** and set the **Default** to **Static** with the value **1**.

![](../../assets/Chapter-21/APEX_Workflows_59a.jpg)

- Name the next Page Item **P1_TODAY** and set the Type to **Hidden**.

![](../../assets/Chapter-21/APEX_Workflows_60.jpg)

- Create a Computation for the Page Item. Use the following **SQL Query (return single value)**:

```sql
select to_char(systimestamp, 'DD.MM.YYYY HH24:MI') from dual
```

![](../../assets/Chapter-21/APEX_Workflows_61.jpg)

- Enable **Show Time** for the Page Item **P1_START_DATE**. For **Minimum Date**, choose **Item** and set the **Minimum Item** to **P1_TODAY**. Enter **Format Mask** as **DD.MM.YYYY HH24:MI**.

![](../../assets/Chapter-21/APEX_Workflows_62.jpg)

- Also, enable **Show Time** for the Page Item **P1_END_DATE**. Here, the **Minimum Item** becomes **P1_START_DATE**. Similarly, enter **Format Mask** as **DD.MM.YYYY HH24:MI**.

![](../../assets/Chapter-21/APEX_Workflows_63.jpg)

- On the page, switch to the Processing tab and create a new Process called **Submit Reservation Workflow**, with the **Type** set to **Workflow**, and the **Definition** to our **Dinner Reservation** workflow. The **Details Primary Key Item** is **P1_APPROVER** - this assigns the task to the employee selected in the Page Item. Enter the following **Success Message**: **Reservation request successfully submitted!**. The Error Message is **Something went wrong**. The **Server-side Condition** is **When Button Pressed** with the button being **Request_reservation**.

![](../../assets/Chapter-21/APEX_Workflows_64.jpg)

- Set the **Parameters** as follows, **Type** is **Item** for each:

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

 - Under **After Processing**, create a new **Branch** named **Go to Page 1**. The **Behavior** is **Type Page or URL (Redirect)**.
 
  ![](../../assets/Chapter-21/APEX_Workflows_66.jpg)
 
 - Set the Target to Page 1. The cache of page 1 should be cleared. Then save the page.

![](../../assets/Chapter-21/APEX_Workflows_67.jpg)

- Now switch to the App Builder and create a new page in your application. Create a **Calendar Page** as Page 2 of the Application.

![](../../assets/Chapter-21/APEX_Workflows_68.jpg)

- The title of the page will be **Reservations**, and the view used is **TUTOWF_RESERVATION_VW**. Use the **Navigation** and set **Parent Navigation Menu Entry** to **Home**.

![](../../assets/Chapter-21/APEX_Workflows_69.jpg)

- Then select the following settings:

  | | |  
  |--|--|
  | **Display Column** | *RES_GUEST_LAST_NAME*|
  | **Start Date Column** | *RES_START_DATE* | 
  | **End Date Column** | *RES_END_DATE*|  
  | **Show Time** | *Yes*|
  | | |

![](../../assets/Chapter-21/APEX_Workflows_70.jpg)

- On the new Page 2, select the **Region** **Reservations**. Under **Attributes**, set the **Primary Key Column** to **ID**. Under **Supplemental Information**, enter the following text:

```
Table &RES_DINING_TABLE_ID.: &RES_GUEST_NAME. &RES_GUEST_LAST_NAME. with &RES_GUEST_COUNT. guests.
```
![](../../assets/Chapter-21/APEX_Workflows_71.jpg)

## <a name="workflow-creating-a-unified-task-list"></a>21.7 Creating a Unified Task List

- Now create another new page, a **Unified Task List**. The restaurant staff can view and decide on incoming reservation requests via this task list.

![](../../assets/Chapter-21/APEX_Workflows_72.jpg)

- Give the page the name **Incoming Reservations**, the **Report Context** should be **My Tasks**. For Navigation, choose **Create a new entry** under the Parent Entry **Home**.

![](../../assets/Chapter-21/APEX_Workflows_73.jpg)

## <a name="creating-the-workflow-console"></a>21.8 Creating the Workflow Console

- In the **App Builder**, create another page - you also need a **Workflow Console** where you can get an overview of the status of the initiated workflows.

![](../../assets/Chapter-21/APEX_Workflows_74.jpg)

- Assign the new page **number 20** and the name **Workflows**. The **Report Context** should be **Initiated by me**. A detail page is directly created for the console. Assign this **Form Page** **number 21** and the name **Reservation Workflow Details**. In the navigation, you can again select **Home** as a new **Parent Navigation Menu Entry**.

![](../../assets/Chapter-21/APEX_Workflows_75.jpg)

## <a name="workflow-customizing-the-application-logo"></a>21.9 Customizing the Application Logo

- To refine the app, set a new icon under **Shared Components**, in **Application Definition**, under the **User Interface** section.

![](../../assets/Chapter-21/APEX_Workflows_76.jpg)

- Choose the icon resembling a calendar and save the change.

![](../../assets/Chapter-21/APEX_Workflows_77.jpg)

- Launch the app and set the theme to **Vita - Dark** in the **Theme Roller**.

![](../../assets/Chapter-21/APEX_Workflows_78.jpg)

- Save the settings.

![](../../assets/Chapter-21/APEX_Workflows_79.jpg)

- With this step, the application is complete! In the next section, we'll take a brief tour of the reservations demo.

## <a name="workflow-tour-of-the-new-app"></a>21.10 Tour of the New App

- Start the tour by logging in with your account. Visit the reservation form and enter something similar to the following (ideally use your email address). Submit the complete entry.

![](../../assets/Chapter-21/APEX_Workflows_80.jpg)

- Log out and then sign in as user **KOCH**.

![](../../assets/Chapter-21/APEX_Workflows_81.jpg)

- On the **Incoming Reservations** page, you should now see the newly created test reservation.

![](../../assets/Chapter-21/APEX_Workflows_82.jpg)

- Click on the title to view reservation details.

![](../../assets/Chapter-21/APEX_Workflows_83.jpg)

- Approve the reservation either on the detail page or overview page. Then switch to the **Reservations** page. The test reservation should now be visible in the calendar.

![](../../assets/Chapter-21/APEX_Workflows_84.jpg)

- Log out the user again and log in with your username. On the **Workflows** page, you get an overview of the created workflows. It should now contain the completed workflow from the test reservation.

![](../../assets/Chapter-21/APEX_Workflows_85.jpg)

- Click on the workflow title to access the details page **Reservation Workflow Details**. Here you see the flow of the workflow and can view the contents of the variables and parameters.

![](../../assets/Chapter-21/APEX_Workflows_86.jpg)

- In the meantime, you should have received the email confirming the reservation. It should look something like this.

![](../../assets/Chapter-21/APEX_Workflows_87.jpg)

- With this, you have successfully completed the introduction to APEX Workflow. We hope this chapter provided you with a brief insight into the possibilities of APEX Workflow!