+++ 
title = "Task 2: Create AWS Config Rules" 
chapter = false 
weight = 2 
+++

Now that you have enabled AWS Config, you will establish rules that will check resource compliance with your organization's published architecture standards.

**NOTE:** You may see a note at the top of the screen that a redesigned AWS Config console is available for use. For this lab, please do not use the redesigned console.

### Task 2.1: Add AWS Config Rule to enforce required tags

First, you will create a rule that confirms required tags populated with appropriate values on each of your EC2 instances. Consistent tagging is a useful tool in managing costs associated with running different applications or workloads in your environment. It can also be helpful in allocating costs to different departments that deploy and operate resources in AWS.

1. On the left hand navigation pane, choose **Rules**.

2. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span>.

3. Select **Add AWS managed rule** for Rule Type.

4. In **AWS Managed Rules** section, enter `required-tags` into the search box.

5. Choose the **required-tags** rule and choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

6. Configure the following settings on the next screen, leaving the other settings as the default values/selections:

  - For **Name** enter `RequiredTagsCompliance`

  - Remove all values from **Resources** field except for **AWS EC2 Instance**.

    (**NOTE:** In case you accidentally deleted **AWS EC" Instance** resource from the list. You could manually add it from the **Resource type** combo menu)

  - For **Parameters** enter the following:

  **NOTE:** The **tag1Key** field is already pre-populated, please complete the missing tag Key/Values.

| Key       | Value                         |
| --------- | ----------------------------- |
| tag1Key   | `CostCenter`                  |
| tag1Value | `CC1,CC2,CC3`                 |
| tag2Key   | `Environment`                 |
| tag2Value | `Development,Production`      |

**NOTE:** Delete unused **tagKey** and **tagValues** by choosing on <span style="background-color:white; font-weight:bold; font-size:90%; color:#545b64; position:relative; top:-1px; border-color:#545b64; border-radius:2px; border-width:1px; border-style:solid; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;">Remove</span>. Additionally, make sure you used the right casing and the spelling for the values you entered in the previous steps.

7. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

8. In Review and create page, choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span> to save the rule.

In the Rules dashboard, you will see the new **RequiredTagsCompliance** rule does not have status under **Compliance** column, this may take a couple of minutes, At this point **Config** has started to evaluate resources configurations. Move on to the next step; you will review compliance with this rule later in the lab.

### Task 2.2: Add AWS Config Rule to enforce approved Instance Types

The second rule you will establish ensures that your EC2 instances are using an approved instance type. Make sure the selected instance type meets the performance requirements of the supported workload. In addition, that it fits the budget approved to deploy and operate resources in AWS.

9. In the left navigation pane under **AWSConfig**, select **Rules**.

**NOTE:** Be careful not to select Rules under Aggregators.

10. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span>.

11. Select **Add AWS managed rule** for Rule Type.

12. Enter `desired-instance-type` into the search box.

13. Choose the **desired-instance-type** rule and select <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

14. Configure the following settings on the next screen, leaving the other settings as the default values/selections:

  - For **Name** enter `DevelopmentInstanceType`.
  - For **Scope of changes** select **Tags**.
  - For **Tag key** enter `Environment`.
  - For **Tag value** enter `Development`.
  - For **Value** field in the **Parameters** section, enter `t3.small`.

  This setting indicates that the specified instance types, should be used for the instances deployed in your environment that have an **Environment** tag value of **Development**, to avoid unnecessary costs associated using unapproved instance types.

15. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

16. In Review and create page, choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span> to save the rule.

Instead of just identifying the non-compliant resources, you may want to resize the non-compliant instances automatically. This prevents them from incurring in additional costs in your environment. To do this, you are going to implement an automatic remediation so that they instances are resize appropriately.

17. In the left navigation pane under **AWSConfig**, select **Rules**.

**NOTE:** Be careful not to select Rules under Aggregators.

18. Click the radio button next to **DevelopmentInstanceType** rule.

19. Choose <span style="background-color:white; font-weight:bold; font-size:90%; color:#545b64; position:relative; top:-1px; border-color:#545b64; border-radius:2px; border-width:1px; border-style:solid; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;">Actions <i class="fas fa-angle-down"></i></span>, then choose **Manage Remediation**.

**NOTE:** If you get an error stating AWS Config is currently experiencing unusually high traffic, you will need to refresh the page in order to select the **remediation action** below.

- For **Select remediation method**, select `Automatic remediation`.
- For **Remediation action details**, enter `AWS-ResizeInstance` in the search box.
- Select **AWS-ResizeInstance**.
- For **Resource ID parameter** select **InstanceId**.
- For **InstanceType** enter `t3.small`.
- Copy the **LabAutomationRole** ARN value from the navigation panel to the left of these instructions and paste it in the **Value** field next to **AutomationAssumeRole**.

20. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Save changes</span>.

In the Rules dashboard, you will see the **DevelopmentInstanceType** rule has a Compliance status of Evaluating. It sometimes takes a while for AWS Config to evaluate the status of the resources in your environment. In the next task you are going to check and remediate AWS Config findings.