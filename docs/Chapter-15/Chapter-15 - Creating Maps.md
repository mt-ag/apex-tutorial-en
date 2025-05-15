# <a name="creating-maps"></a>15. Creating Maps
In this task, you will create an application page with a world map. The necessary data will be obtained through a REST Data Source introduced in Chapter 13.2. The goal is to display all earthquakes that occurred worldwide in the last 24 hours on a map in APEX.

## <a name="maps-rest-data-source"></a>15.1 REST Data Source
To keep the earthquake data on the map up to date later, you need to set up a REST Data Source. If needed, you can review the detailed steps of this subchapter with screenshots in Chapter 13.2; therefore, the steps will be described only roughly below.

First, create a new application in the App Builder and name it **Earthquakes**. No further settings are required. Then, in the application overview, select **Shared Components**.

Once there, click the **REST Data Sources** option under the **Data Sources** category.

Now click the **Create** button, leave the selection as **From Scratch** in the pop-up window, and enter **EarthquakeData** as the name in the next step. Under URL Endpoint, insert the following URL: [https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson](https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson)

Now click on next without changing anything until the window closes and the REST Data Source is created.

To ensure the data is updated daily with a local table, you will now set up a synchronization. Select the REST Data Source you just created. Now click on the field shown in the image:

![](../../assets/Chapter-15/Karten_01.jpg)

Now change nothing except the name and type **EarthquakeData** into the **Table Name** field. After clicking **Save** to save, you will encounter the options shown in the image. Click on the highlighted field:

![](../../assets/Chapter-15/Karten_02.jpg)

This way, you have created a table into which the data retrieved from the previously entered URL will be saved in the future. Now set the synchronization times for the data. To do this, click again on the fields marked in the next image:

![](../../assets/Chapter-15/Karten_03.jpg)

After clicking on the second field, a pop-up window opens where you can configure the synchronization. Since we want to refresh the data once a day, select **daily**. Fill in the **Execution Hour** and **Execution Minute** fields with any time. After clicking **Set Execution Interval**, click the **Save and Run** field, which will fill the created table with data once. Now the table will be updated daily.

The table with the current earthquake data can now be found in the **Object Browser**.

## <a name="creating-the-map-on-a-new-application-page"></a>15.2 Creating the Map on a New Application Page
Ensure you are now navigating to the application overview of the application you created at the beginning.

- There, select **Create Page**.

- Click on **Map** in the opened pop-up window and then click **Next**.

![](../../assets/Chapter-15/Karten_04.jpg)

- In the overview shown, enter any page name.  
- Under **Local Database**, select the newly created table **EARTHQUAKEDATA** under **Table / View Name**.  
- Disable the *Breadcrumb* in the Navigation section and click **Next**.

![](../../assets/Chapter-15/Karten_05.jpg)  

In the next overview, you can choose between different display options for how the locations should be represented.
- Since you are creating an overview of earthquakes, do not select **Points**, which would only mark the locations of the earthquakes, but select **Heat Map** to recognize the location and get an impression of the magnitude on the map later.

- Now you only need to change the **Geometry-Column** field from the options displayed. Select the **Geometry** column there.

![](../../assets/Chapter-15/Karten_06.jpg)

After clicking on **Create Page**, you can start the application and navigate to the created page.

There you will see all saved earthquakes and get an impression of their magnitude.

![](../../assets/Chapter-15/Karten_07.jpg)