+++ 
title = "Task 5: Installing Amazon CloudWatch agent with SSM" 
chapter = false 
weight = 5 
+++

The CloudWatch agent monitors activity on your EC2 instance to collect logs and metrics. The CloudWatch agent needs to be installed on the EC2 instance using AWS Systems Manager Run Command. Run Command enables you to perform actions on EC2 instances remotely. This tool is especially helpful at scale, where you can manage the configuration of many instances with a single command. 

1. In *Systems Manager* go again to the navigation pane, choose **Run command**

<img src="../images/cw1.png" alt="drawing" width="800"/> 

2. Then click on **Run a Command**.

<img src="../images/cw2.png" alt="drawing" width="500"/> 

3. In the *Command document list*, search and choose `AWS-ConfigureAWSPackage`

<img src="../images/cw3.png" alt="drawing" width="700"/> 

4. Into the *Command parameter* area:

* Action: select "Install" option
* Name: type `AmazonCloudWatchAgent`

<img src="../images/cw4.png" alt="drawing" width="700"/> 

5. In the *Targets* area:

* For Targets option, select "Choose a resource group"
* For Resource group, select `rg-wa` (This was the resource group that you created in the Task 3)

<img src="../images/cw5.png" alt="drawing" width="700"/> 

6. Click on **Run**

You will see the installation progress for the Amazon CloudWatch agent in both EC2 instances. Just wait a few seconds and then refresh your browser. You will see the status indicate *Success*.

<img src="../images/cw7.png" alt="drawing" width="800"/> 

{{% notice tip %}}
Reference: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance-fleet.html
*Section: Download the CloudWatch Agent on an Amazon EC2 Instance Using Systems Manager*
{{% /notice %}}