# Preparation

Welcome to the "Hands-On APEX 23.1" workshop of MT - IT Solutions.
Before you can start working on this tutorial, you need to request a workspace on Oracle's servers. You can do this in a few minutes at [apex.oracle.com](apex.oracle.com).

If you want to use English-language tutorials, you can do so via the following link. Simply click on [https://apex.oracle.com/en/learn/tutorials/](https://apex.oracle.com/en/learn/tutorials/) and work on the tutorials provided by APEX if you want to gain a broader insight into the world of APEX.

# 1. Import of Required Data

## 1.1. Script

A script is a list of commands for automating processes. In this case, the script generates tables and sequences. Additionally, the script populates the tables with data.

Tables are the basic unit of data storage in an Oracle database. They store data in rows and columns. A row is a collection of column information corresponding to a single data record. The columns define the data types of the individual data of a row.

Before you can start creating the application, you must first load the required data into the database of your workspace using a SQL script.

Uploading and executing the script ensures that all database objects are created and all data is inserted. You can then access this data in your application.

Use the attached SQL script (**Script.sql**) to import the data as described below.

## 1.2. Import of the Script

- Navigate to the **SQL Workshop** by choosing one of the two red-marked options.

![](../../assets/Chapter-01/Open_SQL_Workshop.jpg)

- Once you are in the **SQL Workshop**, click on **SQL Scripts**.

![](../../assets/Chapter-01/Open_SQL_Skripts.jpg)

- Now click on **Upload**.

![](../../assets/Chapter-01/SQL_Workshop_open_upload.jpg)

- Select the script **Script.sql**, which is located in the **Chapter-01** folder. Upload the script by clicking on the upload button or drag it into the intended field.

![](../../assets/Chapter-01/SQL_Workshop_upload_Skript.jpg)

- Start the script by pressing the **Run** button.

![](../../assets/Chapter-01/SQL_Workshop_run_Skript_1.jpg)

- Click on **Run Now**.

![](../../assets/Chapter-01/SQL_Workshop_run_Skript_2.jpg)

- After a successful import, you should see the following result:

![](../../assets/Chapter-01/SQL_Workshop_result.jpg)

All tables and data required for this tutorial should now be available in your workspace.  

## 1.3. Data Modeling with Quick SQL

Another way to create data models with little effort is by using Quick SQL.  
You can learn how this works in <span style="color:red">**Task #14: Excursus: Data Modeling with Quick SQL**</span>.