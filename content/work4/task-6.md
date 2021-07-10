+++ 
title = "Task 6: Minimize admin access risk" 
chapter = false 
weight = 6 
+++

Finally, let's further reduce administrative risks by reducing access and improving logging. With our current setup, there is still a risk of open administrative ports, right? It's a bigger risk if those ports are open to the internet and a smaller risk if open internally for malware to find. Can we find a way around this requirement?

1.  Let's go back to **VPC** and **Security Groups**.
2.  Open the **Services Server Security Group** and the **Inbound Rules**.
3.  Now, despite the fact that those are made up IPs, you are going to **Edit Rules** and delete all the rules (Click the x on the right). Then **Save** and **Close**.
4.  But with no access, how can we monitor or log into the box if we need to? Our **Service** called **Systems Manager** can help there.
5.  Systems Manager has a feature called **Session Manager** worth checking out.
6.  At **Sessions**, you can **Start a session** with any server with the SSM agent and access to the SSM Service.
7.  We disabled all access to the **Services Server for AZ1**, yet there it is. Let's select it and **Start session**.
8.  Is this a console? For the AWS server? Let's find out.\
    Type:

    >  TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
    >  curl -H "X-aws-ec2-metadata-token: $TOKEN"  http://169.254.169.254/latest/meta-data/instance-id

    Does that instance ID look familiar?

    >  curl -H "X-aws-ec2-metadata-token: $TOKEN"  http://169.254.169.254/latest/meta-data/security-groups

    That looks like the Security Group we modified doesn't it?

    >  ping 8.8.8.8

    Should it work?

    >  curl -H "X-aws-ec2-metadata-token: $TOKEN"  http://169.254.169.254/latest/meta-data/iam/security-credentials/SharedServerConnectivityRole

    Sure looks like an AWS server.

Congratulations! You have successfully set up this AWS environment for strong logging with Cloudtrail and Config, granular communication with Security Groups and NACLs, intelligent threat detection with AWS GuardDuty, and configured your machines to have safe administrative access without requiring access from the public internet.