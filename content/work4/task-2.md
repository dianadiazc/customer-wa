+++ 
title = "Task 2: Improve granular control of communication" 
chapter = false 
weight = 2 
+++
Let's review and improve upon granular control of communication between workloads in the cloud.

1. Looking at the granular control of system-to-system communication used to be difficult. Now, looking at your **EC2** Service **Security Groups** allows you to quickly see who can talk to whom.

<img src="../images/sg1.png" alt="drawing" width="600"/>

2. Picking a Security Group like the **wa-database-sg** we can see the more traditional way of doing things.

<img src="../images/sg2.png" alt="drawing" width="600"/>

3. Checking the **Outbound rules**, we see the servers can talk to a range of IP’s, 65,536 to be precise. But there are only maybe 6-8 servers that they actually need to talk to. We can start reducing that number editing the Destination rule. 

<img src="../images/sg3.png" alt="drawing" width="700"/>

4. Go to **Edit Outbound rules** and **delete** the existing rule.

<img src="../images/sg5.png" alt="drawing" width="700"/>

<img src="../images/sg6.png" alt="drawing" width="700"/>

5. Select **Add rule**.

<img src="../images/sg7.png" alt="drawing" width="700"/>

6. For **Type**, select *"All Trafic"*. For **Destination**, look for the Security Group name **wa-web-server-dg** and select it. Click on **Save rule**.

<img src="../images/sg9.png" alt="drawing" width="700"/>

7. You will see the **Destination** of the rule now shows the Security Group you selected.

<img src="../images/sg10.png" alt="drawing" width="700"/>

You can **repeat** this by **Editing** and **Adding Rules** for each security group you want to allow access to.

{{% notice note %}}
In doing this, you’ve reduced the scope of internal traffic communication from 65,636 host down to 8. Additionally, if you ever need to stand up more servers in these groups, they would be automatically accessible without intervention, as long as you put them in the same Security Group. On premise, you would either need to have Firewalls between all internal VLAN’s, Routers, and sites or complex Network ACL’s on every switch in your environment. This reduces the risk of threats, the risk of misconfiguration, and the operational burden all at once.
{{% /notice %}}