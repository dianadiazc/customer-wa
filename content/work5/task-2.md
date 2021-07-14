+++ 
title = "Task 2: Create dynamic scaling policies" 
chapter = false 
weight = 1 
+++

<img src="../images/allup_light_Artboard.png" alt="drawing" width="200"/>

We will create policies to automate the creation of instances to scale out the architecture and support the increase in the demand. We can also reduce the number of instances in case the there is a reduction in the users and transactions into the application.

1.	You will create the **scale-out-policy**. Navigate to **EC2** > **Auto Scaling Groups**.

<img src="../images/T02S01.png" alt="drawing" width="600"/>

2.	Click on **waAutoscaleGroup**.

<img src="../images/T02S02.png" alt="drawing" width="600"/>

3.	Click the **Automatic scaling** tab.

<img src="../images/T02S03.png" alt="drawing" width="600"/>

4.	Click on **Create dynamic scaling policy**.

<img src="../images/T02S04.png" alt="drawing" width="600"/>

5.	In the **Create dynamic scaling policy** page, set the **Policy type** to **Simple scaling**.

<img src="../images/T02S05.png" alt="drawing" width="600"/>

6.	In the **Scaling policy name**, type `scale-out-policy`.

<img src="../images/T02S06.png" alt="drawing" width="600"/>

7.	In **CloudWatch alarm**, select **scale-out-alarm** from the dropdown menu.

<img src="../images/T02S07.png" alt="drawing" width="600"/>

8.	Under **Take the action**, set **Add | 2 | Capacity units**.

<img src="../images/T02S08.png" alt="drawing" width="600"/>

9.	Under **And then wait** type `60` seconds and click **Create**.

<img src="../images/T02S09.png" alt="drawing" width="600"/>

10.	Now you will create the **scale-in** policy, click on **Create dynamic scaling policy**.

<img src="../images/T02S10.png" alt="drawing" width="600"/>

11.	In the **Create dynamic scaling policy** page, set the **Policy type** to **Simple scaling**.

<img src="../images/T02S05.png" alt="drawing" width="600"/>

12.	In the **Scaling policy name**, type `scale-in-policy`.

<img src="../images/T02S12.png" alt="drawing" width="600"/>

13.	In **CloudWatch alarm**, select **scale-in-alarm** from the dropdown menu.

<img src="../images/T02S13.png" alt="drawing" width="600"/>

14.	Under **Take the action**, set **Remove | 2 | Capacity units**.

<img src="../images/T02S14.png" alt="drawing" width="600"/>

15.	Under **And then wait** type `60` seconds and click **Create**.

<img src="../images/T02S15.png" alt="drawing" width="600"/>

We have just automated the **scaling out** and **scaling in** for our architecture, this is an example of an easy implementation of advanced technology, that means that we just apply the design principle of **Democratize advanced technologies**.

<img src="../images/T02S15_.png" alt="drawing" width="600"/>