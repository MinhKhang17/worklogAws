---
title : "3.1 Create EMR cluster"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

If you are running this workshop in your own account you need to follow below steps to create the EMR Cluster.

1.  Navigate to [EMR Console](https://console.aws.amazon.com/elasticmapreduce/home) 

---

2.  Click on **Create cluster** button

![click-create-cluster](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/create_cluster.png)

---

3.  On the **create cluster console** under **Name and applications** enter cluster name

![go-to-advance-option](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/clustername.png)

4.  Next, under **Amazon EMR release** , select `emr-6.5.0`, and in **application bundle** select check boxes for
    
    1.  Hadoop
    2.  Hive
    3.  JupyterEnterpriseGateway
    4.  Spark
    5.  Livy

In **Software settings** choose the drop down and enter below configurations

```java
[{ "Classification":"iceberg-defaults",
    "Properties":{"iceberg.enabled":"true"}
}]
```

This lab has been tested with `EMR 6.5.0`. Hence, we recommend that you use the same EMR release for your workshop.

![Create-Cluster-Advanced-Options](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/cluster-config.png)

Click on the **Next** and scroll down to **Auto-termination** option and uncheck the **auto-termination** Check Box.

![Create-Cluster-Advanced-Options](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/disable-auto-terminate.png)

Click on **Next** button few times till you get **Create cluster** button. Keep all other settings default. Click on **Create cluster** to create EMR cluster. This step may take up to 10 minutes to complete. Once the EMR cluster is created, continue with the next section.

---
