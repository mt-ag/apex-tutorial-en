# <a name="create"></a>2. Create App Wizard

The Create App Wizard is an assistant that allows developers to quickly design and develop standard APEX applications. It can be used to create complete applications consisting of multiple pages and a variety of different reports and forms.

In this chapter, the basic structure of the application and the first page are created. In the Create App Wizard, you specify the settings for your application. After clicking on Create Application, APEX creates the application with your settings.

## <a name="erstelleneineranwendung"></a>2.1 Creating an Application

- For the following tasks, an **application** must first be created. To do this, first open the **App Builder**. The App Builder displays all installed applications. Now click on the **Create** button.

![](../../assets/Chapter-02/Open_Create_App_Wizard.jpg)

- The application creation wizard is launched. Click on Use Create App Wizard to open the wizard for a new application.

![](../../assets/Chapter-02/Create_App_Wizard_1.jpg)

- Now enter the name of the application (e.g., Apex Tutorial).

![](../../assets/Chapter-02/Create_App_Wizard_2.jpg)

- If desired, the Application Icon can be customized by clicking on the blue envelope to the left of the name. A wizard opens where an icon and a color can be selected or an own image can be uploaded.

- In the wizard, you can directly create a first page in your application. To do this, click on the plus or on Add Page.

![](../../assets/Chapter-02/Create_App_Wizard_3.jpg)

## <a name="report"></a>2.2 Report

In APEX, a report is a formatted presentation of a SQL query. A report can be generated via the wizard or through a manually entered SQL query.

APEX distinguishes between the classic and the interactive report. The difference between the two is that in an interactive report, the user has the ability to adjust the data presentation by searching, filtering, sorting, column selection, highlighting, and other data manipulations.

- After clicking on the button to add a page, a new window opens with a wizard for creating the page. There, select **Interactive Report**.

![](../../assets/Chapter-02/Interactive_Report_1.jpg)

- The properties of the page follow in the next window. Enter ***STATES*** as the **Page Name**.
- The settings **Table or View** and **Interactive Report** are selected by default. If this is not the case, please select them.
- Next, click on the dropdown menu on the right to select a **table** to be displayed in the Interactive Report.

![](../../assets/Chapter-02/Interactive_Report_2.jpg)

- The **Search Dialog** opens, where you select the table ***STATES***.
- Check the box for **Include Form** and then click on the **Add Page** button.

![](../../assets/Chapter-02/Interactive_Report_3.jpg)
 
## <a name="createapplication"></a>2.3 Create Application

- This is how your Create App Wizard should look now.

![](../../assets/Chapter-02/Create_App_Wizard_4.jpg)

- Now check the box for the feature **"Install Progressive Web App"**. With this feature, APEX applications can be installed on mobile devices and used as standalone applications. You can learn more about this in <span style="color:red">**Task #07: Features for Mobile Devices**</span>.

![](../../assets/Chapter-02/Create_App_Wizard_Features.jpg)

- Scrolling down, you will see the **Application ID** under **Settings**. Since you will need this later, it is advisable to note it down.  
The Application ID is a unique number through which the application can be accessed in the browser.

- After completing all other steps, click the **Create Application** button to create the application.

![](../../assets/Chapter-02/Create_App_Wizard_Settings.jpg)
 
## <a name="runpage"></a> 2.4 Run Page

After creating the application, the page overview of your application opens. 
You see five pages: **0 - Global Page - Desktop**, **1 - Home**, and **9999 - Login Page** are standard pages created with every application. The Global Page is a master page. All components placed on the Global Page are displayed on all pages of the application. 
The pages **2 - STATES** and **3 - State** you just created using the Add Page wizard.
- Click on the marked button to open the **List View**.

![](../../assets/Chapter-02/App_Builder_Page_Overview.jpg)

- Click on the **Run-Button** of the ***STATES*** page to view the created page.

![](../../assets/Chapter-02/App_Builder_Page_Overview_List.jpg)

- A login screen appears, where you log in with your username and password (same credentials as for the Workspace).

![](../../assets/Chapter-02/Login_Screen.jpg)

- After logging in, the page ***STATES*** appears with an Interactive Report.

![](../../assets/Chapter-02/Page_2.jpg)

- Clicking on the **pencil icon** in the left column opens a modal dialog where you can change the data.

![](../../assets/Chapter-02/Modal_Dialog.jpg)

- For now, we leave the contents as they are and close the modal dialog again (via the **Cancel** button or the x at the top corner).  

- Now switch back to the **App Builder** tab.

![](../../assets/Chapter-02/Navigationbar_Browser.jpg)