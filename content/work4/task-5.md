+++ 
title = "Task 5: Evaluate network-based protections" 
chapter = false 
weight = 5 
+++

1. Let's go back to **GuardDuty** and see what findings we may have. Because this is a new account, you may have no Findings.

<img src="../images/ct11.png" alt="drawing" width="800"/>

2. Since this is a good implementation based on the best practices and relatively new infrastructure, let's create some demonstration findings in **Settings**.

<img src="../images/gd1.png" alt="drawing" width="800"/>

3. Go to **Sample findings** and click on **Generate sample findings**.

<img src="../images/gd2.png" alt="drawing" width="800"/>

4. Go to  **Findings**.

<img src="../images/gd3.png" alt="drawing" width="800"/>

5. Now we have High, Medium and Low Severity Findings. You can identify the number of findings per severity checking at the top right of your screen.

<img src="../images/gd4.png" alt="drawing" width="300"/>

In this case we have:

* 12 **Low** Severity Findings
* 30 **Medium** Severity Findings
* 32 **High** Severity Findings

6. We are going to filter the High Severity Findings just clicking on the red icon.

<img src="../images/gd5.png" alt="drawing" width="800"/>

7. Let's investigate the High Severity finding called **[SAMPLE] Backdoor:EC2/DenialOfService.Dns**.

<img src="../images/gd7.png" alt="drawing" width="800"/>

8. You can see the (fake) instance that caused this Finding, what the instance did wrong, when it occurred, and more information. If you **scroll down** into the finding details, you will see information related to the **Action** which gives details on the type of activity that triggered the finding. The information available varies based on action type.

<img src="../images/gd8.png" alt="drawing" width="800"/>

9. Take a look at other findings. 

<img src="../images/gd9.png" alt="drawing" width="800"/>

Now you've seen that GuardDuty is monitoring logs on your behalf, and without you having to pay for storage, the AI/ML or Threat feeds, and the man hours to do the analysis. This is all happening at Cloud scale too, you no longer need to have terabytes of logs that are never used.

{{% notice tip %}}
Learn more about **Amazon GuardDuty** findings here: https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html
{{% /notice %}}