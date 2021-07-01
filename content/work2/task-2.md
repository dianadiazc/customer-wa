+++ 
title = "Task 2: Tagging the EC2 instances" 
chapter = false 
weight = 2 
+++

Amazon Web Services allows customers to assign metadata to their AWS resources in the form
of tags. Each tag is a simple label consisting of a customer-defined key and an optional value
that can make it easier to manage, search for, and filter resources. Tags are a great way to organize AWS resources in the AWS Management Console. 

1. Keep your web server selected, go to **Tags** option and clic on **Manage Tags**.

<img src="../images/tag1.png" alt="drawing" width="900"/>

2.  Select **Add tags** option. You are going to add 2 tags. These tags will be used in the task.

* Tag 1:  Key: type <code>environment</code>, Value: <code>production</code>
* Tag 2:  Key: type <code>application</code>, Value: <code>product-catalog</code>

<img src="../images/tag2.png" alt="drawing" width="800"/>

3. Follow steps **1.** and **2.** for the DB server (wa-db-server)
