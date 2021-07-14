+++ 
title = "Task 1: Create the autoscaling alarms" 
chapter = false 
weight = 1 
+++

<img src="../images/aws-auto-scaling-how-it-works-diagram.png" alt="drawing" width="600"/>

After taking actions over Operations Excellence, Resiliency and Security, we are now executing actions to improve the performance through alarms to automate the leverage or reduction of the number of instances required, based on the performance of the application.

1. First you will create the **scale out** alarm, navigate to AWS CloudWatch.

<img src="../images/T01S01.png" alt="drawing" width="600"/>

2. Left pane, click on **Alarms**.

<img src="../images/T01S02.png" alt="drawing" width="600"/>

3.  Click on **Create alarm**.

<img src="../images/T01S03.png" alt="drawing" width="600"/>

4. In **Specify metric and conditions**, click on **Select metric**. 

<img src="../images/T01S04.png" alt="drawing" width="600"/>

5. In **Select metrics** section, go down to the bottom of the window and click on **EC2**.

<img src="../images/T01S05.png" alt="drawing" width="600"/>

6. Click on **By Auto Scaling Group**.

<img src="../images/T01S06.png" alt="drawing" width="600"/>

7. Select the **CPUUtilization** metric in the **Metric Name** column and click on **Select metric**.

<img src="../images/T01S07.png" alt="drawing" width="600"/>

8. In the **Specify metric and conditions** page, in the **Metric** section, change **Period** to `1 minute`.

<img src="../images/T01S08.png" alt="drawing" width="600"/>

9. Go down in the window and in the **Conditions** section, make sure the **Whenever CPUUtilization is...** is set to **Greater**.

<img src="../images/T01S09.png" alt="drawing" width="600"/>

10. Update the **than...** text box typing `70` and click on **Next**.

<img src="../images/T01S10.png" alt="drawing" width="600"/>

11. For the purpose of this lab, we are not going to send any notification, but you should consider configuring this option to send automated notifications in your environment. That's why we are going to select in the **Configure actions** page, in the **Notification** section, click on **Remove** and go to the bottom of the page to click con **Next**.

<img src="../images/T01S11.png" alt="drawing" width="600"/>

12. In the **Add name and description** page, in the **Alarm name** box type `scale-out-alarm` and click on **Next**.

<img src="../images/T01S12.png" alt="drawing" width="600"/>

13. In the **Preview and create** page, click on **Create alarm**.

<img src="../images/T01S13.png" alt="drawing" width="600"/>

You have created the **scale out** alarm, now you will create the **scale in** alarm. 
Click on **Create alarm**

<img src="../images/T01S13_.png" alt="drawing" width="600"/>

14.	In **Specify metric and conditions**, click on **Select metric**.

<img src="../images/T01S04.png" alt="drawing" width="600"/>

15.	 In **Select metrics** section, go down to the bottom of the window and click on **EC2**.

<img src="../images/T01S05.png" alt="drawing" width="600"/>

16.	Click on **By Auto Scaling Group**.

<img src="../images/T01S06.png" alt="drawing" width="600"/>

17.	Select the **CPUUtilization** metric in the **Metric Name** column and click on **Select metric**.

<img src="../images/T01S07.png" alt="drawing" width="600"/>

18.	In the **Specify metric and conditions** page, **Metric** section, change **Period** to `1 minute`.

<img src="../images/T01S08.png" alt="drawing" width="600"/>

19.	In the **Conditions** section, set the **Whenever CPUUtilization is...** to **Lower**.

<img src="../images/T01S19.png" alt="drawing" width="600"/>

20.	Update the **than...** text box, type `30` and click on **Next**.

<img src="../images/T01S20.png" alt="drawing" width="600"/>

21.	For the purpose of this lab, we are not going to send any notification, but you should consider configuring this option to send automated notifications in your environment. That's why we are going to in the **Configure actions** page, **Notification** section, click on **Remove** and go to the bottom of the page, click on **Next**.

<img src="../images/T01S11.png" alt="drawing" width="600"/>

22.	In the **Add name and description** page, in the **Alarm name** box type `scale-in-alarm` and click on **Next**.

<img src="../images/T01S22.png" alt="drawing" width="600"/>

23.	In the **Preview and create** page, click on **Create alarm**.

<img src="../images/T01S23.png" alt="drawing" width="600"/>

You have created the **scale in** and **scale out** alarms. Now let's go to create the policies to execute the automated increment or reduction in the architecture.

<img src="../images/T01S23_.png" alt="drawing" width="600"/>