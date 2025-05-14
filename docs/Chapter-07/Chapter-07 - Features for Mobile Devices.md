# 7. Features for Mobile Devices
## 7.1. Reflow Report & Column Toggle Report
Two types of reports that help make APEX applications comfortable to use on mobile devices are the **Reflow Report** and the **Column Toggle** Report.

The Reflow Report displays table columns vertically when there is not enough space to display them horizontally. The **Column Toggle** Report allows columns to be assigned different priorities. Columns with lower priority are displayed narrower and hidden earlier than columns with higher priority.

### 7.1.1. Create View
- You will need a **View** to complete this task.

- Name your **View***TUTO_P0032_VW***:
  ```sql
  select o.ordr_id as order_id,
         o.ordr_ctmr_id as customer_id,
         o.ordr_total as order_total,
         o.ordr_dd as order_date,
         o.ordr_user_name as user_name,
         oi.ordr_item_id as order_item_id,
         oi.ordr_item_prdt_info_id as product_id,
         oi.ordr_item_unit_price as unit_price,
         oi.ordr_item_quantity as quantity,
         p.prdt_info_name as product_name,
         p.prdt_info_descr as product_description,
         p.prdt_info_category as category,
         p.prdt_info_avail as product_avail,
         p.prdt_info_list_price as list_price
    from order_items oi
    join product_info p
      on oi.ordr_item_prdt_info_id = p.prdt_info_id
    join orders o
      on oi.ordr_item_ordr_id = o.ordr_id
  ```

### 7.1.2. Create Report
- Create a new page. To do this, navigate to the **App Builder** and click on **Create Page**.
- Select **Interactive Report** as the **Page Type**.

![](../../assets/Chapter-07/Features_01.jpg)

- Enter **Page Number** ***32*** and **Page Name** ***Customer Orders for Mobile***.
- Select **Local Database** as the **Data Source** and the view you created ***TUTO_P0032_VW*** as the **Table / View Name**.
- In the Navigation area, disable *Breadcrumb* and click **Create Page**.

![](../../assets/Chapter-07/Features_02.jpg)

- In the Page Designer, select your report ***Customer Orders for Mobile*** on the left side. On the right side, you can change the **Type**. First, choose the ***Reflow Report*** setting and click the **Run** button.

![](../../assets/Chapter-07/Features_03.jpg)

The displayed table is "responsive," meaning the display of the table columns automatically adapts to the screen size of the device.

![](../../assets/Chapter-07/Features_04.jpg)

If you shrink the browser window, the display area of the webpage also reduces. When the display screen width is ≤ 560 pixels, the table columns are no longer displayed side by side, but underneath each other.

![](../../assets/Chapter-07/Features_05.jpg)

- Return to the Page Designer and select ***Column Toggle Report*** as the **Type** and click **Run**.

![](../../assets/Chapter-07/Features_06.jpg)

- In this case, you can set which table columns should be displayed. Click the **Columns** button and select the desired columns.

![](../../assets/Chapter-07/Features_07.jpg)

This is a temporary personalized setting of the table columns. Other users are not affected by this setting. The setting is ***not*** saved across page reloads.
 

## 7.2. Progressive Web Apps
By selecting the "Install Progressive Web App" feature when creating the application, it can now be installed as a desktop application.

Progressive Web Apps are faster applications because they use a special browser cache to store resources more efficiently, which leads to faster page loading.

If it is a progressive Web App, a new entry **Install App** is visible in the navigation bar:

![](../../assets/Chapter-07/Features_08.jpg)

- Click the **Install App** button. A popup appears, allowing you to confirm that you want to install the application.

![](../../assets/Chapter-07/Features_09.jpg)

Once the installation is complete, the application opens in its own window, independent of the browser you are in.

![](../../assets/Chapter-07/Features_10.jpg)

The application can now also be found and started via the Start menu.

Existing applications created from APEX version 21.2 can also be converted into or used as progressive Web Apps. The following settings need to be adjusted:

- Open your application's page overview and click **Edit Application Definition**.

![](../../assets/Chapter-07/Features_11.jpg)

- Click **Progressive Web App** and enable the **Installable** option.

![](../../assets/Chapter-07/Features_12.jpg)

A section opens with more settings that can be used to customize the Progressive Web App user interface.

![](../../assets/Chapter-07/Features_13.jpg)


## 7.3. Persistent Authentication
For Progressive Web Apps, there is a new authentication method named "Persistent Authentication" with version 22.1.

Unlike normal APEX applications, a "**Remember me**" checkbox appears on the login screen, which should not be confused with "**Remember Username**".

![](../../assets/Chapter-07/Features_14.jpg)

When the "**Remember me**" option is activated, APEX remembers the login data for a certain period (30 days). During this time, the user can access the desired page without having to log in again. When a session expires, a new session is automatically provided.