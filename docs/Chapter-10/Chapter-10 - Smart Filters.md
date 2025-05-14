# 10. Smart Filters
The **Smart Filters** provide the ability to easily narrow down data using filter suggestions or search terms. These are displayed as chips under the search bar or as suggestions while typing.
## 10.1. Creation of the View
A **View** is needed for this task. 
**View Name: TUTO_P0091_VW**
Query:
 ```sql
select prdt_info_id as product_id,
       prdt_info_name as product_name,
       prdt_info_descr as product_description,
       prdt_info_category as category,
       prdt_info_avail as product_avail,
       prdt_info_list_price as list_price 
from product_info
```

## 10.2. Create Page
- Open the **App Builder** via the navigation bar, select your application, and click on the **Create Page** button.  
- Choose the **Component** page type.  
- Select the **Smart Filters** region type.  
 
![](../../assets/Chapter-10/Smart_01.jpg)  

- Enter **Page Number 91** and **Page Name Product Filter**. 
- Under **Table/View Name**, select the previously created view (TUTO_P0091_VW).  
- In the **Navigation** section, deactivate *Breadcrumb* and click **Next**.  
  
![](../../assets/Chapter-10/Smart_02.jpg)  

- Deactivate all filters in the last step and click the **Create Page** button.  
 
![](../../assets/Chapter-10/Smart_03.jpg)  

- Then call up the page using the **Run** button.  
The data is displayed as a **Classic Report**. Above it is a search bar, under which the chips to be added next are displayed.  

![](../../assets/Chapter-10/Smart_04.jpg)  
 
## 10.3. Create Filters
- Switch back to the **Page Designer** and create a new filter by right-clicking on the **Filters** entry and then selecting **Create Filter**.  

![](../../assets/Chapter-10/Smart_05.jpg)  

- Select the item and modify the following fields as specified:  

  | | |  
  |--|--|
  | **Identification** |  |
  | Name | *P91_PRODUCT_NAME* |
  | Type | *Checkbox Group* |  
  | **Label**| *Product Name* |
  | **List of Values** |  |
  | Type | *Distinct Values* |
  | | |  

- Start the page by clicking the Run button.  

![](../../assets/Chapter-10/Smart_06.jpg)  

When clicking in the search bar, the *Product Name* filter appears. Clicking on the filter displays all filter options based on the column values. By clicking on the displayed suggestion, it is adopted as a filter in the search bar.  

- Switch back to the **Page Designer** to create another filter. Modify it according to the following guidelines:  

  | | |  
  |--|--|
  | **Identification** |
  | Name | *P91_CATEGORY* |
  | Type | *Checkbox Group*|  
  | **Label**| *Category* |
  | **List of Values** |  |
  | Type | *Distinct Values* |
  | | |  

![](../../assets/Chapter-10/Smart_07.jpg)  

- Save and call up the page again.  
The created filters for *Product Name* and *Category* are now displayed when clicking in the search bar.  

![](../../assets/Chapter-10/Smart_08.jpg)  
