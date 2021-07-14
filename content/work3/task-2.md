+++ 
title = "Task 2: Deploying Amazon RDS using multi-AZ" 
chapter = false 
weight = 2 
+++

This task will walk you through the steps needed of creating an **Amazon RDS MariaDB - Multi-AZ deployment**. This deployment provide enhanced availability and durability for RDS database (DB) instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ).

{{% notice note %}}
Remember that current customer's database doesn't have high availibility. You are looking for improving reliability for the Application components, which includes the Database. You will use the multi-AZ deployment in a future Task in this Lab to migrate the original Database.
{{% /notice %}} 

After completing the steps in this Lab, you will have the following architecture:

<img src="../images/lab2-task2.png" alt="drawing" width="800"/>

1. Create RDS subnets in both AZs (us-west-2a and us-west-2b).

```sh
aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.4.0/24" --availability-zone "us-west-2a" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-rds-subnet-1}]'

aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.5.0/24" --availability-zone "us-west-2b" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-rds-subnet-2}]'
```

2. Add new RDS subnets as environment variables.

```sh
export rdsSubnet1Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-rds-subnet-1 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

export rdsSubnet2Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-rds-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2`
```

3. Associate RDS subnets to a private route table.

```sh
aws ec2 associate-route-table --subnet-id $rdsSubnet1Id --route-table-id $privateRt
aws ec2 associate-route-table --subnet-id $rdsSubnet2Id --route-table-id $privateRt
```

4. Create RDS subnet group.

```sh
aws rds create-db-subnet-group --db-subnet-group-name "wa-rds-subnet-group" --db-subnet-group-description "WA RDS Subnet Group" --subnet-ids $rdsSubnet1Id $rdsSubnet2Id
```

5. Create RDS Security Group.

```sh
aws ec2 create-security-group --description "RDS Security group" --group-name "wa-rds-sg" --vpc-id $VPC
export rdsSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-rds-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2`

export ec2DbSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-database-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2`

aws ec2 authorize-security-group-ingress --group-id $rdsSg --source-group $ec2DbSg --protocol "tcp" --port "3306"
```

6. Create Multi-AZ RDS instance.

```sh
aws rds create-db-instance --db-name "WaRdsDb" --db-instance-identifier "waDbInstance" --allocated-storage 20 --db-instance-class db.t3.micro --engine "mariadb" --master-username "masteruser" --master-user-password "WaStr0ngP4ssw0rd" --vpc-security-group-ids $rdsSg --db-subnet-group-name "wa-rds-subnet-group" --multi-az --no-publicly-accessible --backup-retention-period 0
```
{{% notice info %}}
Multi-AZ RDS creation will take **~10-15 minutes**. Please go ahead and continue with the next task.
{{% /notice %}}