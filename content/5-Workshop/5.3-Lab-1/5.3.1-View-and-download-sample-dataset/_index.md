---
title : "1.1 View and download sample dataset"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

We will be working with a simulated version of the Amazon Product Reviews dataset for both the Athena and EMR labs. Take a few minutes to familiarize yourself with the structure and content of this dataset.

**Amazon Customer Reviews Dataset**

Amazon Customer Reviews (also known as Product Reviews) is one of Amazon's most iconic features. Over more than two decades since the first review was published in 1995, millions of Amazon customers have contributed over one hundred million reviews, sharing opinions and describing their experiences with products on Amazon.com. This rich dataset has become a valuable resource for academic research in fields such as Natural Language Processing (NLP), Information Retrieval (IR), and Machine Learning (ML). The dataset was designed to represent a cross-section of customer evaluations and opinions, geographical variations in product perception, as well as promotional intent or reviewer bias.

NOTE: The dataset used in this workshop is simulated and contains randomly generated numbers, names, and text.

**Download the sample dataset and upload it to S3**

1.  Download the dataset from one of the links below
    
    -   [Sample Data - us-east-1](https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/e57af944-04b9-41f5-8285-90295ed32bdc/simulatedproductreviews.parquet)
        
    -   [Sample Data - us-west-2](https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/e57af944-04b9-41f5-8285-90295ed32bdc/simulatedproductreviews.parquet)
        
2.  Open your [AWS S3 console](https://s3.console.aws.amazon.com/s3/buckets) 
    
3.  Click on the name of the S3 bucket that was created for you
    
4.  Click **Create folder**
    
![create folder](/images/5-Workshops/5.3/5.3.1/3.png)

5.  Type **productreviews** as the folder name, then click the **Create folder** button
    
6.  Navigate into the newly created folder by clicking on **productreviews**, then click the **Upload** button
    
7.  Click **Add files**, select the dataset file you downloaded in step 1, then click **Upload**

![upload file](/images/5-Workshops/5.3/5.3.1/4.png)
