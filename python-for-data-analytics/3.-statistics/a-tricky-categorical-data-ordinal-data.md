# A Tricky Categorical Data - Ordinal Data

### **Tricky Categorical Data – Ordinal Data**

Not all data is about exact numbers. Sometimes we have **categories** like _Poor_, _Average_, _Good_, _Excellent_. These are **categorical data**, but some of them are tricky because they have an **order**. That’s what makes them **ordinal data**.

***

#### **What is Ordinal Data?**

**Ordinal data** means:

* Categories have a **natural order**.
* The **distance between categories may or may not be equal**.

Example:

* Poor → Fair → Good → Excellent

You can say _Excellent > Good > Fair > Poor_, but you **cannot always measure exactly how much better** one is than another.

***

#### **When Ordinal Data Should Stay Ordinal**

Keep it purely ordinal when:

* Intervals between categories are **unknown or unequal**.
* Categories are **subjective or opinion-based**.

Examples:

* Satisfaction: Very Unsatisfied, Unsatisfied, Neutral, Satisfied, Very Satisfied
* Product ratings: ★, ★★, ★★★, ★★★★, ★★★★★

Here, using averages or numeric calculations would **mislead you**, because the gap between levels is not guaranteed to be equal.

***

#### **When Ordinal Data Can Be Treated as Numerical**

Sometimes, ordinal data comes from **measured ranges that are approximately equal**.\
In such cases, you can treat it as **numeric**.

Example: Grades based on marks:

| Grade | Marks Range | Width |
| ----- | ----------- | ----- |
| A     | 90–100      | 11    |
| B     | 80–89       | 10    |
| C     | 70–79       | 10    |
| D     | 60–69       | 10    |
| F     | <60         | —     |

* Here, the intervals are **roughly equal**, so assigning numbers (A=5, B=4, C=3, D=2, F=1) is acceptable.
* You can calculate **mean, correlation, or regression** using these numbers.

⚠️ If intervals were **very unequal** (e.g., Poor = 0–20, Fair = 21–40, Good = 41–100), numeric treatment would **distort the results**.

***

#### **Quick Summary Table**

| Case                              | Can Treat as Numerical? | Reason                     |
| --------------------------------- | ----------------------- | -------------------------- |
| Intervals roughly equal           | ✅ Yes                   | Differences are meaningful |
| Intervals unknown or very unequal | ❌ No                    | Only the order matters     |

***

#### **Key Takeaways**

1. Ordinal data = order matters, exact difference may not.
2. Keep it ordinal when differences are unknown.
3. Treat it as numeric when intervals are approximately equal.
4. Misusing numeric operations on purely ordinal data **can give wrong conclusions**.
