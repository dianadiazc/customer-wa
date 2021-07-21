+++ 
title = "Task 2: Adding a data source in QuickSight" 
chapter = false 
weight = 3 
+++

1. In this task you will a add an Athena table pre-created for you as part of this lab environment as a new Dataset for Analysis. The source dataset is an parquet file stored in an S3 bucket in the account you currently working on.

1. In the Analyses page, click on **New analysis**.

    <img src="../images/qs-new-analysis.png" alt="drawing" width="800"/>

1. Click on **New dataset**.

1. From the data source options, click on **Athena**.

    <img src="../images/qs-select-athena.png" alt="drawing" width="800"/>

1. In the **New Athena data source** window, type `wa-cur`as the **Data source name.

1. Click on **Create data source**.

    <img src="../images/qs-add-athena-ds.png" alt="drawing" width="500"/>

1. In the **Choose your table** window, under **Database: contain sets of tables.** select **wa-cur-lab5-glue-db**. This Glue database has been precreated for this lab.

1. Under **Tables: contain the data you can visualize.** select the table called `wa_cur_xxxxxxxxxxxx`.

1. Click on **Select**.

    <img src="../images/qs-select-glue-db.png" alt="drawing" width="500"/>

1. In the **Finish dataset creation** window, click on **Visualize**.