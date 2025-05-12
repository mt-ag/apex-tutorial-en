# <a name="faceted-search"></a>9. Faceted Search

**Faceted Search** is a function for dynamically filtering displayed records and targeted searching within them. It is often used in online shops and is usually characterized by a fixed bar at the side of the page, where different filters are found in the form of checkboxes, sliders, and input fields.

## <a name="fs-erstellung-der-view"></a>9.1 Creation of the View

To process this task, a **View** is needed.

**View Name: *TUTO_P0051_VW***

**Query**:

 ```sql
select prdt_info_id,
       prdt_info_name,
       prdt_info_descr,
       prdt_info_category,
       prdt_info_avail,
       prdt_info_list_price 
from product_info
 ```
 
## <a name="fs-create-page"></a>9.2 Create Page

- Open the **App Builder** via the navigation bar, select your application and click the **Create Page** button.
- Select the page type **Component**.
- Select the region type **Faceted Search**.
 
![](../../assets/Chapter-09/Faceted_01.jpg) 

- Enter **Page Number *51*** and **Page Name *Product Search***. 
- Select the previously created View (TUTO_P0051_VW) under the point **Table/View Name**.
- In the **Navigation** area, disable *Breadcrumb* and click **Next**.

![](../../assets/Chapter-09/Faceted_02.jpg) 
  
- In the final step, disable all facets and click the **Create Page** button.

![](../../assets/Chapter-09/Faceted_03.jpg) 

- Then access the page via the **Run** button. 

The data is displayed in the right side area as a **Classic Report**. To the left is the search and filter bar, which currently only contains a search field that can be used to search for specific data. Additional options in the form of facets will be added there in the following steps.

![](../../assets/Chapter-09/Faceted_04.jpg) 

## <a name="fs-create-facets"></a>9.3 Create Facets

- Go back to the **Page Designer** and create a new **Facet** by right-clicking on the **Facets** entry and selecting **Create Facet**.

![](../../assets/Chapter-09/Faceted_05.jpg) 

- Select the item and modify the following fields as specified:

| | |  
|--|--|
| **Identification**|  |
| Name | *P51_CATEGORY* |
| Type| *Checkbox Group*| 
| **Label** | *Category*| 
| **List of Values**|  |
| Type | *SQL Query* |
| SQL Query | select distinct prdt_info_category as d, <br> prdt_info_category as r <br> from TUTO_P0051_VW| 
| | |

![](../../assets/Chapter-09/Faceted_06.jpg) 

Scroll further to the **Source** section. Change the Database Column to **PRDT_INFO_CATEGORY**.

![](../../assets/Chapter-09/Faceted_06a.jpg) 

- Start the **page** by clicking the **Run** button.

The Faceted Search Region now contains a new element with three checkboxes. These allow the displayed data on the right to be dynamically filtered by the values in the *Category* column.

![](../../assets/Chapter-09/Faceted_07.jpg) 

- Go back to the **Page Designer** to create a new **Facet**. Modify it according to the following specifications:

  | | |  
  |--|--|
  | **Identification** |  |
  | Name | *P51_LIST_PRICE* |
  | Type | *Range* | 
  | **Label** | *List Price*| 
  | **Settings** |  |
  | Select Multiple | *Enabled* |
  | Manual Entry | *Enabled* | 
  | **List of Values** |  |
  | Type | *Static Values* | 
  | | |

![](../../assets/Chapter-09/Faceted_08.jpg) 

- To enter the **List of Values**, click the button next to **Static Values**. The following window will open, where you can enter the specified values:

![](../../assets/Chapter-09/Faceted_09.jpg) 

- Under **Source**, set the **Database Column** to **PRDT_INFO_LIST_PRICE** and the **Data Type** for the **LIST_PRICE** column to ****NUMBER****.  

- Save and access the page again.

![](../../assets/Chapter-09/Faceted_10.jpg) 

The newly created facet contains, like the *Category Facet*, various checkboxes for filtering the displayed data. Below are two input fields where values can be manually entered as upper and lower limits.

![](../../assets/Chapter-09/Faceted_11.jpg) 