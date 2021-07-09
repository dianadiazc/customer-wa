+++ 
title = "Task 6: Minimize admin access risk" 
chapter = false 
weight = 6 
+++

Let's review and improve upon granular control of communication between workloads in the cloud.

1. Looking at the granular control of system-to-system communication used to be difficult. Now, looking at your **EC2** Service **Security Groups** allows you to quickly see who can talk to whom.

2. Picking a Security Group like the **Services Server Security Group** we can see the more traditional way of doing things.

3. Checking the **Outbound** rules, we see the servers can talk to a range of IP’s, 65,536 to be precise. But there are only maybe 6-8 servers that they actually need to talk to.

4. Well, if we copy the **GroupID** of the **PoC Web Server Security Group** we can start to reduce that number

5. **Edit** the **Outbound** set of rules for the **Services Server Security Group** and replace the 10.0.0.0/16 with the Security Group name you copied.

6. **Save** this and you’ll see the **Destination** of the rule now shows the Security Group you listed.

7. You can **repeat** this by **Editing** and **Adding Rules** for each security group you want to allow access to.

In doing this, you’ve reduced the scope of internal traffic communication from 65,636 host down to 8. Additionally, if you ever need to stand up more servers in these groups, they would be automatically accessible without intervention, as long as you put them in the same Security Group. On premise, you would either need to have Firewalls between all internal VLAN’s, Routers, and sites or complex Network ACL’s on every switch in your environment. This reduces the risk of threats, the risk of misconfiguration, and the operational burden all at once.