# <a name="smart-filters"></a>10. Smart Filters
The **Smart Filters** provide the option to easily narrow down data using filter suggestions or search terms. These appear as chips under the search bar or as suggestions while typing.
## <a name="sf-erstellung-der-view"></a>10.1 Creating the View
A **View** is needed to edit this task.  
**View Name: TUTO_P0091_VW**
Query:
 ```sql
select prdt_info_id,
       prdt_info_name,
       prdt_info_descr,
       prdt_info_category,
       prdt_info_avail,
       prdt_info_list_price
from product_info
```

## <a name="sf-create-page"></a>10.2 Create Page
- Open the **App Builder** via the navigation bar, select your application, and click on the **Create Page** button.  
- Select the page type **Component**.  
- Select the region type **Smart Filters**.  
 
![](../../assets/Chapter-10/Smart_01.jpg)  

- Enter **Page Number 91** and **Page Name Product Filter**. 
- Select the previously created view (TUTO_P0091_VW) under **Table/View Name**.  
- In the **Navigation** section, disable the *Breadcrumb* and click **Next**.  
  
![](../../assets/Chapter-10/Smart_02.jpg)  

- In the final step, disable all filters and click on the **Create Page** button.  
 
![](../../assets/Chapter-10/Smart_03.jpg)  

- Then access the page using the **Run** button.  
The data is displayed as a **Classic Report**. Above it, there is a search bar under which the filters are displayed as chips, which will be added in the following steps.  

![](../../assets/Chapter-10/Smart_04.jpg)  
 
## <a name="sf-create-filters"></a>10.3 Create Filters
- Go back to the **Page Designer** and create a new filter by right-clicking on the **Filters** entry and then selecting **Create Filter**.  

![](../../assets/Chapter-10/Smart_05.jpg)  

- Select the item and modify the following fields as specified:  

  | | |  
  |--|--|
  | **Identification** |  |
  | Name | *P91_PRDT_INFO_NAME* |
  | Type | *Checkbox Group* |  
  | **Label**| *Product Name* |
  | **List of Values** |  |
  | Type | *Distinct Values* |
  | | |  

- Launch the page by clicking on the Run Button.  

![](../../assets/Chapter-10/Smart_06.jpg)  

When clicking into the search bar, the *Product Name* filter appears. If you click on the filter, all filter options based on the column values are displayed. Clicking on the displayed suggestion adopts it as a filter in the search bar.  

- Go back to the **Page Designer** to create another filter. Modify it as per the following instructions:  

  | | |  
  |--|--|
  | **Identification** |
  | Name | *P91_PRDT_INFO_CATEGORY* |
  | Type | *Checkbox Group*|  
  | **Label**| *Category* |
  | **List of Values** |  |
  | Type | *Distinct Values* |
  | | |  

![](../../assets/Chapter-10/Smart_07.jpg)  

- Save and access the page again.  
The created filters for *Product Name* and *Category* are now displayed when clicking into the search bar.  

![](../../assets/Chapter-10/Smart_08.jpg)  
