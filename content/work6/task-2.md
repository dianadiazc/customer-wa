+++ 
title = "Task 2: Enable AWS Config" 
chapter = false 
weight = 2 
+++

Now that you have enabled AWS Config, you will establish rules that will check resource compliance with your organization's published architecture standards.

**NOTE:** You may see a note at the top of the screen that a redesigned AWS Config console is available for use. For this lab, please do not use the redesigned console.

### Task 2.1: Add AWS Config Rule to enforce required tags

First, you will create a rule that confirms required tags populated with appropriate values on each of your EC2 instances. Consistent tagging is a useful tool in managing costs associated with running different applications or workloads in your environment. It can also be helpful in allocating costs to different departments that deploy and operate resources in AWS.

1. On the left hand navigation pane, choose **Rules**.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span>.

1. Select **Add AWS managed rule** for Rule Type.

1. In **AWS Managed Rules** section, enter `required-tags` into the search box.

1. Choose the **required-tags** rule and choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. Configure the following settings on the next screen, leaving the other settings as the default values/selections:

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

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. In Review and create page, choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span> to save the rule.

In the Rules dashboard, you will see the new **RequiredTagsCompliance** rule does not have status under **Compliance** column, this may take a couple of minutes, At this point **Config** has started to evaluate resources configurations. Move on to the next step; you will review compliance with this rule later in the lab.

### Task 2.2: Add AWS Config Rule to enforce approved Instance Types

The second rule you will establish ensures that your EC2 instances are using an approved instance type. Make sure the selected instance type meets the performance requirements of the supported workload. In addition, that it fits the budget approved to deploy and operate resources in AWS.

1. In the left navigation pane under **AWSConfig**, select **Rules**.

**NOTE:** Be careful not to select Rules under Aggregators.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span>.

1. Select **Add AWS managed rule** for Rule Type.

1. Enter `desired-instance-type` into the search box.

1. Choose the **desired-instance-type** rule and select <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. Configure the following settings on the next screen, leaving the other settings as the default values/selections:

  - For **Name** enter `DevelopmentInstanceType`.
  - For **Scope of changes** select **Tags**.
  - For **Tag key** enter `Environment`.
  - For **Tag value** enter `Development`.
  - For **Value** field in the **Parameters** section, enter `t3.small`.

  This setting indicates that the specified instance types, should be used for the instances deployed in your environment that have an **Environment** tag value of **Development**, to avoid unnecessary costs associated using unapproved instance types.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Next</span>.

1. In Review and create page, choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Add rule</span> to save the rule.

Instead of just identifying the non-compliant resources, you may want to resize the non-compliant instances automatically. This prevents them from incurring in additional costs in your environment. To do this, you are going to implement an automatic remediation so that they instances are resize appropriately.

1. In the left navigation pane under **AWSConfig**, select **Rules**.

**NOTE:** Be careful not to select Rules under Aggregators.

1. Click the radio button next to **DevelopmentInstanceType** rule.

1. Choose <span style="background-color:white; font-weight:bold; font-size:90%; color:#545b64; position:relative; top:-1px; border-color:#545b64; border-radius:2px; border-width:1px; border-style:solid; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;">Actions <i class="fas fa-angle-down"></i></span>, then choose **Manage Remediation**.

**NOTE:** If you get an error stating AWS Config is currently experiencing unusually high traffic, you will need to refresh the page in order to select the **remediation action** below.

- For **Select remediation method**, select `Automatic remediation`.
- For **Remediation action details**, enter `AWS-ResizeInstance` in the search box.
- Select **AWS-ResizeInstance**.
- For **Resource ID parameter** select **InstanceId**.
- For **InstanceType** enter `t3.small`.
- Copy the **LabAutomationRole** ARN value from the navigation panel to the left of these instructions and paste it in the **Value** field next to **AutomationAssumeRole**.

1. Choose <span style="background-color:#ec7211; font-weight:bold; font-size:90%; color:white; position:relative; top:-1px; padding-top:3px; padding-bottom:3px; padding-left:10px; padding-right:10px;white-space: nowrap">Save changes</span>.

1. In the left navigation pane under **AWSConfig**, select **Rules**.

1. This automatic remediation action will start to evaluate the configurations of EC2 resources with *Key:Value* tags: `Environment:Development`. At this point you will not see any status under the **Compliance** column. The reason is that your EC2 instances are not properly tagged according to the **RequiredTagsCompliance** rule, hence Config cannot determine if the instances have the correct instance type.

1. Now you will add the required tags to the EC2 instanced to get them in *compliance*.

1. Go to Services >> EC2.

1. Mark the checkbox next to the instance with Name `lab5-dev-instance`

1. In the below panel click on the **Tags** tab.

1. To add the required tags, click on **Manage tags**.

1. Add the missing tags according to the below table. Click on **Add tag** to add tag lines.

  **Note:** Do not delete the *Name* Tag

| Key           | Value                         |
| ------------- | ----------------------------- |
| Name          | lab5-dev-instance             |
| `CostCenter`  | `CC1`                         |
| `Environment` | `Development`                 |

1. Now you will add the required tags on the *Prodction* instance. Mark the checkbox next to the instance with Name `lab5-prod-instance`.

1. In the below panel click on the **Tags** tab.

1. To add the required tags, click on **Manage tags**.

1. Add the missing tags according to the below table. Click on **Add tag** to add tag lines.

  **Note:** Do not delete the *Name* Tag

| Key           | Value                         |
| ------------- | ----------------------------- |
| Name          | lab5-prod-instance            |
| `CostCenter`  | `CC2`                         |
| `Environment` | `Production`                  |

1. Now you will validate if the  **RequiredTagsComplaince** rule changes to **Compliant** status. Go back to **Config** service.

1. In the left navigation pane under **AWSConfig**, select **Rules**.

1. A couple of minutes after you added the required tags in the instances, the **Compliance** status of the **RequiredTagsCompliance** rule must change to **Compliant**.

  **Note:** Rule **DevelopmentInstanceType** must have changed to a **Compliant** status after tagging the instances and confirmed the EC2 instance has the expected instance type.

1. Now it's time to test the **DevelopmentInstanceType** rule. You will change the instance type so you could test the remediation action you configured. Go to the EC2 service.

1. On the left pane, click on **Instances**

1. Look for the instance `lab5-dev-instance` and mark the checkbox next to it.

1. Click on **Instance state**, select **Stop instance** and confirm your action.

1. Wait a few seconds until the instance state changes to **Stopped** (You may need to click on the *refresh* button next to **Connect**).

1. Once the EC2 instance is in a **Stopped** state you could change the instance type. Click on **Actions** >> **Instance settings** >> **Change instance type**.

1. In the **Change instance type** window, below **Instance type**, select `t3.medium`

1. Click **Apply**

1. Now start the EC2 instance, mark the checkbox next to the instance, click **Instance state** >> **Start instance**

1. This change will trigger the **Config** rule remediation action, it will take aprox 4-5 minutes for the rule to change the instance status automatically, from shutting down, to resize back to `t3.small` and finally start the instance again, so it can enter in a **Compliant** state according to the rule you have created.

---