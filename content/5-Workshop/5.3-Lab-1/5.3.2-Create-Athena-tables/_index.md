---
title : "1.2 Create Athena tables"
date : 2026-03-25 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

1.  Navigate to [Athena Console](https://console.aws.amazon.com/athena/home) 
    
    ---
    
2.  Open the Query Editor (not Notebook editor)
    
    ---
    
3.  Once in the Athena console Query editor, click on '**Edit Settings**' as shown below:
    

![Athena console](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/athena_save_qry_result.png)

---

1.  Click on Settings and then click **Manage**

![Athena Settings](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/athena_save_qry_result_manage.png)

---

4.  Under Manage Settings, click on **Browse S3**.

![Athena Settings](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/athena_save_qry_result_manage_settings.png)

---

5.  Choose the S3 bucket by clicking on the radio button and then click **Choose**. For self paced labs, choose the S3 bucket created previously. For AWS Events, choose the S3 bucket with the title iceberg-workshop-ACCOUNTID (for example: iceberg-workshop-123456789)

![Choose-S3-data-set](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/Choose-S3-data-set.png)

---

6.  Click on **Save** to save the S3 location

![Save-s3-location](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/Save-s3-location.png)

---

7.  Click on **Editor** and copy paste below query. Update **YOURBUCKET** with your S3 bucket name then click on Run.

```sql
CREATE EXTERNAL TABLE default.amazon_reviews_parquet(
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
ROW FORMAT SERDE 
'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe' 
STORED AS INPUTFORMAT 
'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat' 
OUTPUTFORMAT 
'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
's3://YOURBUCKET/productreviews/'; 
```

![Run-athena-create-table](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/Run-athena-create-table.png)

---

8.  Copy paste below code in query editor and click on **Run**.

The `MSCK REPAIR TABLE` command scans a file system such as Amazon S3 for Hive compatible partitions that were added to the file system after the table was created. `MSCK REPAIR TABLE` compares the partitions in the table metadata and the partitions in S3. If new partitions are present in the S3 location that you specified when you created the table, it adds those partitions to the metadata and to the Athena table.

```sql
1
MSCK REPAIR TABLE default.amazon_reviews_parquet;
```

---

**You have created Athena table successfully. This Athena table (`default.amazon_reviews_parquet`) will be used to load data into Iceberg tables which we will be creating in next Lab.**

