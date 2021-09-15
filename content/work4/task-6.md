+++ 
title = "Task 5: Minimize admin access risk" 
chapter = false 
weight = 5 
+++

Finally, let's further reduce administrative risks by reducing access and improving logging. With our current setup, there is still a risk of open administrative ports, right? It's a bigger risk if those ports are open to the internet and a smaller risk if open internally for malware to find. Can we find a way around this requirement?

1. Let's go back to **VPC** and **Security Groups**.

<img src="../images/ssm1.png" alt="drawing" width="600"/>

2. Open the **wa-asg-sg**.

<img src="../images/ssm2.png" alt="drawing" width="900"/>

3. Check the **Inbound Rules**. There is no rule to access the instances using SSH protocol (Port 22).

<img src="../images/ssm3.png" alt="drawing" width="800"/>

4. But with no access, how can we monitor or log into the instance if we need to? Our **Service** called **AWS Systems Manager** can help there. You are already familiar with this service because you used it in Lab 1.

<img src="../images/ip9.png" alt="drawing" width="800"/> 

5. Systems Manager has a feature called **Session Manager** worth checking out.

<img src="../images/ssm4.png" alt="drawing" width="600"/>

6. Click on **Start session**.

<img src="../images/ssm5.png" alt="drawing" width="600"/>

7. Remember that we are using Amazon Linux 2 instances, they have SSM agent installed by default. According to that, you can start a session an access the instances. Select one instance and click on **Start session**.

<img src="../images/ssm6.png" alt="drawing" width="900"/>

Another tab/window will be opened in your browser:

<img src="../images/ssm7.png" alt="drawing" width="350"/>

8. Is this a console? For the AWS server? Let's find out.

    Type:

    ```
    TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
    curl -H "X-aws-ec2-metadata-token: $TOKEN"  http://169.254.169.254/latest/meta-data/instance-id
    ```

    Does that instance ID look familiar?

    ```
    curl -H "X-aws-ec2-metadata-token: $TOKEN"  http://169.254.169.254/latest/meta-data/security-groups
    ```

    That looks like the Security Group we checked, doesn't it?

    ```
    ping 8.8.8.8
    ```

Should it work?

Sure looks like an AWS server!

---
**Congratulations! :)** You have successfully set up this AWS environment for strong logging with AWS Cloudtrail and AWS Config, granular communication with Security Groups and NACLs, intelligent threat detection with AWS GuardDuty, and configured your machines to have safe administrative access without requiring access from the public internet.
