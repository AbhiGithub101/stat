# Report View, Table View and Model View

In **Power BI Desktop**, there are **3 main views**:

* [ ] Report View
* [ ] Table View or Data View
* [ ] Model View

Here we understand the Power BI views in a descriptive way, what they are, and how they work....

To understand better way we start from Model view.





### Model View :

**Model View** shows the relationships between different tables in the Power BI data model.

#### Purpose

* Create relationships between tables.
* Manage star and snowflake schemas.
* Define cardinality (One-to-Many, Many-to-One).
* Improve data modeling and report performance.

<figure><img src="../../.gitbook/assets/Model_vv.jpg" alt=""><figcaption></figcaption></figure>

&#x20;&#x20;

&#x20;      After Data loaded in Power BI, it automatically creates some relations within tables. But we have to check manually whether the weather relations are connected with same type or not. Also we can **DELETE** the relations manually.

We can also **Create** realation between the tables manually. It can be added by 2 types:

* By Drag and Drop
* Manage Relationships option



1. **Drag and Drop** is a method of creating relationships between tables in **Model View** by dragging a common column from one table and dropping it onto the matching column in another table.

* Quickly create relationships between tables.
* Connect Fact and Dimension tables.
* Enable data filtering and analysis across multiple tables.

<figure><img src="../../.gitbook/assets/Drag and Drop.png" alt=""><figcaption></figcaption></figure>

#### Example

Suppose you have:

**Sales Table**

* Customer\_ID
* Product\_ID
* Sales\_Amount

**Customer Table**

* Customer\_ID
* Customer\_Name

You can drag **Customer\_ID** from the Sales table and drop it onto **Customer\_ID** in the Customer table to create a relationship.

<figure><img src="../../.gitbook/assets/DD_pb.png" alt=""><figcaption></figcaption></figure>



2. **Manage Relationships** is a feature in Power BI that allows users to create, edit, delete, and view relationships between tables manually.

* Create relationships when Power BI does not detect them automatically.
* Modify existing relationships.
* Set Cardinality (One-to-One, One-to-Many, Many-to-One).
* Configure Cross Filter Direction.
* Manage the data model effectively.

<figure><img src="../../.gitbook/assets/Manage_Rel.png" alt=""><figcaption></figcaption></figure>



<p align="center"><strong>Click on Manage Relationships ------> Select New Relationships</strong></p>

<figure><img src="../../.gitbook/assets/NR_relation.png" alt=""><figcaption></figcaption></figure>



&#x20;    This image shows the Edit Relationship window in Power BI where the FactSale table is connected to the DimDate table using the Invoice Date and Date columns. The relationship has a Many-to-One (\*:1) cardinality because many sales transactions can occur on a single date. The Cross Filter Direction is set to Single, allowing filters to flow from the Date table to the Sales table. This relationship enables date-based analysis such as monthly, quarterly, and yearly sales reporting.

<figure><img src="../../.gitbook/assets/Edit_relation.png" alt=""><figcaption></figcaption></figure>

**Note:** In the above sheet DimDate will be join with FactSale table with Left Join.

























































































