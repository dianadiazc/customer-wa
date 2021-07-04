+++ 
title = "Task 3: Creating a Resource Group" 
chapter = false 
weight = 3
+++

A *resource group* is a collection of AWS resources in the same AWS Region that match tag-based criteria provided in a search query. A resource group can represent an application, a software component, a business unit, an environment, a team, or even an area of ownership. 

You can use resource groups to perform bulk actions. For example, if you manage large numbers of related resources, such as EC2 instances that make up an application layer, you might need to perform bulk actions on these resources at one time. Other examples of bulk actions include the following:

* Applying updates or security patches.
* Upgrading an application version.
* **Installing software** *(This is the action that we are going to use in this lab).*
* Opening or closing ports to network traffic.
* Collecting specific log and monitoring data.


1. Open the **Resource Groups & Tag Editor** console. Service search box > Resource Group.

<img src="../images/rg1.png" alt="drawing" width="900"/>

2. Select **Create Resource Group**

<img src="../images/rg2.png" alt="drawing" width="600"/>

3. For **Group Type** select "Tag based".

<img src="../images/rg3.png" alt="drawing" width="800"/>

4. Now we are going to config **Grouping criteria**. 

* For *Resource types*, select "AWS::EC2::Instance".

<img src="../images/rg4.png" alt="drawing" width="600"/>

* For *Tags*, select <code>App</code> and <code>Product-Catalog</code>. Clid on "Add". We will use the tags that we created in the previous task. 

<img src="../images/rg5.png" alt="drawing" width="900"/>

Repeat the process using <code>Environment</code> and <code>Production</code>. 

<img src="../images/rg6.png" alt="drawing" width="900"/>

5. Click on **Preview group resources**. You will see both EC2 instances. Those instance will make up your Resource group.

<img src="../images/rg7.png" alt="drawing" width="900"/>


6. For **Group details** type:

* Group name: <code>rg-wa</code>
* Group description: <code>Resource Group for Well-Architected Labs</code>

7. Click on "Create Group". 

<img src="../images/rg8.png" alt="drawing" width="900"/>
