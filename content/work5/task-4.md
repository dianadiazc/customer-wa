+++ 
title = "Task 4: Validate the alarms and policies created" 
chapter = false 
weight = 1 
+++

At the end of this task, we should validate the automated actions we configure and consider to experiment more often with new functionalities, services and technologies.

1.	Open the **CloudShell** console.

<img src="../images/T04S01.png" alt="drawing" width="600"/>

2.	We have a pre created script that you will use to increase the instances CPU% utilization and trigger the scale-out alarm and action. Run this commands from the **CloudShell** console to download the bash script and enable it to be executed.

```sh
curl -o run-stress-test.sh https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/run-stress-test.sh
chmod +x run-stress-test.sh
```
{{% notice note %}}
According to their business growth plans, for **AnyCompany**, this stress test could represent a simulation of the expected traffic that they could have in the near future.
{{% /notice %}}


<img src="../images/T04S02.png" alt="drawing" width="800"/>

3.	This script will use **SSM Run Command** to pass the script execution to the EC2 ASG instances OS, you could verify the instances that are being managed by SSM running the below command.

```sh
aws ssm describe-instance-information --output text --query "InstanceInformationList[*]"
```

4.	You should get a couple of EC2 instances from the command output.

<img src="../images/T04S04.png" alt="drawing" width="800"/>

5.	Now run this command to stress the instances.

```sh
./run-stress-test.sh
```

<img src="../images/T04S05.png" alt="drawing" width="800"/>

6.	This script will run for 5 minutes, please navigate to your AWS CloudWatch dashboard and observe the following:

* The average CPU% Utilization will go up to 100%.

* The **scale-out-alarm** will be triggered.

* The number of healthy host will be increased to 4.

<img src="../images/T04S06_01.png" alt="drawing" width="600"/>

<img src="../images/T04S06_02.png" alt="drawing" width="600"/>

7.	After the script finishes running, the instances count in the auto scaling group and their CPU% utilization will get back to normal.

{{% notice info %}}
One of the more important aspects about monitoring performance and runnnig experiments is that **you can use data to make fact-based decisions about your architecture**. In the case of AnyCompany and according to the insights that you got in this Lab: **What would you recommend to the customer?** If the customer want to meet the demand in the near future, should the customer change the EC2 instance type? Should the customer increase the maximum limit configuration for the EC2 Auto Scaling Group? Are there other activities to do before making decisions?
{{% /notice %}}

---

**Great Job!** You finished this lab, let's wrap up. 

We have worked on the efficient use of computing resources to meet requirements, and how to maintain efficiency as demand changes and technologies evolve. From now on, you should keep reviewing your choices on a regular basis, ensures that you are taking advantage of the continually evolving of AWS Cloud.

When architecting workloads, there are finite options that you can choose from. However, over time, new technologies and approaches become available that could improve the performance of your workload. Fortunately, in the cloud it is much easier to experiment with new features and services.
