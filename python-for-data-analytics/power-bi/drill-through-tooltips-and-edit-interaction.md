# Drill Through, Tooltips,  and Edit Interaction

### 1. Drill Through

**Drill Through** is a Power BI feature that allows users to **go from a summary report to a detailed report** by clicking on a specific data item.

In simple words, it helps you **see detailed information about one selected record** without creating a new report.

#### Benefits

* Shows detailed information.
* Makes reports interactive.
* Helps analyze specific records.
* To reduce the number of steps in page navigation.

#### Example

Suppose you have:

* **Page 1:** Sales Dashboard
* **Page 2:** Product Dashboard (Drill Through Page)

<figure><img src="../../.gitbook/assets/Drill Through (1).png" alt=""><figcaption></figcaption></figure>



* We can drag any data into the Drill Through field. It depends on which data we want to filter out on the 2nd Page, according to the 1st Page data visuals.

<figure><img src="../../.gitbook/assets/Drill_1.png" alt=""><figcaption></figcaption></figure>



* When you right-click on the **Line chart visual** for the year on Page 1, Power BI opens a tab of the **Drill Through** option, which redirects us to Page 2 and displays only the selected **Drill Through detailed data.**

<figure><img src="../../.gitbook/assets/Drill_2.png" alt=""><figcaption></figcaption></figure>



* Drill through automatically creates a **Back Button** over the page where the Drill through is created.
* And according to the 1st Page Drill Through selection, it filters out the **entire** **2nd Page data visuals**.

<figure><img src="../../.gitbook/assets/Drill_3.png" alt=""><figcaption></figcaption></figure>

## How Drill Through Works Internally

<p align="center">User Clicks Data Point<br>↓<br>Right-click on Visual<br>↓<br>Choose Drill Through<br>↓<br>Power BI Reads Selected Value<br>(Fiscal Year = 2014)<br>↓<br>Passes Filter to Drill Through Page<br>↓<br>Detail Page Opens<br>↓<br>Only Matching Records Are Displayed</p>

<p align="center"></p>

## 2. Tooltips

A **Tooltip** is a small information box that appears when you **move the mouse pointer over a visual**.

It provides additional details without taking extra space on the report page.

#### Benefits

* Displays extra information.
* Keeps reports clean.
* Improves user experience.







## 3. Edit Interaction

**Edit Interaction** is a feature in **Power BI** that controls **how one visual affects another visual** on the same report page.

Edit Interaction allows you to decide whether clicking one chart should filter, highlight, or have no effect on other charts in the report.









































