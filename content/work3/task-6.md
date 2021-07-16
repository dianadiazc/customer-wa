+++ 
title = "Task 6: Creating Launch Template"
chapter = false 
weight = 6
+++

You can create a **launch template** that contains the configuration information to launch an instance. Launch templates enable you to store launch parameters so that you do not have to specify them every time you launch an instance.  In this step, you are going to create a *Launch Template* to specify configuration parameters for launching instances with EC2 Auto Scaling Groups (ASG).

1. Back in CloudShell, create an instance role for the Launch Template

```sh
curl -o wa-asg-assume-role-policy-doc.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/wa-asg-assume-role-policy-doc.json

curl -o wa-asg-policy-doc.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/wa-asg-policy-doc.json

aws iam create-policy --policy-name wa-asg-policy --policy-document file://wa-asg-policy-doc.json
aws iam create-role --role-name wa-asg-instance-role --assume-role-policy-document file://wa-asg-assume-role-policy-doc.json
export awsAccount=`aws sts get-caller-identity --query "Account" --output text`
aws iam attach-role-policy --role-name wa-asg-instance-role --policy-arn arn:aws:iam::$awsAccount:policy/wa-asg-policy
aws iam attach-role-policy --role-name wa-asg-instance-role --policy-arn arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore
aws iam attach-role-policy --role-name wa-asg-instance-role --policy-arn arn:aws:iam::aws:policy/CloudWatchAgentServerPolicy
aws iam create-instance-profile --instance-profile-name "wa-asg-instance-profile"
aws iam add-role-to-instance-profile --instance-profile-name "wa-asg-instance-profile" --role-name "wa-asg-instance-role"
```

2. Create a security group for the Launch Template

```sh
aws ec2 create-security-group --description "Launch Template Security group" --group-name "wa-asg-sg" --vpc-id $VPC

export asgSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-asg-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2` && echo asgSg=$asgSg >> ~/.bashrc

aws ec2 authorize-security-group-ingress --group-id $asgSg --source-group $albSg --protocol "tcp" --port "80"
```

3. Add ASG security group as ingress source to RDS security group.

```sh
aws ec2 authorize-security-group-ingress --group-id $rdsSg --source-group $asgSg --protocol "tcp" --port "3306"
```

4. Create the Launch Template.

```sh
curl -o waLaunchTemplate-source.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/waLaunchTemplate-source.json

envsubst < "waLaunchTemplate-source.json" > "waLaunchTemplate.json"

aws ec2 create-launch-template --launch-template-name "waLaunchTemplate" --launch-template-data file://waLaunchTemplate.json
```
