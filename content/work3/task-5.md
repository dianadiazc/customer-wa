+++ 
title = "Task 5: Database migration with SSM Run Command"
chapter = false 
weight = 5
+++

In this task you will migrate Application Database from the EC2 instance to Amazon RDS MariaDB - Multi-AZ Deployment. You will perform this activity using *Run command* option from Systems Manager. 

{{% notice warning %}}
Before starting this task, please **make sure that you have inserted data in your database**. Plase, go to the Web Application and check that you have items included.
{{% /notice %}}

<img src="../images/app3.png" alt="drawing" width="800"/> 


1. Create an IAM policy to add to the DB server EC2 instance role, so the DB server could pull the RDS endpoint from parameter store and the RDS instance password from Secrets Manager.


```sh
curl -o wa-db-migration-policy-doc.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/wa-db-migration-policy-doc.json
aws iam create-policy --policy-name wa-parameter-policy --policy-document file://wa-db-migration-policy-doc.json
aws iam attach-role-policy --role-name wa-lab-ssm-ec2-role --policy-arn arn:aws:iam::$awsAccount:policy/wa-parameter-policy
```

2. Go to **Systems Manager**

<img src="../images/ip9.png" alt="drawing" width="800"/> 

3. From the left panel click on **Run Command** and click on *Run command*

<img src="../images/ssm1.png" alt="drawing" width="900"/> 

4. In the **Command document** search box, type: `AWS-RunShellScript` and hit **Enter**. Click on the radio button next to **AWS-RunShellScript**.

<img src="../images/ssm2.png" alt="drawing" width="800"/> 

7. In the **Command parameters** section, paste commands below. Note that we are using Secrets Manager (created at lab deployment) to pull the RDS Database masteruser password and Parameter Store (also precreated at lab launch) to pull the RDS instance endpoint.

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
<img src="../images/ssm3.png" alt="drawing" width="800"/> 

8. In the **Targets** section select **Choose instances manually" and later the DB server `wa-db-server`.

<img src="../images/ssm4.png" alt="drawing" width="800"/> 

9. Click on **Run**.

10. Database has been migrated to the RDS instance.

<img src="../images/ssm5.png" alt="drawing" width="800"/> 

11. At this point, you could *stop* EC2 instances `wa-web-server` and `wa-db-server` from the EC2 console.

<img src="../images/ssm6.png" alt="drawing" width="800"/> 

