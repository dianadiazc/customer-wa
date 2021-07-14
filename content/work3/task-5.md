+++ 
title = "Task 5: Database migration with SSM Run Command"
chapter = false 
weight = 5
+++

1. Create IAM policy to add to the DB server EC2 instance role, so the DB server could pull the RDS endpoint from parameter store and the RDS instance password from Secrets Manager

```sh
curl -o wa-db-migration-policy-doc.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/wa-db-migration-policy-doc.json
aws iam create-policy --policy-name wa-parameter-policy --policy-document file://wa-db-migration-policy-doc.json
aws iam attach-role-policy --role-name wa-lab-ssm-ec2-role --policy-arn arn:aws:iam::$awsAccount:policy/wa-parameter-policy
```

1. Go to **Systems Manager**

2. From the left panel click on **Run Command**

3. Click on *Run command*

4. In the **Command document** search box, type: `AWS-RunShellScript` and hit **Enter**

5. Click on the radio button next to **AWS-RunShellScript**

6. In the **Command parameters** section, paste the below commands. Note that we are using Secrets Manager (created at lab deployment) to pull the RDS Database masteruser password and Parameter Store (also precreated at lab launch) to pull the RDS instance endpoint

```sh
#!/bin/bash
mysqldump sample > backup.sql
export rdsendpoint=`aws ssm get-parameter --name DbPrivateDns --query 'Parameter.Value' --region us-west-2 --output text`
export user=masteruser
export rdspasswd=`aws secretsmanager get-secret-value --secret-id rdsPassword --query 'SecretString' --output text --region us-west-2`
mysql -h $rdsendpoint -u $user -p$rdspasswd -e "CREATE DATABASE sample;"
mysql -h $rdsendpoint -u $user -p$rdspasswd -e "USE sample;source backup.sql;"
mysql -h $rdsendpoint -u $user -p$rdspasswd -e "CREATE USER 'tutorial_user'@'%' IDENTIFIED BY 'WaFram3w0rk';"
mysql -h $rdsendpoint -u $user -p$rdspasswd -e "GRANT SELECT, INSERT, UPDATE, DELETE ON *.* TO 'tutorial_user'@'%' WITH GRANT OPTION;"
mysql -h $rdsendpoint -u $user -p$rdspasswd -e "FLUSH PRIVILEGES;"
```

7. In the **Targets** section select the DB server `wa-db-server`

8. Click on **Run**

9. Database data has been migrated to the RDS instance, you could now stop EC2 instances `wa-web-server` and `wa-db-server` from the EC2 console
