# <a name="charts"></a>6. Charts
Charts/Diagrams are used for the graphical representation of numerical values. APEX supports by default, among others, pie charts, line charts, bubble charts, scatter plots, and bar charts.

The aim of this chapter is to create a chart displaying the ratio of purchases sorted by categories.

## <a name="charts-erstellung-der-view"></a>6.1 Creation of the View
- A **View** is required to complete this task.

- Name your **View** ***TUTO_P0001_VW***
  ```sql
  select o.ordr_id,
         o.ordr_ctmr_id,
         o.ordr_total,
         o.ordr_dd,
         o.ordr_user_name,
         oi.ordr_item_id,
         oi.ordr_item_prdt_info_id,
         oi.ordr_item_unit_price,
         oi.ordr_item_quantity,
         p.prdt_info_name,
         p.prdt_info_descr,
         p.prdt_info_category,
         p.prdt_info_avail,
         p.prdt_info_list_price
    from order_items oi
    join product_info p
      on oi.ordr_item_prdt_info_id = p.prdt_info_id
    join orders o
      on oi.ordr_item_ordr_id = o.ordr_id
  ```
## <a name="charts-region"></a>6.2 Charts Region
- First, open the **App Builder** for your **application**. Then click on **Page 1 -** ***Home***.

- **Breadcrumbs** can usually be deleted after creation. They take up a lot of space and generally provide no added value for the end user. **Breadcrumbs** are hierarchical lists of links and offer hierarchical navigation.

- Right-click on the *Breadcrumb* **Apex TUTORIAL** and select **Delete**.

![](../../assets/Chapter-06/Charts_01.jpg)

- Also delete the region **Page Navigation**.

- Right-click on the entry **Components**. Select **Create Region** here.

![](../../assets/Chapter-06/Charts_02.jpg)

- Now select the region you created and change the **Title** to ***Orders per Category*** and the **Type** to ***Chart***.

![](../../assets/Chapter-06/Charts_03.jpg)

- Now select the entry **NEW** under Series and change the **Title** to ***Orders***.
- Under Source, choose **Location** as ***Local Database*** and specify the **Table Name** as the view you just created (***TUTO_P0001_VW***).

![](../../assets/Chapter-06/Charts_04.jpg)

- Now change the **Label** value to the column ***PRDT_INFO_CATEGORY*** and the **Value** to the column ***ORDR_TOTAL***.

![](../../assets/Chapter-06/Charts_05.jpg)

- Now switch to the **Attributes** tab in Orders per Category. Change the **Type** to ***Pie***. Your diagram will now be displayed as a pie chart. Pie charts are visual representations of parts of a whole in the form of a circle. The entire circle stands for the sum of the individual pie sectors.

![](../../assets/Chapter-06/Charts_06.jpg)

- Then click on the **Run** button.

- You will now see that on your homepage, the ratio of purchases sorted by categories is displayed.

![](../../assets/Chapter-06/Charts_07.jpg)