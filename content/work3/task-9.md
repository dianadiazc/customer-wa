+++ 
title = "Task 9: EC2 test resiliency"
chapter = false 
weight = 9
+++

**Failure injection** (also known as chaos testing) is an effective and essential method to validate and understand the resiliency of your workload and is a recommended practice of the AWS Well-Architected Reliability Pillar. Here you will initiate one failure scenario and assess how your system reacts.

## Test preparation

1. Open a web browser using the ELB DNS name to monitor application connectivity:

<img src="../images/chaos1.png" alt="drawing" width="600"/>

2. Navigate to the **EC2** console at and click Instances in the left pane.

There are two EC2 instances running with a name beginning with `wa-auto*`. For these EC2 instances note:

* Each has a unique Instance ID
* There is one instance per each Availability Zone
* Both instances are healthy

<img src="../images/chaos2.png" alt="drawing" width="900"/>

3. Open up two more console in separate tabs/windows. From the left pane, open **Target Groups** and **Auto Scaling Groups** in separate tabs. You now have three console views open, we will check them later in this Task.

<img src="../images/chaos3.png" alt="drawing" width="200"/>


## EC2 Failure injection

4. Go back to **AWS CloudShell**. Run this commands to get instances launched by the Auto Scaling group.

```sh
aws ec2 describe-instances --filters Name=tag:Name,Values=wa-auto-scale-group --query 'Reservations[].Instances[*].{InstanceID:InstanceId,Type:InstanceType,AZ:Placement.AvailabilityZone,PrivateIP:PrivateIpAddress,Subnet:SubnetId,Time:LaunchTime,State:State.Name}' --output table
```

The output should look like:

<img src="../images/ec2-1.png" alt="drawing" width="1000"/>

5. Choose one of the instance IDs and replace it in the following command. This command will **terminate** the instance that you choose. This will be an **EC2 failure injection**, which simulates a critical problem with one of the two web servers used by your service.

```sh
aws ec2 terminate-instances --instance-ids <YOUR-INSTANCE-ID>
```

<img src="../images/ec2-2.png" alt="drawing" width="800"/>

{{% notice warning %}}
If you get the error message "Credentials were refreshed, but the refreshed credentials are still expired." after running this command, close CloudShell window and open it again.
{{% /notice %}}

6. Go to the web browser with the Application that you already have open. The Application should be responding normaly.

<img src="../images/chaos1.png" alt="drawing" width="600"/>

7. Take a look at your EC2 instances. Make sure the filter **Instance state:Running** is removed. After one minute of running the *terminate* command you will see one instance changing its state to **shutting-down** and then **Terminated**. Make sure you refresh the page to see the updated instances information.

<img src="../images/chaos4.png" alt="drawing" width="900"/>

8. Go to the **Target Groups** console you already have open. Select `waAutoscale-tg` and click on **Targets** and observe:

* Status of the instances in the group. The load balancer will only send traffic to *healthy* instances. You will have just one Target and its status should be *healthy*. 

* When the auto scaling launches a new instance, it is automatically added to the load balancer target group.

* In the screen cap below the unhealthy instance is the newly added one. The load balancer will not send traffic to it until it is completed initialized. It will ultimately transition to healthy and then start receiving traffic.

* Note the new instance was launched in the same Availability Zone as the terminated one. Amazon EC2 Auto Scaling automatically maintains balance across all of the Availability Zones that you specify.

<img src="../images/ec2-3.png" alt="drawing" width="1000"/>

9. Go to the **Auto Scaling Groups console** you already have open. Click on the **Activity** tab and observe:

* First, an instance was taken out of service in response to an EC2 health check indicating it has been terminated or stopped.

* Later on, an instance was started in response to a difference between desired and actual capacity, increasing the capacity from 1 to 2.

<img src="../images/ec2-8-v2.png" alt="drawing" width="900"/>

10. Go to Route53 to monitor the application health status.

<img src="../images/ec2-4.png" alt="drawing" width="900"/>

No application downtime was observed during the test. 


-----

**Congrats :)**. You have finished the second Lab of this workshop!

Deploying multiple servers and Elastic Load Balancing enables a service to recover after the loss of an instance with no availability disruptions as traffic from user is automatically routed to healthy instances. Amazon Auto Scaling ensures unhealthy hosts are removed and replaced with healthy ones to maintain high availability.

Availability Zones (AZs) are isolated sets of resources within a region, each with redundant power, networking, and connectivity, housed in separate facilities. Each Availability Zone is isolated, but the Availability Zones in a Region are connected through low-latency links. AWS provides you with the flexibility to place instances and store data across multiple Availability Zones within each AWS Region for high resiliency.