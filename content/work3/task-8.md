+++ 
title = "Task 8: Creating Route 53 health check"
chapter = false 
weight = 8
+++


Console -> Route53 -> Health checks -> Create health check

**Configure health check**

| Key | Value  |
|---|---|
| Name  | wa-app-health |
| What to monitor | Endpoint  |

**Monitor an endpoint**

| Key | Value  |
|---|---|
| Specify endpoint by | Domain name |
| Protocol | HTTP |
| Domain name * | *ELB DNS name* |
| Path | index.php |

**Advanced configuration**

| Key | Value  |
|---|---|
| Request interval | Fast (10 seconds) |
| Failure threshold * | 1 |

4. Click **Next**

**Get notified when health check fails**

| Key | Value  |
|---|---|
| Create alarm | No |

5. Click on **Create health check**

6. To view the application health status select the health check, and in the below panel click on the **Monitoring** tab, after a couple of minutes you will see the app health check status is `1.0`