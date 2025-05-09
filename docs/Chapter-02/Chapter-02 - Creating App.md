# <a name="create"></a>2. Create App Wizard

The Create App Wizard is an assistant that enables developers to quickly design and develop standard APEX applications. The assistant can be used to create complete applications consisting of multiple pages and a variety of different reports and forms.

In this chapter, the framework of the application and the first page will be created. In the Create App Wizard, you specify the settings for your application. After clicking on Create Application, APEX creates the application with your settings.

## <a name="erstelleneineranwendung"></a>2.1 Creating an Application

- For the subsequent tasks, an **application** must first be created. To do this, first open the **App Builder**. The App Builder displays all installed applications. Now click on the **Create** button.

![](../../assets/Kapitel-02/Open_Create_App_Wizard.jpg)

- The application creation assistant is launched. Click on Use Create App Wizard to open the wizard for a new application.

![](../../assets/Kapitel-02/Create_App_Wizard_1.jpg)

- Now enter the name of the application (e.g. Apex Tutorial).

![](../../assets/Kapitel-02/Create_App_Wizard_2.jpg)

- If desired, you can also adjust the Application Icon by clicking on the blue envelope to the left of the name. A wizard opens in which an icon and a color can be selected or your own image can be uploaded.

- In the wizard, you can directly create a first page in your application. Click on the plus or on Add Page to do so.

![](../../assets/Kapitel-02/Create_App_Wizard_3.jpg)

## <a name="report"></a>2.2 Report

In APEX, a report is a formatted representation of a SQL query. A report can be generated via the assistant or through a manually entered SQL query.

APEX distinguishes between classic reports and interactive reports. The difference between the two is that the user has the ability to customize the data display in an interactive report through searching, filtering, sorting, column selection, highlighting, and other data manipulations.

- After clicking the button to add a page, a new window with a wizard for creating the page opens. There, select **Interactive Report**.

![](../../assets/Kapitel-02/Interactive_Report_1.jpg)

- The properties of the page follow in the next window. Enter ***STATES*** as the **Page Name**.
- The settings **Table or View** and **Interactive Report** are selected by default. If this is not the case, please select them.
- Next, click on the dropdown menu on the right to select a **table** to be displayed in the Interactive Report.

![](../../assets/Kapitel-02/Interactive_Report_2.jpg)

- The **Search Dialog** opens where you select the table ***STATES***.
- Check the box for **Include Form** and then click the **Add Page** button.

![](../../assets/Kapitel-02/Interactive_Report_3.jpg)

## <a name="createapplication"></a>2.3 Create Application

- Your Create App Wizard should now look like this.

![](../../assets/Kapitel-02/Create_App_Wizard_4.jpg)

- Now check the box for the feature **"Install Progressive Web App"**. This feature allows APEX applications to be installed on mobile devices and used as standalone applications. You can find out more in <span style="color:red">**Task #07: Features for Mobile Devices**</span>.

![](../../assets/Kapitel-02/Create_App_Wizard_Features.jpg)

- Scrolling down, you will see the **Application ID** under **Settings**. Since you will need this later on, it is advisable to note it down.
The Application ID is a unique number through which the application can be accessed in the browser.

- After completing all other steps, click the **Create Application** button to create the application.

![](../../assets/Kapitel-02/Create_App_Wizard_Settings.jpg)

## <a name="runpage"></a> 2.4 Run Page

After you have created the application, the page overview of your application opens.
You will see five pages: **0 - Global Page - Desktop**, **1 - Home**, and **9999 - Login Page** are default pages created for every application. The Global Page is a master page. All components added to the Global Page are displayed on all pages of the application.
You have just created the pages **2 - STATES** and **3 - State** using the Add Page wizard.
- Click on the highlighted button to open the **list view**.

![](../../assets/Kapitel-02/App_Builder_Page_Overview.jpg)

- Click on the **Run Button** of the ***STATES*** page to view the created page.

![](../../assets/Kapitel-02/App_Builder_Page_Overview_List.jpg)

- A login screen appears where you log in with your username and password (same credentials as for the workspace).

![](../../assets/Kapitel-02/Login_Screen.jpg)

- After logging in, the ***STATES*** page appears with an Interactive Report.

![](../../assets/Kapitel-02/Page_2.jpg)

- Clicking on the **pencil icon** in the left column opens a modal dialog where you can change the data.

![](../../assets/Kapitel-02/Modal_Dialog.jpg)

- For now, leave the contents as they are and close the modal dialog again (via the **Cancel** button or the x at the top corner).

- Now switch back to the **App Builder** tab.

![](../../assets/Kapitel-02/Navigationbar_Browser.jpg)