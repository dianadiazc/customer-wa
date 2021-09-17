+++ 
title = "Task 3: Review and Remediate AWS Config findings" 
chapter = false 
weight = 3 
+++

Now that you have created your AWS Config rules, you will review the results of each rule to determine which resources are non-compliant.

1. In the left navigation pane under **AWSConfig**, select **Rules**.

2. You will see that **RequiredTagsCompliance** rule has a *Noncompliant* status. This is because the Development instance is not properly tagged according to the parameters we established in Task 2.1 of this Lab. You will also see that **DevelopmentInstanceType** rule does not have any Compliance status. In this case, it is because Config cannot determine if the instances have the correct instance type, due to the lack of appropriate tags.

3. Now you will add the required tags to the EC2 instance to get it in *compliance*.

4. Go to Services >> EC2.

5. Mark the checkbox next to the instance with Name `lab5-dev-instance`

6. In the below panel click on the **Tags** tab.

7. To add the required tags, click on **Manage tags**.

8. Add the missing tags according to the below table. Click on **Add tag** to add tag lines.

  **Note:** Do not delete the *Name* Tag

| Key           | Value                         |
| ------------- | ----------------------------- |
| Name          | lab5-dev-instance             |
| `CostCenter`  | `CC1`                         |
| `Environment` | `Development`                 |

For this lab purposes, we are assuming that *Production* tags are correct, because they are part of an EC2 Auto Scaling group. We will focus on Development environments.

9. Now you will validate if the  **RequiredTagsCompliance** rule changes to **Compliant** status. Go back to **Config** service.

10. In the left navigation pane under **AWSConfig**, select **Rules**.

11. A couple of minutes after you added the required tags in the instances, the **Compliance** status of the **RequiredTagsCompliance** rule must change to **Compliant**.

**Note:** Note that rule **DevelopmentInstanceType** should have a **Non-Compliant** status, because according to the rule configuration in Task 2.2, a Development environment must use t3.small as instance type, and in this case it is using a t3.medium type.

12.  Click on **DevelopmentInstanceType**. You will see that the Automatic remediation is in place. In **Resources in scope**, the status should be "Action execution queued.." This means that `lab5-dev-instance` is beign stopped to change the instance type to "t3.small"

13. Go to EC2 service. On the left pane, click on **Instances**. Look for the instance `lab5-dev-instance`.

14. Verify "Instance state" status and "Instance type". At some point instance must be "running" and using a "t3.small" type. 

15. Go back to Config service. Check again **Rules**. Now the **Compliance** status for both rules should be *Compliant*.


---