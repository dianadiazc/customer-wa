+++
title = "Performance Efficiency"
date = 2021-02-17T17:04:42-06:00
weight = 7
chapter = false
pre = "<b>Lab 4:  </b>"
+++

The Performance Efficiency pillar includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.


<img src="images/per.png" alt="drawing" width="150"/>

https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.pillar.performance.en.html

## Objective

Starting with the Well-Architected Framework Review executed to our customer, we have the information about the decision to use the t2.micro instance. Also, The New Company wants to perform stress tests to be prepared for an increment in the demand in a near future.
Based on than information, the objective of this module is to identify how The New Company can create and operate their infrastructure with the best performance, while maintaining the alignment to the business and technical needs. 

But first we need to measure the performance and the behavior of our infrastructure resources.
Remember, if you can't measure it, you can't manage it, if you can't manage it, you can't improve it. 

That's why we will work on how to visualize and set thresholds to identify the best performance for our infrastructure resources with Amazon CloudWatch Dashboards, we are also going to create alerts to modify the architecture in case a threshold is breached to increase the number of instances or reduce them. 

Finally, we will execute automated tests to validate the performance of the resources. This is a way we can experiment more often to carry out comparative testing using different types of instances, storage, or configurations based in the business and technical needs.

For more information about the design principles like **Experiment more often**, consult the white paper.
https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/design-principles.html

## Services

Amazon CloudWatch, AWS Auto Scaling.

## Tasks

1. Create the autoscaling alarms.
2. Create dynamic scaling policies.
3. Create an Amazon CloudWatch Dashboard.
4. Validate the alarms and policies created.
