+++ 
title = "Task 8: Creating Route 53 health check"
chapter = false 
weight = 8
+++

**Amazon Route 53 health checks** monitor the health and performance of your web applications, web servers, and other resources. Each health check that you create can monitor one of the following:

* The health of a specified resource, such as a web server
* The status of other health checks
* The status of an Amazon CloudWatch alarm

In this task you will configure a health check to monitor the EC2 failure injection that you will test in the last activity of this Lab. 

1. Go to **Amazon Route 53** service. 

<img src="../images/r53-1.png" alt="drawing" width="600"/> 

2. Click on **Health checks** and later on **Create health check**.

<img src="../images/r53-2.png" alt="drawing" width="500"/>

3. Use the information in tables below to configure the health check.

**Configure health check**

| Key | Value  |
|---|---|
| Name  | wa-app-health |
| What to monitor | Endpoint  |

<img src="../images/r53-3.png" alt="drawing" width="600"/>

**Monitor an endpoint**

| Key | Value  |
|---|---|
| Specify endpoint by | Domain name |
| Protocol | HTTP |
| Domain name * | *ELB DNS name* |
| Path | index.php |

<img src="../images/r53-4.png" alt="drawing" width="600"/>

**Advanced configuration**

| Key | Value  |
|---|---|
| Request interval | Fast (10 seconds) |
| Failure threshold * | 1 |

<img src="../images/r53-5.png" alt="drawing" width="600"/>

4. Click on **Next**.

5. For **Create alarm**, select *No*. Click on **Create health check**.

<img src="../images/r53-6.png" alt="drawing" width="600"/>

6. To view the application health status select the health check, and in the below panel click on the **Monitoring** tab, after a couple of minutes you will see the app health check status is `1.0`

<img src="../images/r53-7.png" alt="drawing" width="600"/>