+++ 
title = "Task 3: Updating SSM Parameter Store database"
chapter = false 
weight = 3 
+++

1. Validate RDS instance endpoint is available (if the output is null please wait a little more, it shoult take 3-4 minutes)

```sh
aws rds describe-db-instances --db-instance-identifier "waDbInstance" --query 'DBInstances[*].Endpoint.Address' --output text --region us-west-2
```

2. Update SSM parameter store

First validate the Parameter Store paramenter value the actual application is using to point to the application database installed in a EC2 instance

```sh
aws ssm get-parameters --names "DbPrivateDns" --output table
```

3. Look for the Value unde "Value" column, this is the DB server private DNS name

Now update the Parameter Store parameter with the RDS instance endpoint the Autoscaling group application instances will use during their bootstrapping

```sh
export rdsEndPoint=`aws rds describe-db-instances --db-instance-identifier "waDbInstance" --query 'DBInstances[*].Endpoint.Address' --output text --region us-west-2`

aws ssm put-parameter --name "DbPrivateDns" --value $rdsEndPoint --overwrite
```

4. Run again the below script to validate the Parameter Store parameter has been updated with the RDS endpoint

```sh
aws ssm get-parameters --names "DbPrivateDns" --output table
```