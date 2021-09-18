+++ 
title = "Task 1: Enable AWS Config" 
chapter = false 
weight = 1 
+++

Before you can start monitoring your AWS resources for compliance, you must enable AWS Config in your environment. AWS Config provides a detailed view of the configuration of AWS resources in your account. Additionally, you can observe how resources relate to one another, past configurations, and how the relationships change over time.

### Set up AWS Config

1. Open the **AWS Config Console** by selecting <span style="background-color:#232f3e; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;">Services <i class="fas fa-angle-down"></i></span> and typing `config` in the filter box.

1. Choose **Config**.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Get started</span>.

1. In the **General Settings** section, for **Resource types to record**, choose **Record specific resource types**.

1. Within **Resource category**, choose **AWS resources**.

1. Within **Resource type**, select **AWS EC2 Instance**. The dropdown will display **Multiple Selected**.

1. In the **AWS Config role** section, select the option **Choose a role from your account**.

1. For **Role name** select **ConfigServiceRole**.

1. In the **Delivery method** section, select **Choose a bucket from your account**. For **S3 bucket name**, select the bucket starting with "config-bucket-lab*".

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. No changes on this page, choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Confirm</span>.

1. You may close the "Welcome to AWS Config" window

**NOTE:** A warning message may appear at the top of the page requesting that you update the IAM Policy used by AWS Config. This warning can be ignored for purposes of this lab.
