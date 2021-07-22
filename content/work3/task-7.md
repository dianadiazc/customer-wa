+++ 
title = "Task 7: Creating an EC2 Auto Scaling Group"
chapter = false 
weight = 7
+++

An **Auto Scaling group** contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. Amazon EC2 Auto Scaling enables you to take advantage of the safety and reliability of geographic redundancy by spanning Auto Scaling groups across multiple Availability Zones within a Region. 

After completing the steps in this Task, you will have the architecture as in the following diagram:

<img src="../images/lab2-task7.png" alt="drawing" width="800"/>

1. Create Auto Scaling Group

```sh
export asgSubnet1Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-private-subnet-1 --query 'Subnets[*].SubnetId' --output text --region us-west-2` && echo asgSubnet1Id=$asgSubnet1Id >> ~/.bashrc

export asgSubnet2Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-private-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2` && echo asgSubnet2Id=$asgSubnet2Id >> ~/.bashrc

export waLaunchTemplate=`aws ec2 describe-launch-templates --launch-template-names waLaunchTemplate --query 'LaunchTemplates[*].LaunchTemplateId' --output text --region us-west-2` && echo waLaunchTemplate=$waLaunchTemplate >> ~/.bashrc

aws autoscaling create-auto-scaling-group --auto-scaling-group-name "waAutoscaleGroup" --launch-template LaunchTemplateId=$waLaunchTemplate --min-size "2" --max-size "4" --target-group-arns $waTg --vpc-zone-identifier "$asgSubnet1Id,$asgSubnet2Id"
```

2. Go to **EC2** service and validate that a couple of new instances are being created.

<img src="../images/ssm7.png" alt="drawing" width="900"/>

3. From the left pane, select **Load Balancers** and click on **DNS name** icon. 

<img src="../images/dns2.png" alt="drawing" width="800"/>

4. Paste the ELB DNS name in a web browser and insert a couple items to test the application.

<img src="../images/app4.png" alt="drawing" width="800"/>