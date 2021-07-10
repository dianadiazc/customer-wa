+++
title = "Operational Excellence"
date = 2021-02-17T17:04:42-06:00
weight = 4
chapter = false
pre = "<b>Lab 1:  </b>"
+++

The Operational Excellence pillar includes the ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value. 

<img src="images/operational-ex.png" alt="drawing" width="150"/>

{{% notice note %}}
Remember that one of the insights found in the Well-Architected Framework Review (WAFR) was about the need to automate tasks. The New Company people are performing a lot of operational tasks manually. One of the issues they mentioned was a lack of visilibility into important metrics like memory and disk utilization for the Amazon EC2 instances. They would like an automated process to get that information. Additionally, they need a centralized log monitoring for the DB and App instances. 
{{% /notice %}}

## Objective

In this Lab, you will use AWS Systems Manager according to the **“Perform operations as code”** design principle. You will create a Resource Group with both Amazon EC2 instances and use the “Run command” option in SSM to install the Amazon CloudWatch agent for collecting logs and getting some additional metrics. The tasks in this Lab will guide you through the steps to achieve this objective.

## Services

Amazon EC2, AWS Systems Manager, Amazon CloudWatch

## Tasks

1. Checking the existing architecture
1. Tagging the Amazon EC2 instances
1. Creating a Resource Group
1. Enabling SSM for Amazon EC2 instances
1. Installing Amazon CloudWatch agent with SSM
1. Starting Amazon CloudWatch Agent
1. Validating custom metrics and log groups


