+++ 
title = "Task 7: Create Auto Scaling Group"
chapter = false 
weight = 7
+++

End of task architecture

<img src="../images/lab2-task7.png" alt="drawing" width="800"/>

1. Create Auto Scaling Group

```sh
export asgSubnet1Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-private-subnet-1 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

export asgSubnet2Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-private-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

export waLaunchTemplate=`aws ec2 describe-launch-templates --launch-template-names waLaunchTemplate --query 'LaunchTemplates[*].LaunchTemplateId' --output text --region us-west-2`

aws autoscaling create-auto-scaling-group --auto-scaling-group-name "waAutoscaleGroup" --launch-template LaunchTemplateId=$waLaunchTemplate --min-size "2" --max-size "4" --target-group-arns $waTg --vpc-zone-identifier "$asgSubnet1Id,$asgSubnet2Id"
```

2. Go to EC2 and validate a couple of new instances are being created

3. Paste the ELB DNS name in a web browser to test the application


