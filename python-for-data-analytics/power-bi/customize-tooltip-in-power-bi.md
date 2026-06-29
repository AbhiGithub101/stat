# Customize Tooltip in Power BI

## Customize Tooltip&#x20;

**Customize Tooltip** is a feature in **Power BI** that allows you to create a **custom tooltip page** with additional visuals and information. When a user **hovers the mouse over a data point**, the custom tooltip appears and shows more details than the default tooltip.

### Why Use Customize Tooltip?

* Displays more information without opening another page.
* Makes reports more interactive.
* Saves report space.
* Improves user experience.
* Helps users understand data quickly.

<figure><img src="../../.gitbook/assets/Tool_2.png" alt=""><figcaption></figcaption></figure>



#### How to Create Customize Tooltip?



* Create a new page, and go to **Format Page**, then on **Page Information.**

<figure><img src="../../.gitbook/assets/Cus_Tool6.png" alt=""><figcaption></figcaption></figure>



* Click on **ON** option on **Allow use as tooltip**, a new tooltip page open on page.

<figure><img src="../../.gitbook/assets/Cus_Tool7.png" alt=""><figcaption></figcaption></figure>



* On Visualization page, go to Build Visual and select **Table Chart**.

<figure><img src="../../.gitbook/assets/Cus_Tool8.png" alt=""><figcaption></figcaption></figure>



* Drag the values from Data to Chart Visual, like Total Including Tax and Profit from **Fact Sales.**&#x20;

<figure><img src="../../.gitbook/assets/Cus_Tool9.png" alt=""><figcaption></figcaption></figure>



* Add another chart, which is a Cluster Bar Chart. Drag the values from Data to Chart Visual, like Total Including Tax and Profit from **Fact Sales.**&#x41;nd from **Dim Date,** select **Fiscal Year.**

<figure><img src="../../.gitbook/assets/Cus_Tool10.png" alt=""><figcaption></figcaption></figure>



* Then go to the **Sales Dashboard Pag**e, select any visuals to connect with the **Customioze Tooltip**.

<p align="center">Go to Visualization -----> Format Visual -----> <strong>ON</strong> Tooltips -----> Go to <strong>Options Type</strong></p>

<figure><img src="../../.gitbook/assets/Cus_Tool1.png" alt=""><figcaption></figcaption></figure>



<p align="center">Go to <strong>Options Type ------></strong> Select <strong>Report page</strong> in <strong>Type</strong></p>

<figure><img src="../../.gitbook/assets/Cus_Tool2.png" alt=""><figcaption></figcaption></figure>



<p align="center">In <strong>Options</strong> -----> <strong>Page</strong> ----->Select Created <strong>Tooltip page</strong></p>

<figure><img src="../../.gitbook/assets/Cus_Tool3.png" alt=""><figcaption></figcaption></figure>



* **Hover** over the **Line Chart**, **Customized Tooltip** appers over the chart contins with details.

<figure><img src="../../.gitbook/assets/Tool_2.png" alt=""><figcaption></figcaption></figure>



* We can create multiple duplicate tooltip pages to connect with more visuals in the **Sales dashboard Page**.

Create a duplicate page of Custamize Tooltip -----> Select different Chart Visual -----> Go to Visualization -----> Select Format Visual -----> **ON** the Tooltip option -----> Go to **Options Type        ------>** Select **Report page** in **Type -----> Page** ----->Select the **Duplicate Tooltip page**

<figure><img src="../../.gitbook/assets/Cus_Tool4.png" alt=""><figcaption></figcaption></figure>



* Same as Above.

<figure><img src="../../.gitbook/assets/Cus_Tool5.png" alt=""><figcaption></figcaption></figure>



## How the Customize Tooltip Works Internally

<p align="center">Create New Page<br>↓<br>Select Line Chart<br>(Revenue, Sum of Profit and Sum of Quantity by Fiscal Year)<br>↓<br>Go to Visualisation Option<br>↓<br>Search for Tooltip Option<br>↓<br>Drag the values from Data<br>(Profit and Quantity)<br>↓<br>Hover on "Line Chart"<br>↓<br>Power BI Detects<br>(Profit and Quantity)<br>↓<br>Reads Sales Data<br>↓<br>Applies Current Filters<br>↓<br>Shows Tooltip</p>

