+++ 
title = "Task 3: Creating visuals in QuickSight" 
chapter = false 
weight = 4 
+++

In this task you will use the new **Dataset** to create four visualizations from the Cost and Usage Report (CUR) data. You will build the following dashboard:

<img src="../images/qs-final-dash.png" alt="drawing" width="800"/>

---

#### Visual #1: Monthly expense per AWS service

From the dataset, for this visualization, we will use the following fields (or columns of data):

| Field | Definition |
|---|---|
| *line_item_blended_cost*  | The average cost incurred for each service SKU across an organization multiplied by the amount of usage that you incurred during the specified time period |
| *product_servicecode* | AWS service name |

1. Let's create your first visual...

    <img src="../images/qs-visual-ready.png" alt="drawing" width="600"/>

2. You will use two fields from the CUR dataset

	* line_item_blended_cost

	* product_servicecode

3. Scroll down the **Fields list** until you find `line_item_blended_cost` and click on the field to add it to the graph. Optionally you could type the field name in the Fields search box.

    <img src="../images/qs-addblendedcost.png" alt="drawing" width="300"/>

    After that, you will see the monthly total expenditure in the account in the graph. 

<img src="../images/qs-blendedcostingraph.png" alt="drawing" width="700"/>

4. Now, click on the field `product_servicecode`. You could scroll the list or type it in the search box. 

    You can see steps 3 and 4 in the following gif:

<img src="../images/video.gif" alt="drawing" width="900"/>

This is the expected updated graph view:

<img src="../images/qs-samplegraph1.png" alt="drawing" width="450"/>

{{% notice info %}}
Note: These values and fields are the same you will find in an AWS invoice. You will notice a **ComputeSavingsPlans** item in the graph. In this lab scenario the EC2 total expense amount would be the sum of **ComputeSavingPlans** plus **AmazonEC2**. For further information regarding Savings Plans please visit: https://aws.amazon.com/savingsplans/
{{% /notice %}}

---

#### Visual #2: Monthly cost per EC2 instance

In this case, we will use the following fields (or columns of data):

| Field | Definition |
|---|---|
| *line_item_blended_cost*  | The average cost incurred for each service SKU across an organization multiplied by the amount of usage that you incurred during the specified time period |
| *line_item_resource_id* | IDs of the resources provisioned |
| *line_item_line_item_type* | The type of charge covered by this line item. Possible types are the following: Credit, DiscountedUsage, Fee, Refund, RIFee, Tax, Usage, SavingsPlanUpfrontFee, SavingsPlanRecurringFee, SavingsPlanCoveredUsage and SavingsPlanNegation |
| *line_item_usage_type* | The usage details of the line item. For example, USW2-BoxUsage:m2.2xlarge describes an M2 High Memory Double Extra Large instance in the US West (Oregon) Region |

6. Now you will create a visual to show the monthly cost per EC2 instance, you will use this fields from the CUR dataset:

	* line_item_blended_cost

	* line_item_resource_id

    * line_item_line_item_type

    * line_item_usage_type

7. From the top left of your browser, click on **+ Add**, from the drop down menu click on **Add visual**

    <img src="../images/qs-addvisual.png" alt="drawing" width="300"/>

8. You will see a new blank graph added.

    {{% notice warning %}}
Make sure the graph you are working on is selected, it should be highlighted with blue border lines
{{% /notice %}}

9. From the fields list, search and click on `line_item_blended_cost` to add it to the graph.

10. Add a second field to the graph, search and click `line_item_resource_id` to add the field to the graph

11. You will see a graph will **all** the resources in the account and their monthly cost:

<img src="../images/ec2-nofilter.png" alt="drawing" width="500"/>

12. To narrow the information displayed you will use **Filters**, so you can visualize only the data you are interested in.

    You will use 2 different fields as filters:

    * **line_item_line_item_type**: Get the total EC2 expense, considering Savings Plans coverage and uncovered usage.

    * **line_item_usage_type**: Sum all the instance types in the account, in this case we have **t2.large** and **t3.xlarge** instances.

12. From the left menu, click on **Filter**, then click on **Create one...**.

    <img src="../images/qs-addfilter.png" alt="drawing" width="280"/>

13. From the menu displayed type `line_item_line_item_type` in the search box.

    <img src="../images/qs-typefilter.png" alt="drawing" width="280"/>

14. Click on the **Field** displayed.

15. Below the **Filters** options, click on the filter you just added.

    <img src="../images/qs-clickfilter.png" alt="drawing" width="280"/>

1. From the Filter options displayed, click on **Select all** to DE-SELECT all the options and just mark the **SavingsPlanCoveredUsage** and **Usage** checkboxes.

    <img src="../images/qs-filteroptions1.png" alt="drawing" width="280"/>

16. Click **Apply** at the buttom.

17. Now click on **Exit filter edit**

    <img src="../images/qs-exitfilteredit.png" alt="drawing" width="350"/>

18. Now you will create a second filter, click the plus sign next to **Filters**.

    <img src="../images/qs-addfilter2.png" alt="drawing" width="280"/>

19. From the filters menu, type `line_item_usage_type` in the search box.

20. Click on the filter displayed.

21. Click on the filter you just created.

    <img src="../images/qs-secondfilter1.png" alt="drawing" width="280"/>

22. From the values displayed, click on **Select all** to DE-SELECT all values.

23. Select just **BoxUsage:t2.large** and **BoxUsage:t3.xlarge**

    <img src="../images/qs-justboxusage.png" alt="drawing" width="220"/>

24. Click **Apply**

25. You will see the graph will be updated just showing cost data from three EC2 instances.

26. For better visualization now you will change the graph visualization type. From the left menu, click on **Visualize**

 <img src="../images/ec2-instances.png" alt="drawing" width="400"/>

27. Under **Visual types**, click on the *donut chart* option.

    <img src="../images/qs-donut.png" alt="drawing" width="280"/>

28. You will notice how the graph is updated.

    <img src="../images/qs-donut2.png" alt="drawing" width="600"/>

    So far, your dashboard should look like in the following picture:

<img src="../images/dash-2graphs.png" alt="drawing" width="600"/>
    

{{% notice info %}}
Note: The values showed in this graph does not include cost of the EBS volumes associated with the EC2 instances
{{% /notice %}}

---

#### Visual #3: Savings Plan monthly savings

For this visualization, we will use the following fields (or columns of data):

| Field | Definition |
|---|---|
| *line_item_blended_cost*  | The average cost incurred for each service SKU across an organization multiplied by the amount of usage that you incurred during the specified time period |
| *line_item_line_item_type* | The type of charge covered by this line item. Possible types are the following: Credit, DiscountedUsage, Fee, Refund, RIFee, Tax, Usage, SavingsPlanUpfrontFee, SavingsPlanRecurringFee, SavingsPlanCoveredUsage and SavingsPlanNegation |

29. You will now create a visual with amount of money saved by the customer's Savings Plan. You will use this fields from the CUR dataset:

	* line_item_blended_cost

    * line_item_line_item_type

30. From the top left of your browser, click on **+ Add**, from the drop down menu click on **Add visual**

31. From the *Fields list*, select and click on `line_item_blended_cost` to add it to the graph

32. You will see the amount of expense for all the AWS services consumed in the account, to get the savings amount you need to narrow your search adding a filter. From the left menu, click on **Filter**, then click on **Create one...**.

    <img src="../images/qs-addfilter.png" alt="drawing" width="280"/>

33. From the menu displayed type `line_item_line_item_type` in the search box.

    <img src="../images/qs-typefilter.png" alt="drawing" width="280"/>

34. Click on the **Field** displayed.

35. Below the **Filters** options, click on the filter you just added.

    <img src="../images/qs-clickfilter.png" alt="drawing" width="280"/>

36. From the Filter options displayed, click on **Select all** to DE-SELECT all the options and just mark the **SavingsPlanNegation** and **SavingsPlanRecurringFee** checkboxes.

    <img src="../images/qs-savings-filter1.png" alt="drawing" width="280"/>

37. Click **Apply** at the buttom. You have created a visualization with the monthly Savings Plan savings in the account.

    What's the logic in applying those fields in the filter? Here are the fields definitions:

    | Field | Definition |
    |---|---|
    | *SavingsPlanRecurringFee*  | Recurring charges that correspond with your No Upfront or Partial Upfront Savings Plan |
    | *SavingsPlanNegation* | Offset cost associated with the corresponding Savings Plan covered usage item (Always a negative value) |

    Adding this two fields to the filter will sum the amount of money the customer is being charged in the period for the Savings Plan commitment plus the amount of money that is being discounted. Resulting in a negative value.

    For further information visit: https://docs.aws.amazon.com/cur/latest/userguide/cur-sp.html

38. You could change the value format, from left panel click on **Visualize** and below **Fields list** type `line_item_blended_cost`, move your mouse over the field displayed and three dots will show up, click on them...

    <img src="../images/qs-change-value-type.png" alt="drawing" width="280"/>

39. Click on **Show as: Number**, then click on **Currency**

    <img src="../images/qs-set-currency.png" alt="drawing" width="450"/>

    Your visualization should look like:

    <img src="../images/blended-cost.png" alt="drawing" width="350"/>

    And your dashaboard should look like:

    <img src="../images/dashboard-3graphs.png" alt="drawing" width="700"/>
    
    

---

#### Visual #4: Monthly expense per EBS volume type

In this case, we will use the following fields (or columns of data):

| Field | Definition |
|---|---|
| *line_item_blended_cost*  | The average cost incurred for each service SKU across an organization multiplied by the amount of usage that you incurred during the specified time period |
| *line_item_usage_type* | The usage details of the line item. For example, USW2-BoxUsage:m2.2xlarge describes an M2 High Memory Double Extra Large instance in the US West (Oregon) Region |  

40. You will now create a visual with the monthly expense on EBS volumes, per volume type. To create this visualization you will use this fields

	* line_item_blended_cost

	* line_item_usage_type

41. From the top left of your browser, click on **+ Add**, from the drop down menu click on **Add visual**

42. From the *Fields list*, select and click on `line_item_blended_cost` to add it to the graph. You could scroll down the list or type it in the search box.

43. Now also add to the graph the field `line_item_usage_type` from the *Fields list*.

44. You will get this graph.

    <img src="../images/qs-graph4-pre.png" alt="drawing" width="400"/>

45. You have to narrow the items listed with a filter to just show the EBS volume usage types. From the left menu, click on **Filter**, then click on **Create one...**.

46. From the menu displayed, type `line_item_usage_type` in the search box.

47. Click on the **Field** displayed.

48. Below the **Filters** options, click on the filter you just added.

49. From the Filter options displayed, click on **Select all** to DE-SELECT all the options and just mark the **EBS:VolumeUsage.sc1**, **EBS:VolumeUsage.gp2** and **EBS:VolumeUsage** checkboxes.

    Note: **EBS:VolumeUsage** refers to the previous generation HDD EBS volume.

50. Click **Apply** at the buttom to update the graph

51. For better visualization now you will change the graph visualization type. From the left menu, click on **Visualize**

52. Under **Visual types**, click on the *pie chart* option.

    <img src="../images/qs-pie.png" alt="drawing" width="280"/>

53. You will notice how the graph is updated.

    <img src="../images/qs-pie2.png" alt="drawing" width="400"/>

54. Finally you could change the graph labels to better identify the information displayed. On each graph click on the *titles* to change them.

    Sugested *titles*:

    * Visual #1: Monthly expense per AWS service

    * Visual #2: Monthly expense per EC2 instance

    * Visual #3: Savings Plan monthly savings

    * Visual #4: Monthly expense per EBS volume type

This is the final dashboard:

<img src="../images/qs-final-dash.png" alt="drawing" width="800"/>

{{% notice tip %}}
You could find further details about the AWS Cost and Usage Reports data dictionary in the documentation: https://docs.aws.amazon.com/cur/latest/userguide/data-dictionary.html
{{% /notice %}}

**Congratulations**, you have finished the Lab 5 and the Well-Architected Workshop!

---

Once you have this kind of analysis, you will want to add more measuring and monitoring controls so that you can get better insights for IT costs on workloads, which is aligned with the **Analyze and attribute expenditure** desing principle.

Using the appropriate services and resources for your workload is key to cost savings. A well-architected workload uses the most cost-effective resources, which can have a significant and positive economic impact. You also have the opportunity to use managed services to reduce costs. AWS offers a variety of flexible and cost-effective pricing options to acquire instances from EC2 and other services in a way that best fits your needs.