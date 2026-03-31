---
title : "2.3 Time travel and version travel queries"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

1.  Let's retrieve the snapshot history of the Iceberg table using the query below. Paste it into the query editor and click **Run**. Copy the older **snapshot_id** value — you will need it in the next step.

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg$history"
```

![snapshot-timetravel](/images/5-Workshops/5.4/5.4.3/20.png)

---

2.  Now query the snapshot from before we added the `comment` column. Paste the query below into the editor, replace the `snapshot_id` placeholder with the older value you copied, then click **Run**.

After running the query, confirm that the results do not include the `comment` column.

```sql
select * from iceberg_database.amazon_reviews_iceberg FOR VERSION AS OF  <<replace snapshot_id>>
where marketplace ='UK'
```

![retrive-snapshot](/images/5-Workshops/5.4/5.4.3/21.png)

---

3.  We can also use the `made_current_at` timestamp to query a specific snapshot. Paste the query below into the editor, replace the `made_current_at time` placeholder with the actual timestamp value, then click **Run**.

**Alternatively**, you can use the `made_current_at` **column** value directly for timestamp-based access.

```sql
select * from iceberg_database.amazon_reviews_iceberg for TIMESTAMP AS OF TIMESTAMP '<<replace with made_current_at time>>' 
where marketplace ='UK'
```



