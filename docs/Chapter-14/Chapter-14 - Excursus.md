# <a name="exkurs-datenmodellierung-mittels-quick-sql"></a>14. Excursus: Data Modeling with Quick SQL

With Quick SQL, data models can be quickly designed using a **Markdown-like shorthand syntax**. Major detail relationships can be represented through an **ERM** ("Entity-Relationship Model").  

> For more information, visit [https://apex.oracle.com/en/quicksql/](https://apex.oracle.com/en/quicksql/) (Login required).

## <a name="ex-erstellung-der-datenbank-tabelle"></a>14.1 Creating the Database Table

- Navigate to **SQL Workshop** and then click on **SQL Scripts**.

- Click on **Quick SQL** at the top right.

![](../../assets/Chapter-14/Exkurs_01.jpg)
 
- On the following page, enter the following **Quick SQL code** in the left text area:

 ```sql
SALARIES /insert 5
    SARY_ID int/pk
    SARY_EMPLOYEE_NAME vc255/values Mueller, Vogel, Schneider, Fischer, Schmidt
    SARY_DEPARTMENT vc30/check SALE DEV MAN SUP
    SARY_SALARY num/between 500 and 4000
 ```

>! Please pay attention to the indentation shown above when entering!  

- The code is automatically translated into SQL code. The generated SQL code is displayed in the right text area. 

![](../../assets/Chapter-14/Exkurs_02.jpg)

- Click on **Save SQL Script** to save the code. 
- A window will open where you must assign a name to the script. Name the **script** ***salaries*** and then click on **Save Script**. 

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
- To do this, go back to the **App Builder**, then to your **Application**, and then click on **Create Page** and select **Interactive Report**.

![](../../assets/Chapter-14/Exkurs_08.jpg) 
 
- In the following window, enter **Page Number *71*** and **Page Name *Salaries***.
- For **Table / View Name** select ***SALARIES***.
- Disable *Breadcrumb* in the Navigation area and click on **Create Page**.

![](../../assets/Chapter-14/Exkurs_09.jpg) 

- The Page Designer opens. If you click on **Run**, the page loads and you see the report you just created with Quick SQL.

![](../../assets/Chapter-14/Exkurs_10.jpg)

## <a name="beispieldaten-mittels-data-generator-generieren"></a>14.3 Generating Sample Data Using Data Generator

Use the Data Generator utility to create **Blueprints** and then generate sample data.
- Navigate to **SQL Workshop** and then click on **Utilities**.
- Then click on **Data Generator**.

![](../../assets/Chapter-14/Exkurs_11.jpg)

- Click on **Create Blueprint** here.

![](../../assets/Chapter-14/Exkurs_12.jpg)

- In the next step select **Use Existing** Tables to insert sample data into an already existing table.

![](../../assets/Chapter-14/Exkurs_13.jpg)

- In the next step, name the *Blueprint* **Salaries Blueprint**, and select the previously created table **Salaries**. Finally, click on **Create Blueprint**.

![](../../assets/Chapter-14/Exkurs_14.jpg) 

- You will now automatically be redirected to the Blueprint Designer. From here, you can define what sample data should be generated.
- Select for **SARY_EMPLOYEE_NAME** the Data Source Built-In and the **Built-In** type **Last Name**. Since no null values should be inserted, you must set **required**. Finally, the Maximum Length must be set to **9** according to the table specification with varchar(9).

![](../../assets/Chapter-14/Exkurs_15.jpg) 
 
- Select for **SARY_SALARY** the Data Source **Built-In** and the Built-In type **Number** (search number.random). Specify **500** as Minimum Value and **4000** as Maximum Value. Since no null values should be inserted here as well, **required** must also be set here.

![](../../assets/Chapter-14/Exkurs_16.jpg)

- The blueprint for the sample data is now configured. Save it first by clicking on **Save**. 

![](../../assets/Chapter-14/Exkurs_17.jpg)

- Now click on **Preview Data** to get a preview of the generated data.

![](../../assets/Chapter-14/Exkurs_18.jpg)

- To finally generate the sample data, next click on **Generate Data**.

![](../../assets/Chapter-14/Exkurs_19.jpg)

- Select **Insert into Database** and the Insert Method Insert Into to insert the data directly into the database table. Then click on **Insert Data**.
 
![](../../assets/Chapter-14/Exkurs_20.jpg)
 
- To check the result of the inserts, call up the previously created Page 71 in the App-Builder again. When you click on **Run**, the page loads and you see the report with the newly inserted data.

![](../../assets/Chapter-14/Exkurs_21.jpg)