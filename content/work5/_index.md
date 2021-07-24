+++
title = "Performance Efficiency"
date = 2021-02-17T17:04:42-06:00
weight = 7
chapter = false
pre = "<b>Lab 4:  </b>"
+++

The Performance Efficiency pillar includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.


<img src="images/per.png" alt="drawing" width="150"/>


{{% notice note %}}
Starting with the Well-Architected Framework Review executed to our customer, we have the information about the decision to use the t2.micro instance. Also, **The New Company** wants to perform stress tests to be prepared for an increment in the demand in a near future.
Based on than information, the objective of this module is to identify how The New Company can create and operate their infrastructure with the best performance, while maintaining the alignment to the business and technical needs. 
{{% /notice %}}

## Objective

This Lab will guide you through activities to learn how to measure the performance and the behavior of an EC2 auto scaling group.
Remember, if you can't measure it, you can't manage it, if you can't manage it, you can't improve it. 

You will visualize and set thresholds to check the performance for the infrastructure resources using Amazon CloudWatch Dashboards. You will also create alerts to modify the architecture in case a threshold is breached to increase the number of instances or reduce them. Finally, and aligned with the desing principle **"experiment more often"**, you will execute an automated test to validate the performance of the resources. 


## Services

Amazon CloudWatch, AWS Auto Scaling.

## Prerequisites

You will run this Lab at an AWS sponsored workshop then you will be provided with an AWS Account to perform all the tasks in the following section.

You should run **Lab 2: Reliability** in this workshop before performing this Lab. 

## Duration

Estimated time to complete: 40 min

## Tasks

1. [Create the autoscaling alarms](https://main.d2azidedm760yt.amplifyapp.com/work5/task-1/)
2. [Create dynamic scaling policies](https://main.d2azidedm760yt.amplifyapp.com/work5/task-2/)
3. [Create an Amazon CloudWatch Dashboard](https://main.d2azidedm760yt.amplifyapp.com/work5/task-3/)
4. [Validate the alarms and policies created](https://main.d2azidedm760yt.amplifyapp.com/work5/task-4/)
