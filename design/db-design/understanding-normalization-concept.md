# Understanding normalization concept

{% hint style="success" %}
**Database normalization** is the process of structuring a relational database in accordance with a series of so-called normal forms in order to reduce data redundancy and improve data integrity.
{% endhint %}

Normalization entails organizing the columns \(attributes\) and tables \(relations\) of a database to ensure that their dependencies are properly enforced by database integrity constraints.

### Side effects

**Side-effects** may arise in relations that have not been sufficiently normalized:

* **Update anomaly** \(change may need to be applied to multiple records; if update partially successful – data inconsistency appears\)

![](../../.gitbook/assets/update-anomaly.png)

* **Insertion anomaly** \(all attributes should be filled during insertion; if not – data integrity compromised\)

![](../../.gitbook/assets/insert-anomaly.png)

* **Deletion anomaly** \(deletion of data representing certain facts necessitates deletion of data representing completely different facts\)

![](../../.gitbook/assets/delete-anomaly.png)

### Normalization Forms

#### **UNF - Unnormalized form**

![](../../.gitbook/assets/nf-0.png)

#### **1NF - First normal form**

* Each sell to be Single valued
* Entries in a column are same type
* Rows uniquely identified \(add Unique ID or add more columns to make unique\)

![](../../.gitbook/assets/nf-1.png)

#### **2NF - Second normal form**

* 1st normal form
* All attributes \(Non-Key Columns\) dependent on the key

![](../../.gitbook/assets/nf-2.png)

#### **3NF - Third normal form**

* 2nd normal form
* All fields \(columns\) can be determined Only by the Key in the table and no other column

![](../../.gitbook/assets/nf-3.png)

#### **4NF - Fourth normal form**

* 3rd normal form
* No multi-valued dependencies

![](../../.gitbook/assets/nf-4.png)

