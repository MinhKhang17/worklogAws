---
title : "2.5 Recovering deleted data from an Iceberg table snapshot"
date : 2026-03-25
weight : 5
chapter : false
pre : " <b> 5.4.5 </b> "
---

1.  Retrieve the snapshot history of the Iceberg table using the query below. Paste it into the editor and click **Run**.

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg$history"
```

![retrive-rows](/images/5-Workshops/5.4/5.4.5/23.png)

---

2.  Use the query below to retrieve deleted rows from a specific snapshot and re-insert them into the main table. Update the `<<Enter Snapshot ID>>` placeholder with the appropriate Snapshot ID before running. Paste the query into the editor and click **Run**.

```sql
insert into iceberg_database.amazon_reviews_iceberg
select * from iceberg_database.amazon_reviews_iceberg FOR VERSION AS OF  <<Enter Snapshot ID>>
where product_category = 'Software' limit 10
```

![retrive-rows](/images/5-Workshops/5.4/5.4.5/24.png)

---

3.  Query the main table to verify that the deleted rows have been successfully restored. Paste the query below into the editor and click **Run**.

```sql
Select * from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software' limit 10
```

![rows-retrived](/images/5-Workshops/5.4/5.4.5/25.png)


