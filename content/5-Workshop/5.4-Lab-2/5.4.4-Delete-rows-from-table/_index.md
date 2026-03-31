---
title : "2.4 Delete rows from table"
date : 2026-03-25
weight : 4
chapter : false
pre : " <b> 5.4.4 </b> "
---

We will now remove some records from the table and later retrieve the deleted data using an Iceberg table Snapshot.

1.  Delete all rows where product\_category = 'Software'. Paste the query below into the query editor and click **Run**.

```sql
delete from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software'
```

![delete-rows](/images/5-Workshops/5.4/5.4.4/21.png)

---

2.  Run the query below to confirm the rows were deleted — you should get zero results. Paste the query into the editor and click **Run**.

```sql
Select * from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software'
```
![delete-rows](/images/5-Workshops/5.4/5.4.4/22.png)
