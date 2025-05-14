# <a name="karten-erstellen"></a>15. Creating Maps 
In this task, you will create an application page with a world map. We will obtain the necessary data via a REST Data Source (introduced in Chapter 13.2). The goal is to display all the earthquakes on Earth that occurred within the last 24 hours on a map in APEX.

## <a name="karten-rest-data-source"></a>15.1	REST Data Source 
To keep the earthquake data on the map up-to-date later, you will now set up a REST Data Source. You can review the detailed steps of this subchapter with screenshots in Chapter 13.2 if needed; the steps are only roughly described below.

To begin, create a new application in the App Builder and name it **Earthquakes**. No further settings are necessary. In the application overview, select **Shared Components**.

Once there, click on the option **REST Data Sources** under the category **Data Sources**.

Now click on the **Create** button; in the pop-up window, leave the selection at **From Scratch** and enter **EarthquakeData** as the name in the next step. Under URL Endpoint, insert the following URL: [https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson](https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson)  

Now, keep clicking next without changing anything until the window closes and the REST Data Source is created. 

To update the data daily with a local table, you will now set up synchronization. Select the REST Data Source you just created. Click on the field shown in the picture:

![](../../assets/Chapter-15/Karten_01.jpg)

Now change nothing except the name and enter **EarthquakeData** in the **Table Name** field. After clicking **Save**, you will encounter the options shown in the picture. 
Click on the highlighted field: 

![](../../assets/Chapter-15/Karten_02.jpg)

By doing this, you have now created a table where the data retrieved from the previously entered URL will be stored in the future. Now set the data synchronization times. Click again on the fields marked in the next picture:

![](../../assets/Chapter-15/Karten_03.jpg)

After clicking on the second field, a pop-up window opens where you can now configure the synchronization. Since we want to refresh the data once every day, select **daily**. Fill in the **Execution Hour** and **Execution Minute** fields with any time of your choice. After clicking **Set Execution Interval**, click the **Save and Run** field, which will fill the created table with data once. Now the table will be updated daily.  

The table along with the current earthquake data can now be found in the **Object Browser**.  

## <a name="erstellen-der-karte-auf-einer-neuen-anwendungsseite"></a>15.2	Creating the Map on a New Application Page
Make sure you are now navigating to the application overview of the application you created at the beginning.  

- There, select **Create Page**.  

- Click on **Map** in the open pop-up window and then on **Next**.  
  
![](../../assets/Chapter-15/Karten_04.jpg)  

- In the overview displayed subsequently, enter any page name.  
- Under **Local Database**, select the recently created table **EARTHQUAKEDATA** under **Table / View Name**.  
- Deactivate the *Breadcrumb* in the Navigation section and click **Next**.   

![](../../assets/Chapter-15/Karten_05.jpg)  

In the next overview, you can choose between different display options for how the locations should be represented.  
- Since you are creating an overview of earthquakes, select **Heat Map** instead of **Points**, which would only mark the locations of the earthquakes, to see the location and get a certain impression of the magnitude on the map later. 

- Now, only change the **Geometry-Column** field from the displayed options. Select the **Geometry** column there.  

![](../../assets/Chapter-15/Karten_06.jpg) 

After clicking **Create Page**, you can start the application and navigate to the created page.

There, you will now see all the stored earthquakes and get an impression of their magnitude.

![](../../assets/Chapter-15/Karten_07.jpg)