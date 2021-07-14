+++ 
title = "Task 3: Create an Amazon CloudWatch Dashboard" 
chapter = false 
weight = 1 
+++

<img src="../images/allup_light_analyze-data.png" alt="drawing" width="200"/>

In this phase we will create a dashboard to visualize the performance of our resources and detect the alarms that can trigger an automated action like scaling.

1.	Go to AWS Cloudwatch.

<img src="../images/T01S01.png" alt="drawing" width="600"/>

2.	From the left pane, click on **Dashboards**.

<img src="../images/T03S02.png" alt="drawing" width="150"/>

3.	Click on **Create dashboard**.

<img src="../images/T03S03.png" alt="drawing" width="600"/>

4.	For **Dashboard name** type `WA-ASG` and then click **Create dashboard**.

<img src="../images/T03S04.png" alt="drawing" width="400"/>

5.	Click on **Cancel** in the **Add to this dashboard** window.

<img src="../images/T03S05.png" alt="drawing" width="600"/>

You will add 3 widgets to this dashboard.

* Number of heathy ELB instances

* Average CPU% Utilization

* Alarm status

6.	First you will add the number of healthy instances widget, from the left pane click on **Metrics**.

<img src="../images/T03S06.png" alt="drawing" width="150"/>

7.	From the **All metrics** tab, click on **ApplicationELB**.

<img src="../images/T03S07.png" alt="drawing" width="600"/>

8.	Click on **Per AppELB, per TG Metrics**.

<img src="../images/T03S08.png" alt="drawing" width="600"/>

9.	Select the checkbox which has **HealthyHostCount** under the **Metric Name** column.

<img src="../images/T03S09.png" alt="drawing" width="600"/>

10.	Click on the **Graphed metrics** tab.

<img src="../images/T03S10.png" alt="drawing" width="600"/>

11.	Set **Statistics** to **Maximum** and **Period** to `1 minute`.

<img src="../images/T03S11.png" alt="drawing" width="600"/>

12.	From the top right corner click on **Actions** > **Add to dashboard**.

<img src="../images/T03S12.png" alt="drawing" width="600"/>

13.	Under **Select a widget type** select **Number** and click on **Add to dashboard**.

<img src="../images/T03S13.png" alt="drawing" width="600"/>

14.	From the top of the Dashboard page, click on **Save dashboard**.

<img src="../images/T03S14.png" alt="drawing" width="600"/>

15.	Now you will add the CPU% average utilization widget, from the left pane click on **Metrics**.

<img src="../images/T03S06.png" alt="drawing" width="150"/>

16.	Click **Remove all** to clean the graph panel.

<img src="../images/T03S16.png" alt="drawing" width="600"/>

17.	Click the **All metrics** tab.

<img src="../images/T03S17.png" alt="drawing" width="600"/>

18. Click on **All**.

<img src="../images/T03S18.png" alt="drawing" width="600"/>

19. Click on **EC2**.

<img src="../images/T03S19.png" alt="drawing" width="600"/>

20.	Click **By Auto Scaling Group**.

<img src="../images/T03S20.png" alt="drawing" width="600"/>

21.	Select the checkbox which has **CPUUtilization** under the **Metric Name** column.

<img src="../images/T03S21.png" alt="drawing" width="600"/>

22.	Click the **Graphed metric** tab.

<img src="../images/T03S22.png" alt="drawing" width="600"/>

23.	Set the **Statistic** to **Average** and **Period** to **1 minute**.

<img src="../images/T03S23.png" alt="drawing" width="600"/>

24.	From the top right corner click on **Actions** > **Add to dashboard**.

<img src="../images/T03S24.png" alt="drawing" width="600"/>

25.	Leave defaults and click on **Add to dashboard**.

<img src="../images/T03S25.png" alt="drawing" width="600"/>

26.	From the top of the Dashboard page, click on **Save dashboard**.

<img src="../images/T03S26.png" alt="drawing" width="600"/>

27.	Now you will add the alarm status widget, from the left pane click on **Alarms**.

<img src="../images/T03S27.png" alt="drawing" width="150"/>

28.	Click on the checkboxes next to both alarms, **scale-in-alarm** and **scale-out-alarm**.

<img src="../images/T03S28.png" alt="drawing" width="600"/>

29.	From the top right corner click on **Actions** > **Add to dashboard**.

<img src="../images/T03S29.png" alt="drawing" width="600"/>

30.	Under **Select a widget type** select **Alarm status** and click on **Add to dashboard**.

<img src="../images/T03S30.png" alt="drawing" width="600"/>

31.	From the left pane, click on **WA-ASG**, under **Dashboards**.

<img src="../images/T03S31.png" alt="drawing" width="600"/>

32.	From the top of the Dashboard page, click on **Save dashboard**.

<img src="../images/T03S32.png" alt="drawing" width="600"/>

33.	Feel free to move and resize the *widgets* as you like, and remember to save your changes.

Now, considering that monitoring is an area of **Performance efficiency** and for taking a data-driven approach for our architecture, we created our dashboard to be aware of any deviance from expected performance and take automated actions. We also should consider to make trade-offs in the architecture to improve performance, such as scaling up, scaling out, using compression or caching, or relaxing consistency requirements.