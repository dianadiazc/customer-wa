+++ 
title = "Task 1: Enable granular logging" 
chapter = false 
weight = 1 
+++

**AWS CloudTrail** is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With AWS CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.

We want to enable detailed, holistic logging and network-based security monitoring.

1. Go to the **CloudTrail** service in the console.

<img src="../images/ct1.png" alt="drawing" width="700"/>

2. When appears, click on *Getting Started*.

We are going to create a trail to capture **All Read/Write** events which would show us every API calls made to our AWS environment from now on.

3. Go to **Create trail**.

<img src="../images/ct2.png" alt="drawing" width="600"/>

{{% notice warning %}}
You will see a warning in your console: *"The option to create an organization trail is not available for this AWS account. Learn more
com.amazonaws.services.organizations.model.AccessDeniedException: You don't have permissions to access this resource. (Service: AWSOrganizations; Status Code: 400; Error Code: AccessDeniedException; Request ID: 0080f181-3022-4e69-af49-9d76a5dabd85; Proxy: null)".*  **You can safely ignore this warning and continue with the next step.**
{{% /notice %}}


4. We should save trail logs for further evaluation, so you would want to create a new S3 bucket and give it a unique name e.g. “cloudsecurity-demo-bucket-{yourname}”.

* Trail Name : `All-API-Commands-across-all-Regions`
* Storage Location :  Select *Create new S3 bucket*
* Trail log bucket and folder : `cloudsecurity-demo-bucket-{myname}`
* Log file SSE-KMS encryption: *Disabled*

<img src="../images/ct3.png" alt="drawing" width="700"/>

Keep other parameters by default and click on **Next**.

{{% notice info %}}
Please ensure S3 buckets must have unique names, so make sure to add your name at the end. They can also only be lower case letters, numbers, “-“, and “.”).
{{% /notice %}}

5. *Choose Log Event:* We have kept default setting here, however you can select the other event types for the different log events you want. We have selected the **Management events** in this case. Click on **Next**.

<img src="../images/ct4.png" alt="drawing" width="600"/>

Give it a final review and select **Create trail**. 

<img src="../images/ct5.png" alt="drawing" width="600"/>

<img src="../images/ct6.png" alt="drawing" width="600"/>

We will come back to look at it later. Monitoring what API calls are made is great, but it’s difficult to convert that into something like Change Management for all infrastructure in the cloud. Is there any service to help us here?

Let us also look into one of the Services called **Config**.

6. Go to **Config** Service.

<img src="../images/ct7.png" alt="drawing" width="800"/>

7. Click on **Get started** and we can start tracking All resources, Including Global Resources.

<img src="../images/ct8.png" alt="drawing" width="600"/>

We would want to store this data in a central bucket as well. Let’s Create a new bucket and use the default to ensure its unique (Note: We could use the bucket we just created, but you would have to add permissions, which would take more time).

8. Let's keep settings parameters by default and click on **Next**.

<img src="../images/ct9.png" alt="drawing" width="800"/>

9. Next, we can choose rules we want to test against, but we can do that later too if we skip it for now. Click on **Next**.

10. Review and **Confirm** these choices to enable Config to monitor all changes to our environment. And we’ll see that in a bit.
Now that we’ve got good logging of the Control Plane (API commands and Changes to the environment), let’s turn on logging of the Data Plane.

<img src="../images/ct10.png" alt="drawing" width="600"/>

{{% notice info %}}
You can close the Welcome box that it is open after the Confirmation. 
{{% /notice %}}

11. Then, let us use a Service like **GuardDuty** to monitor logs in near real time for security anomalies. Go to Service search box > GuardDuty.

<img src="../images/ct11.png" alt="drawing" width="800"/>

12. After **Getting Started** we can quickly enable this service with just one click. It’s that easy. 

<img src="../images/ct12.png" alt="drawing" width="600"/>

13. We are going to **Enable GuardDuty** 30 day free trial. 

<img src="../images/ct16.png" alt="drawing" width="600"/>

We'll check out what GuardDuty is monitoring later in this lab.

{{% notice note %}}
When we looked at on-premises environment, we identified that there are disjointed security tooling, lack of insight into what’s going on in the environment, and difficulty managing change control and permissions in the environment, all led to risks becoming problems pretty fast. With the services we just enabled, we’ll see how we now have complete insight into who’s doing what in the environment, what changes are being made, and when problems start to arise.
{{% /notice %}}