+++ 
title = "Task 7: Validating custom metrics and log groups" 
chapter = false 
weight = 7 
+++

1. Go to **Amazon Cloudwatch** service.

<img src="../images/lg1.png" alt="drawing" width="600"/> 

2. In the navigation pane, select **Metrics**, **All metrics** and later click on **CWAgent** on *Custom Namespaces*

<img src="../images/lg2.png" alt="drawing" width="600"/> 

{{% notice info %}}
NOTE: It may take up to 5 minutes for metrics to appear in the dashboard. **Refresh** your browser in case you don't see **CWAgent** after a couple of minutes.
{{% /notice %}}

3. Select the first metrics group.

<img src="../images/lg3.png" alt="drawing" width="600"/> 

4. Select one of the paths to check disk utilization percentage in the last hour.

<img src="../images/lg4.png" alt="drawing" width="800"/> 

5. (Optional) You can check memory utilization for your EC2 instances.

6. We are going to navigate through log groups. Go to **Logs** in the navigation pane and then click on Log groups. You will see 4 new **Log groups** where you can view the events happening in your instances’ operating system and applications (Apache and MariaDB).

* db_general_query_log
* httpd_access_log
* mariadb_log
* messages

<img src="../images/lg5.png" alt="drawing" width="800"/> 

7. Now access the application web server using the public DNS or IP, make some inserts to update the database.

<img src="../images/app4.png" alt="drawing" width="800"/> 

8. Go back to **CloudWatch logs** -> **Log groups** -> **httpd_access_log** -> Click on the log stream and you will see your public IP listed (use https://www.whatismyip.com)

<img src="../images/lg7.png" alt="drawing" width="900"/> 

<img src="../images/lg10.png" alt="drawing" width="1000"/> 

9. Now go to **db_general_query_log** -> Click on the log stream and you will see logged the database inserts you just made.

<img src="../images/lg9.png" alt="drawing" width="1000"/> 

<img src="../images/lg11.png" alt="drawing" width="1000"/> 

**You have finished this first Lab!** Awesome, right? :)

---

In a traditional environment you would have to set up the systems and software to perform administration activities. You would require a server to execute your scripts. You would need to manage authentication credentials across all of your systems.

**Operations as code** reduces the resources, time, risk, and complexity of performing operations tasks and ensures consistent execution, so **your organization can focus on delivering more value to customers vs operational firefighting**. You can take operations as code and automate operations activities by using scheduling and event triggers. Through integration at the infrastructure level you avoid “swivel chair” processes that require multiple interfaces and systems to complete a single operations activity.







