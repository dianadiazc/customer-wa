+++
title = "Cost Optimization"
date = 2021-02-17T17:04:42-06:00
weight = 8
chapter = false
pre = "<b>Lab 5:  </b>"
+++

The Cost Optimization pillar includes the ability to run systems to deliver business value at the lowest price point.

<img src="images/cost.png" alt="drawing" width="150"/>

{{% notice note %}}
In order to control costs, **AnyCompany** would like to implement some controls to avoid people to launch big EC2 intances or with optimized resources, especially for non-production environments. 
{{% /notice %}}

## Objective

This lab will guide you through the steps to use AWS Config to enforce tagging for EC2 instances and instance type standardization for non-production environments. The skills you learn will help you control your cost and usage in alignment with the business requirements. You will pay only for the computing resources you consume and need, which is fundamental according to the **Adopt a consumption model** design principle. 


## Services

AWS Config, AWS Identity and Access Management (IAM)

## Duration

Estimated time to complete: 40 min

## Tasks

1. Enable AWS Config

2. Create AWS Config Rules

3. Review and Remediate AWS Config findings

4. Enable Preventative Controls for Compliance

## Architecture

After completing tasks above, you will have the following architecture. 

<img src="images/target-up.png" alt="drawing" width="1200"/>



