+++
title = "Introduction"
date = 2021-02-17T17:04:42-06:00
weight = 2
chapter = false
+++

In this workshop, you are going to learn about the **AWS Well-Architected Framework** focusing on a hands-on experience. The five labs in this Workshop are intended to guide you through the AWS Well-Architected pillars and how to improve an architecture using different strategies and AWS services.

These labs are designed *to be completed in sequence*, and the full set of instructions are documented below. Read and follow along to complete the labs. 

## The context

You work for an AWS Partner. Now you have a new customer, **The New Company**, a retail business. One of the main Apps for The New company is a *product catalog*, a web application that they recently migrated to the AWS Cloud from their On-prem environment for **testing** purposes. Even though the Application is functional, The New Company people want to have an architecture with best practices applied because they are planning to go live in **production** in 2 months.  They are looking for an architecture that meet performance requirements, mitigate risks and save money. For them is crucial to use automation. 

The following is the initial architecture that you have found. Your mission is to improve it applying some of the Well-Architected principles according to the company needs. 

<img src="images/starting-point.png" alt="drawing" width="600"/>

## Architecture review

You have proposed to the customer a Well-Architected Review (WAR) to understand better the current status and their needs. After that review, you have identified the following insights:

1. They are doing a lot of operational tasks manually. The customer wants to automate the process to have visibility about some important performance metrics, like memory or disk utilization.

1. It is clear for the customer that they need to have a High Available architecture for the production environment. 

1. Security is their number 1 priority. The more insights they can have available related to this topic, the better.

1. They are not sure about the decision that they made when they chose a t2.micro instance to run the application. Performance is something that they do not want to sacrifice. 

1. How much they are going to pay definitely matters. The New Company people want to optimize as much as they can the use of the resources. For instance, before the go live, they would like to automate the process for shutting down resources not needed when they are not working. 

## Target Architecture1

After a Well-Architected Review (WAR), you and The New Company have been defined a Target Architecture. This architecture will help the customer to achieve their initial objectives. You are going to pass through the five Well-Architected pillars to implement the following architecture:

<img src="images/target.png" alt="drawing" width="1100"/>


## Labs:

This Workshop is made up of five Labs structured around the five pillars of the [Well-Architected Framework](https://aws.amazon.com/well-architected):

-   [Operational Excellence](https://wellarchitectedlabs.com/operational-excellence/)
-   [Reliability](https://wellarchitectedlabs.com/reliability/)
-   [Security](https://wellarchitectedlabs.com/security/)
-   [Performance Efficiency](https://wellarchitectedlabs.com/performance-efficiency/)
-   [Cost Optimization](https://wellarchitectedlabs.com/cost/)









	

