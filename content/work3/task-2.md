+++ 
title = "Task 2: Adding RDS subnets to both AZs" 
chapter = false 
weight = 2 
+++

End of task 2 architecture

<img src="../images/lab2-task2.png" alt="drawing" width="800"/>

1. Create RDS subnets (AZ1 and AZ2) and DB instance

```sh
aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.4.0/24" --availability-zone "us-west-2a" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-rds-subnet-1}]'

aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.5.0/24" --availability-zone "us-west-2b" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-rds-subnet-2}]'
```

2. Add new RDS subnets as env vars

```sh
export rdsSubnet1Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-rds-subnet-1 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

export rdsSubnet2Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-rds-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2`
```

3. Associate RDS subnets to private route table

```sh
aws ec2 associate-route-table --subnet-id $rdsSubnet1Id --route-table-id $privateRt
aws ec2 associate-route-table --subnet-id $rdsSubnet2Id --route-table-id $privateRt
```

4. Create RDS subnet group

```sh
aws rds create-db-subnet-group --db-subnet-group-name "wa-rds-subnet-group" --db-subnet-group-description "WA RDS Subnet Group" --subnet-ids $rdsSubnet1Id $rdsSubnet2Id
```

5. Create RDS security group

```sh
aws ec2 create-security-group --description "RDS Security group" --group-name "wa-rds-sg" --vpc-id $VPC
export rdsSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-rds-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2`

export ec2DbSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-database-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2`

aws ec2 authorize-security-group-ingress --group-id $rdsSg --source-group $ec2DbSg --protocol "tcp" --port "3306"
```

6. Create Multi-AZ RDS instance

```sh
aws rds create-db-instance --db-name "WaRdsDb" --db-instance-identifier "waDbInstance" --allocated-storage 20 --db-instance-class db.t3.micro --engine "mariadb" --master-username "masteruser" --master-user-password "WaStr0ngP4ssw0rd" --vpc-security-group-ids $rdsSg --db-subnet-group-name "wa-rds-subnet-group" --multi-az --no-publicly-accessible --backup-retention-period 0
```
