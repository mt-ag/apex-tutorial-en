# 12. Plug-Ins

## 12.1. Introduction

Plug-ins are extensions that allow APEX to be expanded with custom item types, region types, processes, and dynamic actions. Components based on plug-ins are created and maintained similarly to standard APEX components. With plug-ins, developers can create customized components to enhance the functionality, appearance, and user-friendliness of their applications.

Plug-ins can help make the application more user-friendly and add extras. As part of this task, two plug-ins will be integrated. Below you will integrate plug-ins into your application.

> You can find more plug-ins besides the ones mentioned here on apex.world:  
[https://apex.world/ords/f?p=100:700](https://apex.world/ords/f?p=100:700)

## 12.2. Plug-Ins

To complete these tasks, we will use a plug-in from the following page:

[https://api.github.com/repos/Dani3lSun/apex-plugin-apextooltip/zipball](https://api.github.com/repos/Dani3lSun/apex-plugin-apextooltip/zipball)

This plugin allows developers to incorporate tooltips into buttons, fields, regions, reports, and other components. The plug-in must first be downloaded and unpacked.

### 12.2.1. Import Plug-In

- First open the **App Builder** and your **Application**. Then click on **Shared Components**.

- Under **Other Components**, click on **Plug-Ins**.

![](../../assets/Chapter-12/Plugins_01.jpg)

- Click on **Import**.

![](../../assets/Chapter-12/Plugins_02.jpg)

- Upload the plug-in. It should be in the folder where you unpacked the plug-in:   
**…source\dynamic_action_plugin_de_danielh_apextooltip.sql**.

  Drag and drop this file into the appropriate field. Select **Plug-in** as **File Type** and then click **Next**.

![](../../assets/Chapter-12/Plugins_03.jpg)

- Click **Next** again.

![](../../assets/Chapter-12/Plugins_04.jpg)

- Choose the application with which you are conducting this tutorial and click on **Install Plug-In**.

![](../../assets/Chapter-12/Plugins_05.jpg)

### 12.2.2. Integrate Plugin

- The plug-in is now installed. Click on your application to return.

![](../../assets/Chapter-12/Plugins_06.jpg)

- Select page 2 - **STATES**.

- Click on **Dynamic Actions** (lightning icon) and right-click under **Page Load** on **Create Dynamic Action**.

![](../../assets/Chapter-12/Plugins_07.jpg)

Dynamic Actions allow developers to define client-side behavior without JavaScript. With the creation wizard, you can specify when certain actions should be carried out and which elements are affected by these actions.  
- Change the name of the Dynamic Action to **Tooltip** and then click **Show**.

- Now change the following fields:  
  | | |  
  |--|--|
  | **Identification** |
  | Action | APEX Tooltip [Plug-In]|  
  | **Settings** | 
  | Theme | *Light* |
  | Content Text | *Create State* |
  | **Affected Elements** |
  | Selection Type | *Button* | 
  | Button  |  *CREATE* |
  | | |

![](../../assets/Chapter-12/Plugins_08.jpg)

- Now start the application using the **Run** button.  
- When you now hover the mouse over the Create Button, the tooltip will be displayed.

![](../../assets/Chapter-12/Plugins_09.jpg)

There are many other settings or **Plug-In Settings** that you can use as described above. Feel free to try some of them.

### 12.2.3. Quality Assurance Plugin

- Follow the same steps as in 12.2.1 to install another plug-in.  
The plug-in allows development guidelines to be defined and subsequently displays violations against these on the respective page automatically.

> You can download the plug-in here: 
[https://github.com/mt-ag/apex-qa-plugin/archive/master.zip](https://github.com/mt-ag/apex-qa-plugin/archive/master.zip)

- Import the plugin. It should then be in the folder where you unpacked the plug-in: 
**…src\APEX\region_type_plugin_com_mtag_olemm_qa_region.sql**

- Additionally, database objects must be created for the plug-in using an SQL script. To do this, click on **SQL Workshop** and then on **SQL Scripts**. Click on the **Upload** button there.

![](../../assets/Chapter-12/Plugins_10.jpg)

- Upload the file **…\src\plugin_qa_install.sql** from the plugin folder.

![](../../assets/Chapter-12/Plugins_11.jpg)

- The script can now be executed with the **Run** button and then **Run Now**.

![](../../assets/Chapter-12/Plugins_12.jpg)

![](../../assets/Chapter-12/Plugins_13.jpg)

- You can now navigate back to the application via the **App Builder** and call up **Page 0** (Global Page – Desktop).

- By right-clicking on the **Components** tab, create a new region with **Create Region**.

![](../../assets/Chapter-12/Plugins_14.jpg)

- Now change the following fields and then press Save:
  | | |  
  |--|--|
  | **Identification** |
  | Title | **QA** |
  | Type | **Quality Assurance – Region [Plug-In]**|  
  | | |

![](../../assets/Chapter-12/Plugins_15.jpg)

Since this region was created on the **Global Page – 0**, this region will now be displayed on each page of the application.

In order for the plug-in to display violations against the guidelines, these must be defined. Some sample rules are already included when downloading the **plug-in**. 
- As before, an **SQL script** must now be uploaded and executed via the **SQL Workshop**. You can find the script under: **…src\DML\plugin_qa_rules.sql**

- When you now switch to the application and call up a page, the rule violations will be displayed at the end of the page in the QA region.

![](../../assets/Chapter-12/Plugins_16.jpg)

For your own projects, you can define your individual rules for this plug-in to ensure compliance with the guidelines.