+++ 
title = "Task 4: Evaluate detailed logging capabilities" 
chapter = false 
weight = 4 
+++

We just made a bunch of changes, and on-premises it may be difficult to track them. Let's check the **CloudTrail** in **Services** to see what it noticed.

1. Go to service search boc > **CloudTrail**

<img src="../images/ct1.png" alt="drawing" width="500"/>

2.  The Dashboard shows us some recent events, but we want to see the complete **Event History**.

3.  Here we can see your **User Name** performing actions tracked by **Event name** against different **Resource Names**. API commands not related to Data (because we chose that earlier) are being captured by CloudTrail.

4.  You can remove the system calls by using a **Filter** on **User Name** and putting your **User Name** in the text box and hitting enter. Now **Scroll down**. Do you see all the ACL's you changed? But again, seeing these API calls doesn't give you a good visual of the changes occurring.

5.  Let's go to **Config**.

6.  I can see all of my resources, including some called **EC2 NetworkAcl**.

7.  Clicking there gives you a list of ACL's, and you can **click** on the first one.

8.  Seeing details on that ACL, you can also see a visual **Configuration Timeline**

9.  In the configuration timeline, you can see the changes that occurred over the past few minutes.
    -   If you don't see any changes go back and choose a different ACL
    
10. If you expand **Changes** you can see exactly what changes you made to the resource, including what you applied it to as a **Relationship Change**.

How would you do this on-premises?