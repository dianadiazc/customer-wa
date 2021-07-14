+++ 
title = "Task 9: Nuking the web-app"
chapter = false 
weight = 9
+++

1. Run this commands to terminate autoscaling instances

```sh
instances=`aws ec2 describe-instances --filters Name=tag:Name,Values=wa-auto-scale-group --query 'Reservations[*].Instances[*].InstanceId' --output text`

aws ec2 terminate-instances --instance-ids $instances
```

2. Go to Route53 to monitor the time the application comes back online

3. (Optional) Force RDS instance failover

```sh
aws rds reboot-db-instance --db-instance-identifier "waDbInstance" --force-failover
```

4. Also monitor the amount of time the application takes to go back online after RDS failover

### LAB END