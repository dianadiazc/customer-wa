+++ 
title = "Task 1: Checking the existing architecture" 
chapter = false 
weight = 1 
+++

<img src="../images/starting-point.png" alt="drawing" width="600"/>

The product catalog is a Web Application that was recently migrated from On-premises to the AWS Cloud. This is a fundamental application for The New Company customer. Since it was migrated using a simple lift and shift process, into the AWS Cloud this application is made up of two EC2 instances, one for the Web Server and other one for the database (MariaDB). Users access the application through the Internet. 

1. Make sure that your AWS console session is using Oregon region (This lab uses us-east-2 as default region).

<img src="../images/region.png" alt="drawing" width="600"/>

2. Open the EC2 console. Service search box > ECS

<img src="../images/EC2.png" alt="drawing" width="600"/>

You will see two EC2 instances, one for the web server and other one for the database:

<img src="../images/instances.png" alt="drawing" width="600"/>

3.  Now we are going to check that the Application (Product catalog) is up and running. Select your web server instance and copy the public DNS:

<img src="../images/dns.png" alt="drawing" width="600"/>

4. Paste the public DNS in a web browser. You will see that the Product Catalog web application. 

<img src="../images/app.png" alt="drawing" width="600"/>

5. Inser at least 3 products.

<img src="../images/app-names.png" alt="drawing" width="600"/>




