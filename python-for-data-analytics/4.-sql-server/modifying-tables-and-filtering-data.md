---
hidden: true
---

# Modifying Tables and Filtering Data

**Once a table is created, you don't have to live with its structure forever. SQL gives you the power to modify existing tables , add columns, remove columns, change data types, and rename columns.**

The command we use for all of these modifications is **ALTER TABLE**

{% stepper %}
{% step %}
### 1. Adding a New Column

Let's say we realize that we forgot to include a Salary column in the Employee table. We need to add it now.

Here's how you add a new column to an existing table:

```sql
ALTER TABLE Employee
ADD Salary DECIMAL(10, 2);
```

Let's break it down:

•  ALTER TABLE Employee -> we are modifying the Employee table

•  ADD Salary DECIMAL(10, 2) -> we are adding a new column called Salary with data type       DECIMAL(10,2)
{% endstep %}

{% step %}
###


{% endstep %}
{% endstepper %}
