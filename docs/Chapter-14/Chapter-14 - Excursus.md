# <a name="exkurs-datenmodellierung-mittels-quick-sql"></a>14. Excursion: Data Modeling Using Quick SQL

Quick SQL allows for rapid design of data models using a **Markdown-like shorthand syntax**. Main detail relationships can be represented via an **ERM** ("Entity-Relationship Model").  

> More information is available at [https://apex.oracle.com/en/quicksql/](https://apex.oracle.com/en/quicksql/) (Login required).

## <a name="ex-erstellung-der-datenbank-tabelle"></a>14.1 Creating the Database Table

- Navigate to **SQL Workshop** and then click on **SQL Scripts**.

- Click on **Quick SQL** in the top right corner.

![](../../assets/Chapter-14/Exkurs_01.jpg)
 
- On the following page, enter the following **Quick SQL code** in the left text area:

 ```sql
SALARIES /insert 5
    SARY_ID int/pk
    SARY_EMPLOYEE_NAME vc255/values Mueller, Vogel, Schneider, Fischer, Schmidt
    SARY_DEPARTMENT vc30/check SALE DEV MAN SUP
    SARY_SALARY num/between 500 and 4000
 ```

>! Please pay attention to the indentations shown above when entering the code!  

- The code is automatically translated into SQL code. The generated SQL code is displayed in the right text area.

![](../../assets/Chapter-14/Exkurs_02.jpg)

- Click on **Save SQL Script** to save the code. 
- A window opens where you need to give a name to the script. Name the **script** ***salaries*** and then click on **Save Script**. 

![](../../assets/Chapter-14/Exkurs_03.jpg)

- Then click on **Review and Run**. 

![](../../assets/Chapter-14/Exkurs_04.jpg)

- You will see a preview of your SQL code. Start the script by clicking the **Run** button. 

![](../../assets/Chapter-14/Exkurs_05.jpg)

- Click on **Run Now**.  

![](../../assets/Chapter-14/Exkurs_06.jpg) 
 
- After successful import, you should see the following output:

![](../../assets/Chapter-14/Exkurs_07.jpg)
 
## <a name="ex-erstellung-eines-interactive-reports"></a>14.2 Creating an Interactive Report

To visualize the data just created, you will create an Interactive Report in this task.
- To do this, go back to the **App Builder**, then to your **Application** and click on **Create Page** and select **Interactive Report**.

![](../../assets/Chapter-14/Exkurs_08.jpg) 
 
- In the next window, enter **Page Number *71*** and for **Page Name *Salaries***.
- Select ***SALARIES*** as the **Table / View Name**.
- In the Navigation area, disable the *Breadcrumb* and click on **Create Page**.

![](../../assets/Chapter-14/Exkurs_09.jpg) 

- The Page Designer opens. When you click **Run**, the page loads and you see the report you just created using Quick SQL.

![](../../assets/Chapter-14/Exkurs_10.jpg)

## <a name="beispieldaten-mittels-data-generator-generieren"></a>14.3 Generating Sample Data Using Data Generator

Use the Data Generator utility to create **blueprints** and then generate sample data.
- Navigate to **SQL Workshop** and then click on **Utilities**.
- Then click on **Data Generator**.

![](../../assets/Chapter-14/Exkurs_11.jpg)

- Click on **Create Blueprint** here.

![](../../assets/Chapter-14/Exkurs_12.jpg)

- In the next step, select **Use Existing** Tables to insert sample data into an already existing table.

![](../../assets/Chapter-14/Exkurs_13.jpg)

- In the next step, name the *Blueprint* **Salaries Blueprint**, and select the previously created table **Salaries**. Finally, click on **Create Blueprint**.

![](../../assets/Chapter-14/Exkurs_14.jpg) 

- You are now automatically redirected to the Blueprint Designer. From here, you can define what sample data should be generated.
- For **SARY_EMPLOYEE_NAME**, select the Data Source Built-In and the **Built-In** type **Last Name**. Since no null values should be inserted, **required** must also be set. Finally, Maximum Length according to the table specification with varchar(9) must be set to **9**.

![](../../assets/Chapter-14/Exkurs_15.jpg) 
 
- For **SARY_SALARY**, select the Data Source **Built-In** and the Built-In type **Number** (search for number.random). Set **500** as the Minimum Value and **4000** as the Maximum Value. Since no null values should be inserted here as well, **required** must also be set here.

![](../../assets/Chapter-14/Exkurs_16.jpg)

- The blueprint for the sample data would now be fully configured. Save it first by clicking on **Save**. 

![](../../assets/Chapter-14/Exkurs_17.jpg)

- Now click on **Preview Data** to get a preview of the generated data.

![](../../assets/Chapter-14/Exkurs_18.jpg)

- To finally generate the sample data, next click on **Generate Data**.

![](../../assets/Chapter-14/Exkurs_19.jpg)

- Select **Insert into Database** here and the Insert Method Insert Into to directly insert the data into the database table. Then click on **Insert Data**.
 
![](../../assets/Chapter-14/Exkurs_20.jpg)
 
- To check the result of the inserts, call up the previously created Page 71 in the App Builder again. When you now click on **Run**, the page loads and you see the report with the newly inserted data.

![](../../assets/Chapter-14/Exkurs_21.jpg)