# 19. Template Components

**Template Components** are a new plug-in type in APEX. They allow you to define an HTML template (with or without additional CSS and JavaScript) and use placeholders. They are much easier to use than a full region plug-in, where you don't need in-depth knowledge of the plug-in APIs.

On each page, you can then create a section of this plug-in type, place a query, and then receive an instance of this template filled with the data for each returned row. You can also render a single instance in a region or even use them in columns of interactive reports.

## 19.1. Creating a "Template Components" (APEX Plugin)

1. Open the **Shared Components**, click on **Plug-ins** and then on **create**

![](../../assets/Chapter-19/1.jpg)

2. Click on **Next**

![](../../assets/Chapter-19/2.jpg)

3. Enter the values as follows:

| | | |
|--|--|--|
| **Field Name** | **Value** |
| Name | Progress Bars | 
| Internal Name | PROGRESS_BARS | 
| Type | Template Components | 
| Available as Single | Checkbox: YES | 
| Available as Multiple | Checkbox: YES | 
| | |

Finally, press the **Create Plug-in** button
![](../../assets/Chapter-19/3.jpg)

4. In the next step, insert the following code into **Partial**, **Report Body**, and **Report Row** at the corresponding places according to the screenshot. Finally, press the **Create Plug-in** button.

![](../../assets/Chapter-19/4.jpg)

Insert the HTML code in **Partial**
   ```html
    {if APEX$IS_LAZY_LOADING/}
       <p>loading...</p>
    {else/}
       <div class="mb-1 flex justify-between">
         <span class="text-base font-medium">#SKILL#</span>
         <span class="text-sm font-medium">#PCT#%</span>
       </div>
   
       <div class="h-2.5 w-full rounded-full bg-gray-200 ">
          <div class="h-2.5 rounded-full bg-blue-600" style="width: #PCT#%; background: {if COLOR_INDEX%assigned/}var(--u-color-#COLOR_INDEX#);{else/}var(--u-color-1);{endif/}">
          </div>
       </div>
   {endif/}
  ```

Insert the HTML code in **Report Body**

   ```html
    <div class="progress-list">#APEX$ROWS#</div>
  ```
Insert the HTML code in **Report Row**

   ```html
    <div #APEX$ROW_IDENTIFICATION# style="margin-top: 1lh;">#APEX$PARTIAL#</div>
  ```

5. You have successfully created the **Progress Bars** plugin. Click on the plugin name **Progress Bars** to continue editing.

![](../../assets/Chapter-19/5.jpg)

6. In the next step, scroll down to the **Custom Attributes** section and delete all existing attributes, then click on **Synchronize from Templates**. 

![](../../assets/Chapter-19/6.jpg)

7. Now only 3 attributes should be visible. Click on the first attribute **Color Index**

![](../../assets/Chapter-19/7.jpg)

8. Enter the values for the 3 attributes as follows and press **Apply Changes**.

| | | |
|--|--|--|
| **Color Index** | **Value** |
| Static ID | COLOR_INDEX | 
| Required | YES | 
| Data Types | Number |  
| | |

| | | |
|--|--|--|
| **Pct** | **Value** |
| Static ID | PCT | 
| Required | YES | 
| Data Types | Number |  
| | |

| | | |
|--|--|--|
| **Skill** | **Value** |
| Static ID | SKILL | 
| Required | YES | 
| Data Types | Varchar2 |  
| | |

9. In the next step, a **CSS file** will be created.

![](../../assets/Chapter-19/9.jpg)

10. The **CSS file** is created with the following name.

| | | |
|--|--|--|
| **Input-Field** | **Value** |
| File Name | styles.css |   
| | |

![](../../assets/Chapter-19/10.jpg)

11. Copy the **CSS code** below and paste it into APEX. Note the **Reference** link at the end, as we will need it shortly.

![](../../assets/Chapter-19/11.jpg)

   ```css
.progress-list:first-child {
    margin-top: 0px;
}

.mb-1 {
  margin-bottom: 0.25rem;
}

.flex {
  display: flex;
}

.h-2 {
  height: 0.5rem;
}

.h-2\.5 {
  height: 0.625rem;
}

.w-full {
  width: 100%;
}

.justify-between {
  justify-content: space-between;
}

.rounded-full {
  border-radius: 9999px;
}

.bg-blue-600 {
  --tw-bg-opacity: 1;
  background-color: rgb(37 99 235 / var(--tw-bg-opacity));
}

.bg-gray-200 {
  --tw-bg-opacity: 1;
  background-color: rgb(229 231 235 / var(--tw-bg-opacity));
}

.text-base {
  font-size: 1rem;
  line-height: 1.5rem;
}

.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.font-medium {
  font-weight: 500;
}

.text-blue-700 {
  --tw-text-opacity: 1;
  color: rgb(29 78 216 / var(--tw-text-opacity));
}

  ```

12. Insert the copied **Reference** link in the appropriate place as shown in the screenshot and save.

![](../../assets/Chapter-19/12.jpg)

Up to this step, the **plug-in** has been successfully created.

13. In the next step, a new APEX page will be created with the plugin.

![](../../assets/Chapter-19/13.jpg)

14. Create the new page as follows and click on **create Page**:

| | | |
|--|--|--|
| **Field** | **Value** |
| Page Number | 120 | 
| Name | Progress Bars | 
| Use Breadcrumb | Disable |  
| Icon | fa-bar-chart-horizontal |  
| | |

![](../../assets/Chapter-19/14.jpg)

15. On the page, create a new region with the title: **Progress Bars**. Then select at Type the previously created plug-in: **Progress Bars**.

![](../../assets/Chapter-19/15.jpg)

16. Next, select **SQL Query** as the Type and insert the SQL code below in **SQL-Query**. Then switch to the **Attributes** tab.

![](../../assets/Chapter-19/16.jpg)

   ```sql
WITH web_programming_languages AS (
  SELECT 'JavaScript'   AS language_name FROM DUAL
  UNION ALL
  SELECT 'SQL'          AS language_name FROM DUAL
  UNION ALL
  SELECT 'PL/SQL'       AS language_name FROM DUAL
  UNION ALL
  SELECT 'Python'       AS language_name FROM DUAL
  UNION ALL
  SELECT 'Java'         AS language_name FROM DUAL
  UNION ALL
  SELECT 'C#'           AS language_name FROM DUAL
  UNION ALL
  SELECT 'PHP'          AS language_name FROM DUAL
  UNION ALL
  SELECT 'Ruby'         AS language_name FROM DUAL
  UNION ALL
  SELECT 'TypeScript'   AS language_name FROM DUAL
  UNION ALL
  SELECT 'Swift'        AS language_name FROM DUAL 
)
SELECT language_name                        as SKILLS
     , FLOOR(DBMS_RANDOM.VALUE(0, 100))     as PCT
     , FLOOR(DBMS_RANDOM.VALUE(0, 45))      as COLOR_INDEX
  FROM web_programming_languages
;
  ```

17. In the **Attributes** tab, adjust the values as follows:

| | | |
|--|--|--|
| **Field** | **Value** |
| Display | Multiple (Report) | 
| Color Index | COLOR_INDEX | 
| Pct | PCT |  
| Skill | SKILLS |  
| | |

![](../../assets/Chapter-19/17.jpg)

18. Finally, create a button here and save the APEX page.

Create a button with the following settings:

| | | |
|--|--|--|
| **Field** | **Value** |
| Button Name | P120_REFRESH_PAGE | 
| Label | Refresh Page | 
|   |  
| Region | Progress Bars |  
| Position | Next |  
|   |  
| Button Template | Text with Icon |  
| icon | fa-refresh |  
|   |  
| Action | Submit Page |  
| | |

Click on **Template Options**

| | | |
|--|--|--|
| **Field** | **Value** |
| Type | success | 
| Icon Hover Animation | Push | 
| Width | Stretch |   
| | |

![](../../assets/Chapter-19/18.jpg)

19. Finally, the page looks as follows. Press the Refresh Button to reload **Random** values.

![](../../assets/Chapter-19/19.jpg)

<br><br>
Congratulations!
You have successfully completed the tutorial.  
If you want to learn more about APEX, feel free to visit our APEX portal:  
[apex.mt-itsolutions.com/from-zero-to-hero](https://apex.mt-itsolutions.com/from-zero-to-hero)