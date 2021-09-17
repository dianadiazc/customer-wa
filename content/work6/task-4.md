+++ 
title = "Task 4: Enable Preventative Controls for Compliance" 
chapter = false 
weight = 4 
+++

Enabling AWS Config will allow you to detect and remediate non-compliant resources in a reactive manner. Now, you will use AWS Identity and Access Management to put proactive controls in place that prevent users from deploying non-compliant resources. With IAM, you can grant different permissions, to different people, for different resources. You will use the capabilities of IAM to ensure that your AP Developers can launch new EC2 instances in the Development environment as needed, but only if they select the appropriate instance type, and configure the required tags at launch to be compliant with your organization’s standards.

### Task 4.1: Review AWS IAM User Group and Policy

To efficiently manage multiple users that perform the same job duties as one, IAM Groups are used. They collectively administer permissions for all users that are members of that group.

1. Open the **IAM Console** by selecting <span style="ssb_services">Services <i class="fas fa-angle-down"></i></span> and typing `iam` in the filter box.

2. Choose **IAM**.

3. In the left menu, select **User groups**.

A user group for AP Developers was created allowing users in that group to deploy EC2 instances that meet certain requirements. This allows you to enable self-service capabilities while maintaining compliance with your documented standards.

4. Choose the **DeveloperGroup** group name link.

5. Select the **Permissions** tab.

This user group has an Inline Policy that grants permissions to the users in the group.

6. Choose the **developer-policy** policy link.

7. Choose the **JSON** tab.

The inline policy will looks similar to the example below.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["ec2:Describe*"],
      "Resource": "*",
      "Effect": "Allow",
      "Sid": "AllowToDescribeAll"
    },
    {
      "Action": ["ec2:RunInstances", "ec2:CreateVolume"],
      "Resource": [
        "arn:aws:ec2:*::image/*",
        "arn:aws:ec2:*::snapshot/*",
        "arn:aws:ec2:*:*:subnet/*",
        "arn:aws:ec2:*:*:network-interface/*",
        "arn:aws:ec2:*:*:security-group/*",
        "arn:aws:ec2:*:*:key-pair/*",
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Effect": "Allow",
      "Sid": "AllowRunInstances"
    },
    {
      "Condition": {
        "StringEquals": {
          "aws:RequestTag/CostCenter": "CC1",
          "aws:RequestTag/Environment": "Development",
          "ec2:InstanceType": "t3.small"
        }
      },
      "Action": ["ec2:RunInstances"],
      "Resource": ["arn:aws:ec2:*:*:instance/*"],
      "Effect": "Allow",
      "Sid": "AllowRunInstancesWithRestrictions"
    },
    {
      "Condition": {
        "StringEquals": {
          "ec2:CreateAction": "RunInstances"
        }
      },
      "Action": ["ec2:CreateTags"],
      "Resource": [
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:network-interface/*"
      ],
      "Effect": "Allow",
      "Sid": "AllowCreateTagsOnlyLaunching"
    }
  ]
}
```

This policy statement allows users in this group to launch an EC2 instance, so long as the instance is a **t3.small** and the instance has been populated with the following tags:

| Key         | Value            |
| ----------- | ---------------- |
| CostCenter  | CC1              |
| Environment | Development      |

8. Choose the **Cancel** link at the bottom of the pop-up window.

### Task 4.2: Add developer1 to the DeveloperGroup Group

Now that you have reviewed the user group and inline policy, you will add the user awsstudent to the group. This will allow the user to create EC2 instances, so long as they are compliant with the policy conditions.

9. In the left menu, choose **User groups**.

10. Choose the **DeveloperGroup** link.

11. Choose <span style="ssb_grey">Add users</span>.

12. Select <i class="far fa-check-square"></i> **developer1**.

13. Choose <span style="ssb_blue">Add users</span>.

`developer1` is now a member of the `DeveloperGroup` group.

**Note:** You will complete the rest of the lab as `developer1`

### Task 4.3: Verify Preventative Controls

With `developer1` now belonging to the DeveloperGroup group, you will want to confirm that the inline policy is restricting permissions as intended.

14. Copy the value of **LoginURL** to the left of these instructions.

15. In a new private window or tab, paste the LoginURL, then press **Enter**.

16. At the Sign-in window, configure:

- **IAM user name:** `developer1`
- **Password:** Paste the value of **DeveloperPassword** located to the left of these instructions.

17. Choose <span style="ssb_blue">Sign in</span>.

18. Open the **EC2 Console** by selecting <span style="ssb_services">Services <i class="fas fa-angle-down"></i></span> and typing `ec2` in the filter box.

19. Choose **EC2**.

20. At the top of the screen, choose the **LabRegion** value located to the left of these instructions.

You need to ensure that you are in the correct region before you create the instance.

21. In the left menu, select **Instances**.

22. Select <span style="ssb_orange">Launch instances</span>.

23. Next to **Amazon Linux 2 AMI**, select <span style="ssb_blue">Select</span>.

24. Select an Instance Type of **t3.small**.

25. Choose <span style="ssb_grey">Next: Configure Instance Details</span>.

On the Instance Details page, you will want to identify the VPC to deploy your new instance in.

26. In the **Network** field, select **wa-lab5-vpc**.

27. Choose <span style="ssb_grey">Next: Add Storage</span>.

No adjustments are required for the storage options for the instance.

28. Choose <span style="ssb_grey">Next: Add Tags</span>.

You will want to add tags to these instances to make sure they are compliant with your organizations published architecture standards. This will avoid the instance from flagging as non-compliant based on the Config rules you have implemented.

29. Choose <span style="ssb_grey">Add Tag</span>.

30. Enter a Key of `Name` and a Value of `My Server`.

31. Choose <span style="ssb_grey">Add another tag</span>.

32. Enter a Key of `Environment` and a Value of `Dev`.

33. Choose <span style="ssb_grey">Add another tag</span>.

34. Enter a Key of `CostCenter` and a Value of `CC1`.

35. Choose <span style="ssb_grey">Next: Configure Security Group</span>.

You will use a security group that is already in place in your environment for this Dev instance.

36. Select the **Select an existing security group** radio button.

37. Select the checkbox for the security group with a description of <i class="far fa-check-square"></i> **Lab5 instance Security Group**.

38. Choose <span style="ssb_blue">Review and Launch</span>.

You will likely receive a warning that you will not be able to connect to this instance. That is ok, as you would not be connecting to this instance using SSH.

39. Choose <span style="ssb_blue">Continue</span>.

40. Verify your configuration choices on the Review page and select <span style="ssb_blue">Launch</span>.

A pop-up window will appear asking you to select a key pair.

41. In the first dropdown of the popup window, select **Proceed without a key pair**.

42. Check <i class="far fa-check-square"></i> to acknowledge that you will not be able to connect to the instance.

43. Choose <span style="ssb_blue">Launch Instances</span>.

You will receive an error message that launch failed. Do you know why?

The reason for failure is that you entered all of the necessary tags, but entered an incorrect value for the Environment tag. You need to enter **Development** instead of Dev.

44. Choose <span style="ssb_grey">Back to Review Screen</span>. so that you can modify the configuration.

45. Choose the **Edit tags** hyperlink towards the bottom of the page.

Now you can modify the incorrect tag that was defined earlier.

46. Change the Environment tag value from Dev to `Development`.

47. Choose <span style="ssb_blue">Review and Launch</span>.

48. Choose <span style="ssb_blue">Launch</span>.

The pop-up window asking you to select a key pair will appear again.

49. In the first dropdown of the popup window, select **Proceed without a key pair**.

50. Check <i class="far fa-check-square"></i> to acknowledge that you will not be able to connect to the instance.

51. Choose <span style="ssb_blue">Launch Instances</span>.

Because you have specified the correct required tag values, you should now receive a message that reads **Your instances are now launching**.

52. Choose <span style="ssb_blue">View Instances</span>.

Here you can view all of the instances running in your account, including a new instance with the appropriate tags that are compliant with your AWS Config rules established earlier in the lab.

---

<i class="far fa-thumbs-up" style="color:blue"></i> Congratulations! You now have finished Lab 5.


Using the appropriate services and resources for your workload is key to cost savings. A well-architected workload uses the most cost-effective resources, which can have a significant and positive economic impact. You also have the opportunity to use managed services to reduce costs. AWS offers a variety of flexible and cost-effective pricing options to acquire instances from EC2 and other services in a way that best fits your needs.