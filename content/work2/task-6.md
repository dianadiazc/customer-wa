+++ 
title = "Task 6: Starting Amazon CloudWatch Agent" 
chapter = false 
weight = 6 
+++

Follow these steps to start the agent using Systems Manager Run Command:

1. Open the **Systems Manager** console and in the navigation pane, choose **Run Command** and then **Run Command**.

<img src="../images/rc1.png" alt="drawing" width="600"/> 

2. In the *Command document* list search and later select `AmazonCloudWatch-ManageAgent`.

<img src="../images/rc2.png" alt="drawing" width="800"/> 

3. In the *Command parameters*:

* For *Action*, choose **Configure**
* For *Optional Configuration Source* list, select **ssm**
* For *Optional Configuration Location* box, enter the name of the Parameter Store which is storing the agent configuration file. The parameter name is `wa-cw-config-file-httpd-mariadb`. We have precreated the parameter for you as part of the lab environment initial deployment.
* For Optional Restart, select **yes**

This is the JSON agent configuration file stored in SSM Parameter store. Please take a minute to review it and follow with the next step.

```
    {
        "agent": {
            "metrics_collection_interval": 60,
            "run_as_user": "root"
        },
        "logs": {
            "logs_collected": {
                "files": {
                    "collect_list": [
                        {
                            "file_path": "/var/log/messages",
                            "log_group_name": "messages",
                            "log_stream_name": "{instance_id}"
                        },
                        {
                            "file_path": "/var/log/httpd/access_log",
                            "log_group_name": "httpd_access_log",
                            "log_stream_name": "{instance_id}"
                        },
                        {
                            "file_path": "/var/log/mariadb/wa-db-server.log",
                            "log_group_name": "db_general_query_log",
                            "log_stream_name": "{instance_id}"
                        },
                        {
                            "file_path": "/var/log/mariadb/mariadb.log",
                            "log_group_name": "mariadb_log",
                            "log_stream_name": "{instance_id}"
                        }
                    ]
                }
            }
        },
        "metrics": {
            "append_dimensions": {
                "AutoScalingGroupName": "${aws:AutoScalingGroupName}",
                "ImageId": "${aws:ImageId}",
                "InstanceId": "${aws:InstanceId}",
                "InstanceType": "${aws:InstanceType}"
            },
            "metrics_collected": {
                "disk": {
                    "measurement": [
                        "used_percent"
                    ],
                    "metrics_collection_interval": 60,
                    "resources": [
                        "*"
                    ]
                },
                "mem": {
                    "measurement": [
                        "mem_used_percent"
                    ],
                    "metrics_collection_interval": 60
                },
                "statsd": {
                    "metrics_aggregation_interval": 60,
                    "metrics_collection_interval": 10,
                    "service_address": ":8125"
                }
            }
        }
    }
```   
<img src="../images/rc3.png" alt="drawing" width="900"/> 

4. In the *Targets* area:

* For Targets opion, select "Choose a resource group"
* For Resource group, select `rg-wa` (This was the resource group that you created in the Task 3)

<img src="../images/rc4.png" alt="drawing" width="700"/> 

5. Click on **Run**

You will see the Run Command result. Use the refresh option to update the status until it displays Success. You have now installed and started the CloudWatch agent on both EC2 instances using the “Perform Operations as Code” design principle.

<img src="../images/rc5.png" alt="drawing" width="800"/> 

{{% notice tip %}}
Reference: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance-fleet.html
{{% /notice %}}