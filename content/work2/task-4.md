+++ 
title = "Task 4: Enabling SSM for EC2 instances" 
chapter = false 
weight = 4 
+++

**AWS Systems Manager** (formerly known as SSM) is an AWS service that you can use to view and control your infrastructure on AWS. Using the Systems Manager console, you can view operational data from multiple AWS services and automate operational tasks across your AWS resources. 

AWS Systems Manager Agent (SSM Agent) is Amazon software that can be installed and configured on an EC2 instance, an on-premises server, or a virtual machine (VM). SSM Agent makes it possible for Systems Manager to update, manage, and configure these resources.

SSM Agent is preinstalled, by default, on the following Amazon Machine Images (AMIs):

* Amazon Linux

* Amazon Linux 2

* Amazon Linux 2 ECS-Optimized Base AMIs

* Ubuntu Server 16.04, 18.04, and 20.04

In this lab we will use Amazon Linux 2 AMIs. For manually installation of the SSM agent you can review the following link: 

https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html


## Creating an EC2 instance profile

By default, AWS Systems Manager doesn't have permission to perform actions on your instances. Grant access by using an AWS Identity and Access Management (IAM) instance profile. An instance profile is a container that passes IAM role information to an Amazon Elastic Compute Cloud (Amazon EC2) instance at launch. More info here: 

https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html

1. Go to **IAM** Service

<img src="../images/ip1.png" alt="drawing" width="700"/>

2. Click on **Role** and later on **Create Role**

<img src="../images/iam1.png" alt="drawing" width="700"/>

3. Click on "AWS service", select EC2 and later on "Next: Permissions".

<img src="../images/ip3.png" alt="drawing" width="700"/>

4. Add the following Managed Policies:

* AmazonSSMManagedInstanceCore
* CloudWatchAgentServerPolicy

<img src="../images/ip4.png" alt="drawing" width="500"/>

<img src="../images/ip5.png" alt="drawing" width="500"/>

5. Click on **Next: Tags** (You are not going to modify anything here) and later click on **Next: Review**. Use <code>wa-lab-ssm-ec2-role</code> as *"Role name"*. Verify policies added in the previous step. Finally, click on **Create role**.

<img src="../images/ip6.png" alt="drawing" width="500"/>

## Modifying EC2 instance profiles

6. Go to **EC2** console and select the *wa-web-server* instance. Click on **Actions** -> **Security** -> **Modify IAM role**

<img src="../images/ip7.png" alt="drawing" width="1000"/>

7. For *IAM Role*, select <code>wa-lab-ssm-ec2-role</code> and click on **Save**

<img src="../images/ip8.png" alt="drawing" width="8000"/>

8. Repeat the steps **6** and **7** with *wa-db-server* instance.

<img src="../images/ip81.png" alt="drawing" width="8000"/>

{{% notice warning %}}
To ensure that your instances will be available in Systems Manager, please **stop** and **start** both **EC2 instances**. 
{{% /notice %}}

## Checking EC2 instances in Systems Manager

9. Go to **Systems Manager** service.

<img src="../images/ip9.png" alt="drawing" width="800"/> 

10. To ensure that your EC2 instances are correctly configured for Systems Manager, go to Inventory in the left panel.

<img src="../images/ip10.png" alt="drawing" width="800"/> 

11. Scroll down to the bottom page. On *Corresponding managed instances*, you will see your Amazon EC2 instances. Now you can use Systems Manager to automate operational tasks on your EC2 instances.

{{% notice info %}}
**NOTE:** After modifying the instance profiles and restarting instances, it may take up to 5 minutes for the instances to appear in the managed instances inventory.
{{% /notice %}}

<img src="../images/ip11.png" alt="drawing" width="800"/> 







