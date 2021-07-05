+++ 
title = "Task 7: Validating custom metrics and log groups" 
chapter = false 
weight = 7 
+++

1. Go to **Amazon Cloudwatch** service.

<img src="../images/lg1.png" alt="drawing" width="600"/> 

2. In the navigation pane, select **Metrics** and later click on **CWAgent** on *Custom Namespaces*

<img src="../images/lg2.png" alt="drawing" width="600"/> 

3. Select the first metrics group.

<img src="../images/lg3.png" alt="drawing" width="600"/> 

4. Select one of the paths to check disk utilization percentage in the last hour.

<img src="../images/lg4.png" alt="drawing" width="800"/> 

5. (optional) You can check memory utilization for your EC2 instances.

6. We are going to navigate through log groups. Go to **Logs** in the navigation pane and later click on **Log groups**. You will see 4 new log groups where you can visualize the events happening in your instances operating system and applications (Apache and MariaDB).

* db_general_query_log
* httpd_access_log
* mariadb_log
* messages

<img src="../images/lg5.png" alt="drawing" width="800"/> 


7. Now access the application web server using the public DNS or IP, make some inserts to update the database.

<img src="../images/lg6.png" alt="drawing" width="800"/> 

8. Go back to **CloudWatch logs** -> **Log groups** -> **httpd_access_log** -> Click on the log stream and you will see your public IP listed (use https://www.whatismyip.com)

<img src="../images/lg7.png" alt="drawing" width="900"/> 

<img src="../images/lg8.png" alt="drawing" width="1000"/> 

9. Now go to **db_general_query_log** -> Click on the log stream and you will see logged the database inserts you just made.

<img src="../images/lg9.png" alt="drawing" width="1000"/> 


You have finished this first Lab. Awesome, right? :)







