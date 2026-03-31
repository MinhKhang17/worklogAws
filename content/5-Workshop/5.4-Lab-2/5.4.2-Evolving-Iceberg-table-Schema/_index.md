---
title : "2.2 Evolving Iceberg table schema"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

Schema updates in Iceberg are metadata-only operations. No data files are modified when a schema change is applied.

The Iceberg format supports the following types of schema evolution:

-   Add – Adds a new column to a table or to a nested struct.
-   Drop – Removes an existing column from a table or nested struct.
-   Rename – Renames an existing column or a field in a nested struct.
-   Reorder – Changes the ordering of columns.
-   Type promotion – Widens the data type of a column, struct field, map key, map value, or list element. The following type promotions are currently supported for Iceberg tables: \* integer to big integer \* float to double \* increasing the precision of a decimal type

---

1.  In this step, we will add a new column to the Iceberg table we just created. Specifically, we will add a `comment` column.

Paste the query below into the query editor and click **Run**

```sql
ALTER TABLE iceberg_database.amazon_reviews_iceberg ADD COLUMNS (comment string)
```

![add-column](/images/5-Workshops/5.4/5.4.2/17.png)

---

2.  We will set the value of the `comment` column to `High rated` for all rows that have a rating of 4 or higher. Paste the query below into the query editor and click **Run**

```sql
UPDATE iceberg_database.amazon_reviews_iceberg
SET comment = 'High rated'
Where star_rating >=4;
```

This query may take a few minutes to complete.

![update-column](/images/5-Workshops/5.4/5.4.2/18.png)

---

3.  Verify the column was added successfully by querying the table. Paste the query below into the query editor and click **Run**

```sql
SELECT * FROM iceberg_database.amazon_reviews_iceberg
Where star_rating >=4 limit 10
```

Scroll the results panel to the right to see the new `comment` column and its values.

![add-column](/images/5-Workshops/5.4/5.4.2/19.png)

