---
title : "Introduction to Apache Iceberg on AWS"
date : 2026-03-25 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---


[Apache Iceberg](https://iceberg.apache.org/) is an open table format purpose-built for very large analytical datasets. It supports a wide range of modern data lake operations including record-level insert, update, delete, and time travel queries. Iceberg treats large collections of files as structured tables, enabling seamless schema and partition evolution without data rewrites. Its architecture is specifically optimized for use with Amazon S3 and provides strong guarantees of data correctness even under concurrent write workloads.

---

Key terminology used in Apache Iceberg tables includes:

-   Schema – The names and data types of all fields in a table.
-   Partition spec – A definition that specifies how partition values are computed from data fields.
-   Snapshot – A point-in-time view of the table, capturing the full set of data files at that moment.
-   Manifest list – A file that enumerates all manifest files associated with a given snapshot.
-   Manifest – A file listing data or delete files that together form a portion of a snapshot.
-   Data file – A file containing actual row data for the table.
-   Delete file – A file that encodes which rows have been removed, either by position or by value.

---

Iceberg tracks individual data files rather than directories. Writers can produce files independently and add them to the table in a single, explicit commit. Table state is maintained through metadata files, and every change to the table creates a new metadata file that atomically replaces the previous one. This metadata file records the table's schema, partitioning configuration, and all snapshots of the table. Each snapshot represents the full state of the table at a specific point in time and serves as an access point for querying the complete set of data files.

Each snapshot is a self-contained view of the data at a particular moment. Snapshots are listed in the metadata file, but the actual file references are distributed across separate manifest files. This atomic transition between metadata versions provides snapshot isolation, allowing readers to work from a consistent version without being affected by ongoing changes. Data file paths are stored in manifests, each of which contains metadata about every file in the table, including partition data and statistics. Manifests can be shared across snapshots to minimize rewriting of unchanged metadata.

---

**Apache Iceberg on Amazon Athena**

Iceberg tables registered in the AWS Glue catalog are fully supported by Athena, following the specifications of the open-source [Glue Catalog implementation](https://iceberg.apache.org/docs/latest/aws/#glue-catalog). Athena supports Iceberg v2 tables using the Parquet file format. To define an Iceberg table via Athena, set the `table_type` property to `ICEBERG` in the `TBLPROPERTIES` clause, as shown in the syntax below.

```sql
CREATE TABLE
  [db_name.]table_name (col_name data_type [COMMENT col_comment] [, ...] )
  [PARTITIONED BY (col_name | transform, ... )]
  LOCATION 's3://DOC-EXAMPLE-BUCKET/your-folder/'
  TBLPROPERTIES ( 'table_type' ='ICEBERG' [, property_name=property_value] )
```

---

**Apache Iceberg on Amazon EMR**

Beginning with Amazon EMR release 7.5.0, you can run Apache Spark 3 on EMR clusters with native Iceberg table format support. EMR 7.5.0 ships with Iceberg version 1.6.0. You can provision a cluster via the AWS Management Console, the AWS CLI, or the Amazon EMR API. To activate Iceberg support, include the following classification in your cluster configuration:

```java
[{ "Classification":"iceberg-defaults",
    "Properties":{"iceberg.enabled":"true"}
}]
```

Alternatively, you can create an EMR cluster with the Spark application and include the file `/usr/share/aws/iceberg/lib/iceberg-spark3-runtime.jar` as a JAR dependency in your Spark jobs.

This workshop is expected to take up to 2 hours. Please use the **us-east-1** region throughout, as the dataset used in this workshop resides there.

