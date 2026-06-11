# Power Query Editor

Power Query Editor is a tool in Power BI used to clean, transform, and prepare data before loading it into Power B&#x49;**.** In this place, we fix, clean, and organize data before creating reports and dashboards.

#### What Can We Do in the Power Query Editor?

* Create headers
* Delete rows and columns
* Remove duplicate rows
* Rename columns
* Change data types
* Filter rows
* Split or merge columns
* Replace values
* Handle missing data

<figure><img src="../../.gitbook/assets/P_qwery.png" alt=""><figcaption></figcaption></figure>

### Change Data Type and Data Clearing & Filtration&#x20;

Clearing data means removing unnecessary rows, columns, or errors from the dataset to make it clean and ready for analysis.



1. **Common data cleaning tasks:**

* Remove unwanted columns.
* Remove blank rows.
* Remove duplicate records.
* Replace or remove errors.
* Change incorrect data types.
* Rename columns for better understanding.

<figure><img src="../../.gitbook/assets/Column_Name error.png" alt=""><figcaption></figcaption></figure>



2. To remove the rows, select Remove Top Rows from the Home menu.

Home Menu  ----->  Remove Rows -----> Remove Top Rows -----> Enter Number of Rows -----> OK



<figure><img src="../../.gitbook/assets/Remove row.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Select row no.png" alt=""><figcaption></figcaption></figure>



3. Create First Line as Header" means converting the first row of data into column names so that Power BI can identify each column correctly.

<p align="center">Home Menu -----> Use First Row as Header</p>

<figure><img src="../../.gitbook/assets/First row as header.png" alt=""><figcaption></figcaption></figure>



4. In Power Query Editor, we first clean the data by removing blanks, spaces, and invalid values, then change the data type from Text (String) to Whole Number (Integer) to ensure accurate calculations and analysis.

Select the Column -----> Right-click on the selected Column -----> Replace Values ----->Enter the character to change -----> Change with Blank Space

<figure><img src="../../.gitbook/assets/Replace Values.png" alt=""><figcaption></figcaption></figure>



* It is used to clean unwanted text such as  ?,  "N/A",  "-",  or  "Unknown" before changing the data type. After cleaning, the column can be safely converted from **Text (String)** to **Decimal Numbers (Integer)** without errors.

<figure><img src="../../.gitbook/assets/Replace - value.png" alt=""><figcaption></figcaption></figure>

<p align="center">Select Column -----> Select Decimal Numbers</p>

<figure><img src="../../.gitbook/assets/Change data type.png" alt=""><figcaption></figcaption></figure>



* Data type changed from Text (String) to Decimal Numbers (Integer).

<figure><img src="../../.gitbook/assets/intger Data type.png" alt=""><figcaption></figcaption></figure>























11. **Close & Apply** is an option in Power Query Editor that saves all the data transformations and loads the transformed data into Power BI for reporting and analysis. Close & Apply is used in the Power Query Editor to save all data transformation steps and load the transformed data into the Power BI data model for further analysis and report creation.

#### What Happens When You Click Close & Apply?

* All cleaning and transformation steps are saved.
* The transformed data is loaded into the Power BI data model.



<p align="center">Click on the Close &#x26; Apply option -------> Load the Data in Power BI</p>

<figure><img src="../../.gitbook/assets/Load data in BI.png" alt=""><figcaption></figcaption></figure>

