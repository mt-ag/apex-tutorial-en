# <a name="cards-region"></a>8. Cards Region

Cards are a popular form in web design to present information clearly and vividly. The Cards in APEX can be designed in various ways. For example, you can add icons to a card, display images or videos, or define actions for the card (e.g., through links or buttons).

In this chapter, we will create a page based on a Cards Region. In the first step, we will create a Default Cards Region, and in the second chapter, we will edit it so that an image is displayed in the card.  

## <a name="cards-view-erstellen"></a>8.1	Create View

For this task, a **View** is needed.  
**View Name: *TUTO_P0041_VW***
**Query**:

```sql
select prdt_info_id,
       prdt_info_name,
       prdt_info_descr,
       prdt_info_category,
       prdt_info_product_image,
       prdt_info_list_price
from product_info
 ```

## <a name="cards-seite-erstellen"></a>8.2	Create Page

- Open the **App Builder** from the navigation bar, select your application, and click on the **Create Page** button.  
- Select the page type **Report**.  
- Select the region type **Cards**.  

![](../../assets/Chapter-08/Cards_01.jpg)

- Enter **Page Number *41*** and **Page Name *Products***. Then click the **Next** button.  
- Choose the created view (TUTO_P0041_VW) under the **Table/View Name** section.  
- Disable the *Breadcrumb* under the **Navigation** section and click **Next**.  

![](../../assets/Chapter-08/Cards_02.jpg) 

- Then specify the attributes of your card. For the layout format, choose **Grid**. This ensures that the cards are arranged in an even grid.   

You now need to specify which data is displayed where in the card. A card necessarily consists of a title area. Additionally, you can add a body, an icon, and a badge to it.  
- Enter the following:   

  |  |  |
  |--|--|
  |**Title Column** | PRDT_INFO_NAME |
  |**Body Column** | PRDT_INFO_DESCR |
  |**Icon Initials Column** | PRDT_INFO_CATEGORY |
  |**Badge Column** | PRDT_INFO_LIST_PRICE |
  |  |  |

![](../../assets/Chapter-08/Cards_03.jpg)  

- Click **Run** and open your newly created page.  

![](../../assets/Chapter-08/Cards_04.jpg) 

You can see that the products are now displayed in the form of cards. The title of the card is the product name, the body briefly describes the product. The initials show the category of the product (e.g., AC for accessories), and in the badge, you see the price of the product.  

At the top of the page, there is a select list for choosing how the cards should be sorted. To adjust the displayed names of the sorting fields, switch to the page in Page Designer and navigate to the Page Item **P41_ORDER_BY**. On the right in the properties of the Page Item, open **Static Values** under **List of Values**. 

![](../../assets/Chapter-08/Cards_05.jpg) 

Here you can adjust the displayed sorting criteria under Display Value. Enter the following values from the left column here and confirm with **OK**.

  |  |  |
  |--|--|
  |Product Name | **PRDT_INFO_NAME** |
  |Product Description | **PRDT_INFO_DESCR** |
  |Product List Price | **PRDT_INFO_LIST_PRICE** |
  |  |  |

![](../../assets/Chapter-08/Cards_06.jpg)

- Click **Run** to view the change on the page.

![](../../assets/Chapter-08/Cards_07.jpg) 

## <a name="cards-mit-bild-erstellen"></a>8.3	Create Cards with Image

In this step, you will change the appearance of the cards and display the title images of the products.  
- Click on **Attributes** and then scroll down to **Media**.  

- Select **Source *BLOB Column*** and then under **BLOB_Column *PRDT_INFO_PRODUCT_IMAGE***. 

![](../../assets/Chapter-08/Cards_08.jpg)

- Also set ***PRDT_INFO_ID*** as **Primary Key Column 1**.  

![](../../assets/Chapter-08/Cards_09.jpg)

- Then access the page via the **Run** button.  

- The product images are now additionally displayed in the cards. 

![](../../assets/Chapter-08/Cards_10.jpg)