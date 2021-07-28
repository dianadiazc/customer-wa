+++ 
title = "Task 3: Improve granular network-based controls" 
chapter = false 
weight = 3 
+++

Let's improve on our network-based controls by using Network ACLs to prevent side-to-side movement in a granular way.

Security Groups are awesome at allowing access, but in **VPC** Services, **Network ACLs** are great at explicitly blocking them. For instance, if you wanted to make sure you explicitly blocked the Load Balancer in my Web Application from talking to my Database servers, you could **Create a network ACL**. Let's do it.

1. Go to **VPC** service.

<img src="../images/nacl1.png" alt="drawing" width="800"/>

2. In the left pane, select **Network ACLs**.

<img src="../images/nacl2.png" alt="drawing" width="600"/>

3. Click on **Create network ACL**.

<img src="../images/nacl3.png" alt="drawing" width="800"/>

4. For **Name**, use `LoadBalancerIsolation`. For **VPC**, select `wa-lab-vpc`. Click on **Create network ACL**.

<img src="../images/nacl4.png" alt="drawing" width="600"/>

5. Click on the Network ACL ID that you created in the previous step. When it shows the information, copy the NACL ID in a text editor because we will use it later.

<img src="../images/nacl5.png" alt="drawing" width="900"/>

6.  Select **Outbound Rule** option and later **Editing outbound rules**.

<img src="../images/nacl6.png" alt="drawing" width="800"/>

7.  **Adding Rules** like these would block whatever Subnet you apply this to from talking to the Database Subnets, but still allow access to the rest of the network. Note that NACLs are evaluated in the specific order of their Rule #.

    -   Rule #: **50**\
        Of type **All Traffic**\
        To the Destination **10.100.4.0/24**\
        And a **Deny** Behavior\
        and
    -   Rule #: **60**\
        Of type **All Traffic**\
        To the Destination **10.100.5.0/24**\
        And a **Deny** Behavior\
        and
    -   Rule #: **100**\
        Of type **All Traffic**\
        To the Destination **0.0.0.0/0**\
        And an **Allow** Behavior

Click on **Add new rule**, add information per rule and click on **Save changes**.

<img src="../images/nacl25.png" alt="drawing" width="1000"/>

8.  After **Saving** you need to allow access to that subnet from the internet, so recreating the **All Traffic Allow** rule for **Inbound Rules** is necessary.

    -   Rule #: **100**\
        Of type **All Traffic**\
        To the Destination **0.0.0.0/0**\
        And a **Allow** Behavior

Select **Inbound rules** and **Edit inbound rules**.

<img src="../images/nacl8.png" alt="drawing" width="800"/>

9. Click on **Add rule**, type the information above for the rule and click on **Save changes**.

<img src="../images/nacl9.png" alt="drawing" width="800"/>

10.  After **Saving** you need to use **Subnet Associations**, and then click on **Edit subnet associations**.

<img src="../images/nacl10.png" alt="drawing" width="800"/>

11.  Here you have to associate the NACLs with the subnets **wa-public-subnet-1** and **wa-public-subnet-2**. Select both subnets and click on **Save changes**.

<img src="../images/nacl11.png" alt="drawing" width="1000"/>

12. Let's check at this point that the application is working after networking changes. (Optional) You could add more items in this step.

<img src="../images/chaos1.png" alt="drawing" width="600"/>

{{% notice note %}}
Now, you've effectively ensured that if the Load Balancers in your environment misbehave, they can't communicate with or compromise the Database servers directly. But there was no additional hardware, firewall, or complex routing required to make this simple change in the simple network topology.
{{% /notice %}}
