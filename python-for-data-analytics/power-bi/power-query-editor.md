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

**Home Menu  ----->  Remove Rows -----> Remove Top Rows -----> Enter Number of Rows -----> OK**



<figure><img src="../../.gitbook/assets/Remove row.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Select row no.png" alt=""><figcaption></figcaption></figure>



3. Create First Line as Header" means converting the first row of data into column names so that Power BI can identify each column correctly.

<p align="center"><strong>Home Menu -----> Use First Row as Header</strong></p>

<figure><img src="../../.gitbook/assets/First row as header.png" alt=""><figcaption></figcaption></figure>



4. In Power Query Editor, we first clean the data by removing blanks, spaces, and invalid values, then change the data type from Text (String) to Whole Number (Integer) to ensure accurate calculations and analysis.

**Select the Column -----> Right-click on the selected Column -----> Replace Values ----->Enter the character to change -----> Change with Blank Space**

<figure><img src="../../.gitbook/assets/Replace Values.png" alt=""><figcaption></figcaption></figure>



* It is used to clean unwanted text such as  ?,  "N/A",  "-",  or  "Unknown" before changing the data type. After cleaning, the column can be safely converted from **Text (String)** to **Decimal Numbers (Integer)** without errors.

<figure><img src="../../.gitbook/assets/Replace - value.png" alt=""><figcaption></figcaption></figure>

<p align="center"><strong>Select Column -----> Select Decimal Numbers</strong></p>

<figure><img src="../../.gitbook/assets/Change data type.png" alt=""><figcaption></figcaption></figure>



* **Data type changed from Text (String) to Decimal Numbers (Integer).**

<figure><img src="../../.gitbook/assets/intger Data type.png" alt=""><figcaption></figcaption></figure>



*   Sometimes the date and time format in the source data or in Power BI differs from the date and time format of the computer system (regional settings). In such cases, we change the date and time format in Power BI to match the system's date and time format, ensuring the data is displayed and interpreted correctly.\
    \
    **Example:**-

    **System Date Format:** DD/MM/YYYY

    * Example: 12/06/2026



    **Power BI Date Format:** MM/DD/YYYY

    * Example: 06/12/2026

    To avoid confusion and incorrect date interpretation, we change the Power BI date format to match the system format.

<figure><img src="../../.gitbook/assets/Type of data.png" alt=""><figcaption></figcaption></figure>

We can't change the Date type directly; it shows an error.

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-12 134442.png" alt=""><figcaption></figcaption></figure>

When a date column is not recognized correctly because of a different date format (for example, Power BI reads 06/12/2026 as June 12 instead of 6 December), we can create a new column and convert the values into the correct date format. This helps Power BI interpret and analyze the data accurately.

<figure><img src="../../.gitbook/assets/Custom Column.png" alt=""><figcaption></figcaption></figure>

#### There are two ways to add a Date :

1. In Power Query Editor, a Custom Column can be used to combine Day, Month, and Year columns into a single date field. The Number.ToText() function converts numeric values into text, and the **&** operator concatenates them with separators such as **"-"**. This creates a complete date string, which can then be converted into a Date data type for accurate reporting and analysis in Power BI.



* **Number.ToText()** = Converts a numeric value into text.



* **&** = The concatenation operator in Power Query. Only used to join text values together.



**Note:** The **&** operator can only join text values. Since Day Number, Month Number, and Year are numeric columns, they must first be converted to text.

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-12 140605.png" alt=""><figcaption></figcaption></figure>



2. In Power Query Editor, the "Date.FromText()" function is used to convert text-based date values into a valid Date data type. The format parameter specifies how the text should be interpreted, ensuring that dates are correctly recognized regardless of system or regional settings. This helps Power BI perform accurate date calculations, filtering, sorting, and time-based analysis.



* **Date.FromText()** = Converts text into a Date value.



* **\[Date]** = Column name that has to change (select from the file).



* **\[Format="M/d/yyyy"]** = Tells Power BI how to read the date.



<figure><img src="../../.gitbook/assets/Screenshot 2026-06-12 142944.png" alt=""><figcaption></figcaption></figure>





11. **Close & Apply** is an option in Power Query Editor that saves all the data transformations and loads the transformed data into Power BI for reporting and analysis. Close & Apply is used in the Power Query Editor to save all data transformation steps and load the transformed data into the Power BI data model for further analysis and report creation.

#### What Happens When You Click Close & Apply?

* All cleaning and transformation steps are saved.
* The transformed data is loaded into the Power BI data model.



<p align="center"><strong>Click on the Close &#x26; Apply option -------> Load the Data in Power BI.</strong></p>

<figure><img src="../../.gitbook/assets/Load data in BI.png" alt=""><figcaption></figcaption></figure>

