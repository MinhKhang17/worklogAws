---
title : "1.2 Create Athena tables"
date : 2026-03-25 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

1.  Go to the [Athena Console](https://console.aws.amazon.com/athena/home) 
    
    ---
    
2.  Open the **Query Editor** (not the Notebook editor)
    
    ---
![open query editor](/images/5-Workshops/5.3/5.3.2/5.png)
3.  Once inside the Athena Query Editor, click **Edit Settings** as shown below:
    

![Athena console](/images/5-Workshops/5.3/5.3.2/6.png)

---

1.  Go to **Settings** and click **Manage**

![Athena Settings](/images/5-Workshops/5.3/5.3.2/7.png)

---

4.  Under Manage Settings, click **Browse S3**.

![Athena Settings](/images/5-Workshops/5.3/5.3.2/8.png)

---

5.  Select your S3 bucket by clicking its radio button, then click **Choose**. For self-paced labs, select the bucket you created earlier. For AWS Events, choose the bucket named iceberg-workshop-ACCOUNTID (for example: iceberg-workshop-123456789).

![Choose-S3-data-set](/images/5-Workshops/5.3/5.3.2/9.png)

---

6.  Click **Save** to store the S3 output location.

![Save-s3-location](/images/5-Workshops/5.3/5.3.2/10.png)

---

7.  Switch to the **Editor** tab, paste the query below. Replace **YOURBUCKET** with your S3 bucket name, then click **Run**.

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

![Run-athena-create-table](/images/5-Workshops/5.3/5.3.2/11.png)

---

8.  Paste the command below in the query editor and click **Run**.

The `MSCK REPAIR TABLE` command scans a file system such as Amazon S3 for Hive compatible partitions that were added to the file system after the table was created. `MSCK REPAIR TABLE` compares the partitions in the table metadata and the partitions in S3. If new partitions are present in the S3 location that you specified when you created the table, it adds those partitions to the metadata and to the Athena table.

```sql
MSCK REPAIR TABLE default.amazon_reviews_parquet;
```
![Run-athena-repair-table](/images/5-Workshops/5.3/5.3.2/12.png)
---

**The Athena table has been successfully created. This table (`default.amazon_reviews_parquet`) will act as the data source for loading data into the Iceberg tables we create in the next lab.**


