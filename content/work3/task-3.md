+++ 
title = "Task 3: Updating SSM Parameter Store database"
chapter = false 
weight = 3 
+++

1. The first step in this task is to validate if the RDS instance URL endpoint is already available, usually takes ~3-4 minutes after the RDS instance creation command. Run the below command to confirm if the RDS endpoint is available

```sh
aws rds describe-db-instances --db-instance-identifier "waDbInstance" --query 'DBInstances[*].Endpoint.Address' --output text --region us-west-2
```
{{% notice warning %}}
If the output of the command above is null please wait a little bit more. After you get the enpoint URL as the command output you can continue with the following lab steps.
{{% /notice %}}


2. Update SSM parameter store

First, validate the Parameter Store parameter value that the actual application is using to point to the application database installed in the EC2 instance (the original database).

```sh
aws ssm get-parameters --names "DbPrivateDns" --output table
```

3. Look for the Value under **Value** column, this is the DB server private DNS name.

<img src="../images/cs5.png" alt="drawing" width="900"/>

Now update the Parameter Store parameter with the RDS instance endpoint (the Autoscaling group application instances will use it during their bootstrapping).

```sh
export rdsEndPoint=`aws rds describe-db-instances --db-instance-identifier "waDbInstance" --query 'DBInstances[*].Endpoint.Address' --output text --region us-west-2` && echo rdsEndPoint=$rdsEndPoint >> ~/.bashrc

aws ssm put-parameter --name "DbPrivateDns" --value $rdsEndPoint --overwrite
```

4. Run again the below script to validate the Parameter Store parameter has been updated with the RDS endpoint

```sh
aws ssm get-parameters --names "DbPrivateDns" --output table
```

<img src="../images/cs6.png" alt="drawing" width="900"/>