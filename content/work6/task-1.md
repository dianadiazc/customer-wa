+++ 
title = "Task 1: Enable QuickSight" 
chapter = false 
weight = 2 
+++

Since you will be using QuickSight thru this lab, the first step will be enable the service.

1. In the console, go to **QuickSight** service.

    <img src="../images/goto-quicksight.png" alt="drawing" width="600"/>

1. Click on **Sign up for QuickSight**.

    <img src="../images/qs-signup.png" alt="drawing" width="600"/>

1. For this task we will enable the Standard version, click on the radio button nect to the **Standard** version.

1. Scroll down the page and click on **Continue**.

1. In the next page change the QuickSight region, select **US West (Oregon)**

    <img src="../images/qs-oregon.png" alt="drawing" width="350"/>

1. A warning will show up **Changing this may change some sections**. Click **OK**.

1. In the next page, under **Account info** set a **QuickSight account name** and a **Notification email address**. An account name can only contain characters (A-Za-z), digits (0-9), dashes (-) and no blank spaces.

    <img src="../images/qs-account-info.png" alt="drawing" width="350"/>

1. Remember the CUR dataset is stored in an S3 bucket, you need to provide permissions to QuickSight to access the dataset. Click the *checkbox* next to **Amazon S3**.

    <img src="../images/qs-clicks3.png" alt="drawing" width="600"/>

1. In the **Select Amazon S3 buckets** window, mark the checkbox next to the bucket `wa-cur-xxxxxxxxxx` and give write  permissions fot Athena Workgroup.

    <img src="../images/qs-select-bucket.png" alt="drawing" width="600"/>

1. Click **Finish**.

1. Click **Finish** again.

1. You will see your QuickSight account being created.

    <img src="../images/qs-creation.png" alt="drawing" width="800"/>

1. After a few seconds the account will be created, click on **Go to Amazon QuickSight**

    <img src="../images/qs-congrats.png" alt="drawing" width="450"/>

1. You will be logged in your QuickSight account, in the **What’s New in Amazon QuickSight** window you could see important information regarding service enhacements, fell free to review them. Once done, click **Close** at the bottom of the window.
