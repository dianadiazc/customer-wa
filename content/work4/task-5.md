+++ 
title = "Task 5: Evaluate network-based protections" 
chapter = false 
weight = 5 
+++

1.  Let's go back to **GuardDuty** and see what findings we may have. If this is a new or infrequently used account, you may have no Findings. If you do have Findings and this is not a new account, we can walk through those separately.
2.  Since this is a good design and relatively new, let's create some demonstration findings in **Settings**
3.  After we **Generate sample findings** we can go back to the **Findings**
4.  16 High Severity Findings, 30 Medium Severity Findings, and 7 Informational Findings (where can you see those numbers quickly) show up. Let's investigate the High Severity finding called **[SAMPLE] [SAMPLE] Backdoor:EC2/DenialOfService.Dns**
5.  You can see the (fake) instance that caused this Finding, what the instance did wrong, when it occurred, and more information. The ".Dns" at the end means something, do you know what? Does the **Action Type** help?
    -   What are the 3 data sources GuardDuty uses?
6.  **Scrolling down** the Findings list again you see another high severity **[SAMPLE] Backdoor:EC2/DenialOfService.UdpOnTcpPorts**.
7.  Here you see a lot of the same type of information. But why is this **Action Type** different?
    -   If we didn't turn on those logs how did it see the traffic?
8.  **Scrolling down** the Findings list a bit more you find **[SAMPLE]UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration**
9.  This one not only has a different **Action Type** but also starts with **IAMUser** instead of **EC2**. Why does that matter?
    -   Is this a different data source?

Now you've seen that GuardDuty is monitoring logs on your behalf, and without you having to pay for storage, the AI/ML or Threat feeds, and the man hours to do the analysis. This is all happening at Cloud scale too, no longer do you need to have terabytes of logs that are never touched.