---
title : "5.3.3 - Setup Folder Structure"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

## Step-by-Step Guide: Setup S3 Folder Structure

### Objective
Create an organized folder structure within the S3 bucket to store datasets, metadata, and transaction logs.

---

## Overview: Folder Structure

We will create the following structure:
```
ev-data-marketplace-datasets-xxxxx/
├── /datasets/          (EV dataset files)
├── /metadata/          (Dataset metadata and descriptions)
├── /logs/              (Transaction and access logs)
└── /backups/           (Backup copies)
```

---

## Step 1: Open Your S3 Bucket

1. Navigate to the S3 dashboard
2. Find and click on your bucket: `ev-data-marketplace-datasets-xxxxx`
3. You should see an empty bucket (no objects)


---

## Step 2: Create the `/datasets/` Folder

1. Click the **Create folder** button
2. In the folder name field, type: `datasets`
3. Click **Create folder** button
4. The `/datasets/` folder will appear in the bucket


---

## Step 3: Create the `/metadata/` Folder

1. Click **Create folder** button again
2. In the folder name field, type: `metadata`
3. Click **Create folder** button
4. The `/metadata/` folder will appear in the bucket


---

## Step 4: Create the `/logs/` Folder

1. Click **Create folder** button
2. In the folder name field, type: `logs`
3. Click **Create folder** button
4. The `/logs/` folder will appear in the bucket


---

## Step 5: Create the `/backups/` Folder

1. Click **Create folder** button
2. In the folder name field, type: `backups`
3. Click **Create folder** button
4. The `/backups/` folder will appear in the bucket


---

## Step 6: Verify All Folders

1. Your bucket should now display all four main folders:
   - datasets/
   - metadata/
   - logs/
   - backups/

*Screenshot placeholder: All folders created*

---

## Step 7: Create Sub-Folders in `/datasets/`

Now we'll create sub-folders within datasets to organize data by type:

### 7.1: Open datasets folder

1. Click on the `datasets/` folder to open it
2. Inside, create the following sub-folders by clicking **Create folder** for each:
   - `ev-battery-data`
   - `ev-charging-data`
   - `ev-economic-data`
   - `ev-location-data`


---

## Step 8: Create Sub-Folders in `/metadata/`

1. Navigate back to the bucket root
2. Click on the `metadata/` folder
3. Create the following sub-folders:
   - `dataset-descriptions`
   - `pricing-info`
   - `user-profiles`
   - `purchase-history`


---

## Step 9: Create Sub-Folders in `/logs/`

1. Navigate back to the bucket root
2. Click on the `logs/` folder
3. Create the following sub-folders:
   - `access-logs`
   - `transaction-logs`
   - `error-logs`


---

## Final Folder Structure

After completing all steps, your bucket structure should look like:

```
ev-data-marketplace-datasets-xxxxx/
├── datasets/
│   ├── ev-battery-data/
│   ├── ev-charging-data/
│   ├── ev-economic-data/
│   └── ev-location-data/
├── metadata/
│   ├── dataset-descriptions/
│   ├── pricing-info/
│   ├── user-profiles/
│   └── purchase-history/
├── logs/
│   ├── access-logs/
│   ├── transaction-logs/
│   └── error-logs/
└── backups/
```


---

## Summary

You have successfully set up a well-organized S3 bucket structure with:
- **Main folders** for logical organization (datasets, metadata, logs, backups)
- **Sub-folders** by data type and purpose
- **Clear separation** of concerns for scalability
- **Foundation ready** for data uploads and management

**Lab 1 Complete!** Your S3 bucket is now fully configured and ready for use in the marketplace.

---

## Next: Proceed to Lab 2 - Create IAM Users and Policies
