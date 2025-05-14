# Preparation

Welcome to the workshop "Hands-On APEX 23.2" by MT - IT Solutions.  
Before you can start working on this tutorial, you need to apply for a workspace on Oracle's servers. You can do this in just a few minutes at [apex.oracle.com](apex.oracle.com).

If you want to take advantage of English-language tutorials, you have the opportunity to do so at the following link. Simply click on [https://apex.oracle.com/en/learn/tutorials/](https://apex.oracle.com/en/learn/tutorials/) and work through the tutorials provided by APEX if you wish to gain further insight into the world of APEX.

# <a name="datenimport"></a> 1. Import the Required Data

## <a name="skript"></a> 1.1 Script

A script is a list of commands for automating processes. In this case, the script creates tables and sequences. In addition, the script populates the tables with data.

Tables are the basic unit of data storage in an Oracle database. They store data in rows and columns. A row is a collection of column information corresponding to a single record. The columns define the data types of each data in a row.

Before you can start creating the application, you must first load the required data into your workspace's database via a SQL script.

Uploading and executing the script ensures that all database objects are created and all data is inserted. Then you can access this data in your application.

Use the provided SQL script (**Skript.sql**) to import the data as described below.

## <a name="skriptimport"></a> 1.2 Import the Script

- Navigate to the **SQL Workshop** by choosing one of the two options marked in red.

![](../../assets/Chapter-01/Open_SQL_Workshop.jpg)

- Once you're in the **SQL Workshop**, click on **SQL Scripts**.

![](../../assets/Chapter-01/Open_SQL_Skripts.jpg)

- Now click on **Upload**.

![](../../assets/Chapter-01/SQL_Workshop_open_upload.jpg)

- Select the script **Skript.sql** located in the **Chapter-01** folder. Upload the script by clicking the upload button or dragging it into the designated area.

![](../../assets/Chapter-01/SQL_Workshop_upload_Skript.jpg)

- Start the script by pressing the **Run** button.

![](../../assets/Chapter-01/SQL_Workshop_run_Skript_1.jpg)

- Click on **Run Now**.

![](../../assets/Chapter-01/SQL_Workshop_run_Skript_2.jpg)

- After a successful import, you should see the following result:

![](../../assets/Chapter-01/SQL_Workshop_result.jpg)

All tables and data required for this tutorial should now be present in your workspace.

## <a name="datenmodellierung"></a> 1.3 Data Modeling with Quick SQL

Another way to create data models with little effort is Quick SQL.  
You can learn how this works in <span style="color:red">**Task #14: Excursion: Data Modeling with Quick SQL**</span>.