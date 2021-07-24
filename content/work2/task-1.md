+++ 
title = "Task 1: Checking the existing architecture" 
chapter = false 
weight = 1 
+++

<img src="../images/starting.png" alt="drawing" width="600"/>

The product catalog is a web application that was recently migrated from on-premises to the AWS Cloud. This is a fundamental application for The New Company customer. Since it was migrated using a simple lift and shift process into the AWS Cloud, this application consists of two Amazon EC2 instances, one for the Web Server and other for the database (MariaDB). Users access the application via the Internet.

1. Make sure that your AWS console session is using Oregon region. This lab uses Oregon (us-west-2) as the default region.

<img src="../images/region.png" alt="drawing" width="600"/>

2. Open the EC2 console. Service search box > EC2

<img src="../images/EC2.png" alt="drawing" width="600"/>

You will see two EC2 instances, one for the web server and other one for the database:

<img src="../images/instances.png" alt="drawing" width="600"/>

3.  Now we are going to check that the Product catalog web application `(wa-web-server)`  is up and running. Select your web server instance and copy the public DNS:

<img src="../images/dns.png" alt="drawing" width="600"/>

4. Paste the public DNS in a web browser. You will see that the Product Catalog web application. 

{{% notice info %}}
Please ensure that you are using **http** to access the Application, as some browsers use *https* by default.
{{% /notice %}}

<img src="../images/app.png" alt="drawing" width="600"/>

5. Add at least 3 products to the list and,   when complete, leave this browser window open for later reference.

<img src="../images/app-names.png" alt="drawing" width="600"/>




