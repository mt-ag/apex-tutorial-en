# 15. Create Maps
In this task, you will create an application page with a world map. We obtain the necessary data via a REST Data Source presented in Chapter 13.2. The goal is to display all earthquakes that occurred worldwide in the last 24 hours on a map in APEX.

## 15.1. REST Data Source
To keep the earthquake data on the map up-to-date later, set up a REST Data Source now. You can look at the detailed steps of this subchapter again in Chapter 13.2 with screenshots if needed; the steps will therefore only be roughly described here.

To begin, create a new application in the App Builder and name it **Earthquakes**. You do not need to make any further settings. In the application overview, select **Shared Components**.

There, click on the option **REST Data Sources** under the category **Data Sources**.

Now click on the **Create** button, leave the selection at **From Scratch** in the pop-up window, and enter **EarthquakeData** as the name in the next step. Under URL Endpoint, insert the following URL: [https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson](https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson)

Now click continue until the window closes without changing anything, and the REST Data Source is created.

To update the data daily with a local table, you will now set up synchronization. Select the REST Data Source that you just created. Now click on the field shown in the image:

![](../../assets/Chapter-15/Karten_01.jpg)

Now change nothing except the name and type **EarthquakeData** in the **Table Name** field. After clicking **Save** to save, you will encounter the options shown in the image. Click on the highlighted field:

![](../../assets/Chapter-15/Karten_02.jpg)

This creates a table in which the data retrieved from the previously entered URL will be stored in the future. Now set the synchronization times of the data. To do this, click again on the fields marked in the next image:

![](../../assets/Chapter-15/Karten_03.jpg)

After clicking on the second field, a pop-up window opens where you can configure the synchronization. Since we want to refresh the data once a day, select **daily**. Fill the **Execution Hour** and **Execution Minute** fields with any time. After clicking on **Set Execution Interval**, click on the field **Save and Run**, which will fill the created table with data once. Now the table is updated daily.

The table, along with the current earthquake data, can now be found in the **Object Browser**.

## 15.2. Create the Map on a New Application Page
Make sure that you are now navigating to the application overview of the application you created at the beginning.

- There, select **Create Page**.

- Click on **Map** in the open pop-up window and then click on **Next**.

![](../../assets/Chapter-15/Karten_04.jpg)

- In the subsequent overview, enter any page name.
- Under **Local Database**, select **Table / View Name** and the table **EARTHQUAKEDATA** you just created.
- In the Navigation area, deactivate the *Breadcrumb* and click on **Next**.

![](../../assets/Chapter-15/Karten_05.jpg)

In the next overview, you can choose between different display options for how the locations should be represented.
- Since you are creating an overview of earthquakes, do not select **Points**, which would only mark the locations of the earthquakes, but select **Heat Map** to later recognize the location and get an impression of the extent on the map.

- Now you only need to change the field **Geometry-Column** from the selection options shown there. Select the column **Geometry**.

![](../../assets/Chapter-15/Karten_06.jpg)

After clicking **Create Page**, you can start the application and navigate to the created page.

There you will see all saved earthquakes and get an impression of their extent.

![](../../assets/Chapter-15/Karten_07.jpg)