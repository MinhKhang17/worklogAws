---
title : "2.1 Creating Iceberg tables"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---


1.  To create Database, copy paste below code in query editor and click on **Run**. You need to be in Athena Query Editor to run below commands.

```sql
create database iceberg_database;
```

![create-iceberg-db](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/create-iceberg-db.png)

---

2.  To create Iceberg table, copy paste below code in query editor, replace the `<<update-s3-bucket>>` with S3 bucket created in **Create S3 bucket** prerequisites and click on **Run** .

In the table property we have specified, 'write\_target\_data\_file\_size\_bytes'='536870912' this property is to specify the target size in bytes of the files produced by Athena. In this example the target file size is 512MB.

```sql
CREATE TABLE iceberg_database.amazon_reviews_iceberg(
marketplace string,
customer_id string,
review_id string,
product_category string,
product_id string,
product_parent string,
product_title string,
star_rating int,
helpful_votes int,
total_votes int,
vine string,
verified_purchase string,
review_headline string,
review_body string,
review_date bigint)
LOCATION 's3://<<update-s3-bucket>>/amazon_reviews_iceberg/'
TBLPROPERTIES (
'table_type'='ICEBERG',
'format'='parquet',
'write_target_data_file_size_bytes'='536870912'
)
```

![Create-iceberg-table](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/Create-iceberg-table.png)

---

3.  insert data into `iceberg_database.amazon_reviews_iceberg` from `amazon_reviews_parquet`

Copy Paste below query into editor and click on **Run** . (We are loading only a couple of Product Categories for sake of faster loading.)

This step may take upto 1 mins to complete.

```sql
insert into iceberg_database.amazon_reviews_iceberg
select *
from default.amazon_reviews_parquet
where product_category in ('Gift_Card', 'Apparel','Software')
```

![insert-into-iceberg-table](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/insert-into-iceberg-table.png)

---

4.  Verify data is loaded by querying the table. Copy paste below code in query editor and click on **Run**

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg" limit 10;
```

![iceberg-test-query](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/iceberg-test-query.png)

---

**Congratulation you have create Athena Iceberg table! Now let's explore some of key Athena Iceberg features.**

