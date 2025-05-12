# <a name="oracle-apex-und-ai"></a> 22. Oracle APEX and AI
# <a name="testen-von-funktionen-oracle-apex-und-ai"></a>22.1 Part 1: Testing Three Different Functions with Oracle APEX and AI

In this chapter, we will test three different AI functions in combination with Oracle APEX. We will focus on using AI to assist with SQL creation, app generation, and task execution within an application.

## <a name="unterstuetzung-bei-der-erstellung-von-abfragen"></a>1. Support for Creating SQL Queries

In this section, we test how AI can assist us in creating SQL queries. The AI is used to generate complex SQL queries efficiently and error-free, based on the requirements of the database tables and business logic.

**Objective:** Create various SQL queries running on the databases and optimize the process by integrating AI.

## <a name="automatisierte-app-erstellung"></a>2. Automated App Creation with AI

The second test focuses on AI's ability to generate a complete application with Oracle APEX. This application will link different tables and allow data management, including **Insert**, **Update**, and **Delete** functions. Additionally, the app should include the following features:

- **Report Page:** A report that displays the data from the tables and can be filtered.
- **Dashboard:** A dashboard with key metrics, such as the number of customers, orders, or sales, visualized through charts.
- **Search Function:** A search page where specific orders or customers can be searched.

**Objective:** Use AI to create a fully functional application in Oracle APEX that enables data management from various tables, including a dashboard, report page, and search function.

## <a name="aufgabenautomatisierung-durch-ai"></a>3. Task Automation within the Application by AI

The third function tests how AI can take over tasks within the application. The focus is specifically on the AI processing incoming emails and generating automatic replies. For example, when an email arrives, AI should draft a response based on it.

**Objective:** Use AI to automatically generate email replies. This function should increase efficiency by creating context-based responses.

## <a name="schritt-zugriff-auf-den-app-builder"></a>Step 1: Access App Builder

To begin creating the AI service, first navigate to the **App Builder**.

1. Click on **App Builder** in the main menu.
2. Then select **Workspace Utilities** to utilize more tools.

![](../../assets/Chapter-22/ai_basic_01.jpg)

---

## <a name="schritt-zugriff-auf-den-ai-generator"></a>Step 2: Access AI Generator

Once you are in the **Workspace Utilities** area:

1. Click on **Generator AI** to start the AI service.

![](../../assets/Chapter-22/ai_basic_02.jpg)

---

## <a name="schritt-erstellen-eines-ai-services"></a>Step 3: Create an AI Service

To configure the AI service:

1. Click on the **Create** button to create a new AI service.

![](../../assets/Chapter-22/ai_basic_03.jpg)

---

## <a name="schritt-ai-service-konfigurieren"></a>Step 4: Configure AI Service

Define the settings for the AI service as shown in the image:

![](../../assets/Chapter-22/ai_basic_04.jpg)

---

## <a name="schritt-wechsel-zum-sql-workshop"></a>Step 5: Switch to SQL Workshop

After setting the AI service, navigate to the **SQL Workshop**.

1. Go to the **SQL Commands** area.
2. Click on the **APEX Assistant** button to receive support for SQL queries.

![](../../assets/Chapter-22/ai_basic_05.jpg)
---

## <a name="schritt-nutzung-des-apex-assistant"></a>Step 6: Use APEX Assistant for SQL Queries

In the **APEX Assistant** field, you can receive help in creating SQL queries. Enter the following example text:

**Description of the query:**  
> Create a SQL query that finds all customers from the "CUSTOMERS" table whose credit limit is greater than 5000. Only return key information such as the customer's name, city, email, and credit limit.

```sql
select ctmr_frst_name,
       ctmr_last_name,
       ctmr_city,
       ctmr_email,
       ctmr_credit_limit
  from customers
 where ctmr_credit_limit > 5000
```

![](../../assets/Chapter-22/ai_basic_06.jpg)

---

## <a name="schritt-sql-query-vorschlaege"></a>Step 7: SQL Query Suggestions

After entering the text, you will receive suggestions for SQL queries. Here is an example:

**Description of the query:** 
> Search for all customers and return the full name of the customer (First Name and Last Name), their email address, and the number of orders each customer has placed. Use the data from the "CUSTOMERS" and "ORDERS" tables, with customers stored in the "CUSTOMERS" table and their orders in the "ORDERS" table. Link the two tables using the customer ID. Only output the full name, email address, and the number of orders.

```sql
select ctmr.ctmr_frst_name || ' ' || ctmr.ctmr_last_name as full_name,
       ctmr.ctmr_email,
       count(ord.ordr_id)                          as order_count
  from customers ctmr
  left join orders ord
    on ctmr.ctmr_id = ord.ordr_ctmr_id
 group by ctmr.ctmr_frst_name,
          ctmr.ctmr_last_name,
          ctmr.ctmr_email
```

![](../../assets/Chapter-22/ai_basic_07.jpg)

---

## <a name="schritt-weiteres-sql-beispiel"></a>Step 8: Another SQL Example

Here is another example of an SQL query:

**Description of the query:** 
> Search for all customers and return the full name of the customer (First Name and Last Name), their email address, and the number of orders each customer has placed since 2016. Consider only orders with a total value (ORDR_TOTAL) greater than 100. Customer information comes from the "CUSTOMERS" table, and orders are stored in the "ORDERS" table. Link the two tables using the customer ID. Only return the following information: full name, email address, and the number of qualified orders since 2016.

```sql
select ctmr.ctmr_frst_name || ' ' || ctmr.ctmr_last_name as full_name,
       ctmr.ctmr_email,
       count(ordr.ordr_id)                     as order_count
  from customers           ctmr
  join orders              ordr
    on ctmr.ctmr_id = ordr.ordr_ctmr_id
 where ordr.ordr_dd >= to_date('2016-01-01', 'YYYY-MM-DD')
   and ordr.ordr_total > 100
 group by ctmr.ctmr_frst_name,
          ctmr.ctmr_last_name,
          ctmr.ctmr_email
```

![](../../assets/Chapter-22/ai_basic_08.jpg)

---

That was the first part of the guide showing how AI can assist you with SQL query creation based on your own database.

# <a name="erstellen-einer-app-mit-ai"></a>22.1 Part 2: Creating an App with Help from AI in Oracle APEX

## <a name="schritt-zugriff-auf-den-app-builder-2"></a>Step 1: Access App Builder

To create an application with the help of AI, proceed as follows:

1. Navigate to the **App Builder**.
2. Click **Create** to start the process of creating a new app.

![](../../assets/Chapter-22/ai_basic_09.jpg)

---

## <a name="schritt-app-erstellung-mit-ai-starten"></a>Step 2: Start App Creation with AI

Instead of entering a name for the application, click on **Create app using generative AI**.

![](../../assets/Chapter-22/ai_basic_10.jpg)

---

## <a name="schritt-eingeben-eines-prompts"></a>Step 3: Enter a Prompt

In the search bar, you can now enter a prompt describing the application you want to create. For example, enter a description of your tables and requirements and click on the small arrow.

**Description of the prompt:** 
> Create a full application to manage the following tables: CUSTOMERS, ORDERS, ORDER_ITEMS, PRODUCT_INFO, STATES, and DEPARTMENTS. The application should allow me to create, update, and delete records for all these tables.
> 
> Additionally, provide the following functionalities:
> 
> Search Page: Create a search page where I can search for the orders of any customer by customer name, order date, or other relevant criteria.
> 
> Report Page: Create a report page that shows how many sales I have made, including the total revenue. The report should allow filtering by date range, customer, and product.
> 
> Dashboard: Create a dashboard that displays key metrics, such as the total number of customers, total sales, and the most frequently ordered products. Visualize this data with charts and summary figures.
> 
> Ensure the application has a user-friendly interface with the ability to easily navigate between the search page, report page, and dashboard. Include necessary validations, dynamic actions, and form handling where appropriate. Also, provide a security mechanism that allows role-based access to certain features, such as administrative actions.

![](../../assets/Chapter-22/ai_basic_11.jpg)

---

## <a name="schritt-app-wird-generiert"></a>Step 4: App is Generated

Once you have entered the prompt, AI begins to create the app. You will see the progress display represented by dots showing the status of the creation process.

![](../../assets/Chapter-22/ai_basic_12.jpg)

---

## <a name="ueberpruefung-der-generierten-app"></a>Step 5: Review the Generated App

After the app is generated, you receive an overview of all tables and pages included in the app. Here you can see which functions are intended for which tables. If everything is correct, simply click on **Create Application**.

![](../../assets/Chapter-22/ai_basic_13.jpg)

---

## <a name="schritt-seitenuebersicht-anpassen"></a>Step 6: Adjust Page Overview

On the next page, you will be shown a brief overview of the automatically created pages. If you wish to make changes, you can do so here. Otherwise, click on **Create Application**.

![](../../assets/Chapter-22/ai_basic_14.jpg)

---

## <a name="schritt-erstellung-der-app"></a>Step 7: App Creation

The application is created within a few seconds.

![](../../assets/Chapter-22/ai_basic_15.jpg)

---

## <a name="schritt-starten-der-anwendung"></a>Step 8: Launch the Application

When you run the application, you can see several buttons on the navigation bar. You can now navigate through the application, insert, edit, and manage various data. Additionally, there is a **Search Page** and a **Dashboard Page** providing additional functionalities.

![](../../assets/Chapter-22/ai_basic_17.jpg)

---

That was the second part of the guide showing how you can create an application with the help of AI in Oracle APEX. This process facilitates managing your data and provides the ability to efficiently create your app through generative AI, including dashboards, search pages, and more.

# <a name="erstellen-einer-email-reply-funktion-mit-ai"></a>22.1 Part 3: Creating an Email Reply Function with AI in Oracle APEX

## <a name="schritt-erstellen-einer-neuen-leeren-seite"></a>Step 1: Create a New Blank Page

1. In your application, go to **Create** and create a new **Blank Page**.
2. Click **Next** to continue.

![](../../assets/Chapter-22/ai_basic_18.jpg)

---

## <a name="schritt-seiteneinstellungen"></a>Step 2: Page Settings

Enter the settings as shown in the image and click on **Create Page**.

![](../../assets/Chapter-22/ai_basic_19.jpg)

---

## <a name="schritt-erstellen-einer-region"></a>Step 3: Create the Region

Create a region named **Email Reply**.

![](../../assets/Chapter-22/ai_basic_20.jpg)

---

## <a name="schritt-hinzufuegen-eines-items"></a>Step 4: Add an Item

Add a new item:

- **Item Name**: `P50_MAIL`
- **Label**: `MAIL`

![](../../assets/Chapter-22/ai_basic_21.jpg)

Scroll down and enter the desired email in the **Static Value** field. Then click **OK**.

> Subject: Urgent: Password Recovery Assistance Required
> 
> Dear Our Company,
> 
> I hope this message finds you well. I am writing to request your urgent assistance in recovering my password for my account with your services. Unfortunately, I am currently unable to access my account and have been unsuccessful in using the standard password recovery options provided.
> 
> Here are my account details for your reference:
> 
> Account Holder Name: John Doe
> Username/Email Associated with Account: john.doe@example.com
> Could you please assist me in resetting my password at your earliest convenience? If there are any additional steps or verification processes required, please let me know so that I can promptly provide the necessary information.
> 
> Thank you for your immediate attention to this matter. I appreciate your help and look forward to resolving this issue as soon as possible.
> 
> Best regards,
> 
> Edward Logan
> 
> Edward.Logan@example.com
> 
> (123) 456-7890

![](../../assets/Chapter-22/ai_basic_22.jpg)

---

## <a name="schritt-erstellen-eines-buttons"></a>Step 5: Create a Button

Create a new button with the settings shown.

![](../../assets/Chapter-22/ai_basic_23.jpg)

---

## <a name="schritt-hinzufuegen-einer-dynamic-action"></a>Step 6: Add a Dynamic Action

Select the previously created button and add a **Dynamic Action** named **click on mail reply button**.

![](../../assets/Chapter-22/ai_basic_24.jpg)

---

## <a name="schritt-konfigurieren-der-dynamic-action"></a>Step 7: Configure the Dynamic Action

- **Action Name**: `ai mail reply`
- **Action**: Select **Open AI Assistant**.
- Select the previously created AI service **Tutorial**.

Enter the System Prompt as follows:

- **System Prompt**: `Here is an E-Mail, please reply the E-Mail`.
- **Display As**: Leave the default setting on **Dialog**.

![](../../assets/Chapter-22/ai_basic_25.jpg)

---

## <a name="schritt-system-prompt-und-anzeigeneinstellungen"></a>Step 8: System Prompt and Display Settings

Scroll down and configure the following settings:

- **Initial Prompt**: Choose **Item** and then the item **P50_MAIL**.
- **Message**: Enter, for example: `Here is an E-Mail, please reply the E-Mail`.

Then save the page and run it.

![](../../assets/Chapter-22/ai_basic_26.jpg)

---

## <a name="schritt-ausfuehren-der-seite"></a>Step 9: Running the Page

After saving, the page looks like this. You can now click on the **Mail Reply** button.

![](../../assets/Chapter-22/ai_basic_27.jpg)

---

## <a name="schritt-email-verarbeitung-durch-ai"></a>Step 10: Email Processing by AI

After clicking on **Here is an E-Mail, Please Reply the E-Mail**, the AI generates a response to the email.

![](../../assets/Chapter-22/ai_basic_28.jpg)

--- 

That was the third part of the guide where you learned how to create an email reply function with AI in Oracle APEX.

Thank you for working through this guide. You now have the tools to create SQL queries, efficiently develop applications, and automatically respond to emails. This demonstrates how powerful Oracle APEX can be in combination with generative AI.

We hope this guide has helped you better understand and productively apply the integration of AI in Oracle APEX. Should you have further questions or new challenges, we are here to assist you.

Good luck with your projects!