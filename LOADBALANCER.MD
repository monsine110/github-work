## How to apply a load balancer to instances in AWS ##
1. **Create a Target Group**:
   - Define the group of instances or IP addresses that the load balancer will route traffic to.
   - Configure health checks to monitor the status of targets.

2. **Launch EC2 Instances**:  on this hands-on i'm launching two instances
   - On the AWS management console, navigate to instance and click on launch instance
   ![alt text](<Screenshot 2025-04-21 154149.png>)

   - add your name and tag and number of instances
   ![alt text](<Screenshot 2025-04-21 154329.png>)

   - choose your AMI (AMASON MACHINE IMAGE)
    ![alt text](<Screenshot 2025-04-21 154455.png>)

   - Here i choose red hat as my AMI
    ![alt text](<Screenshot 2025-04-21 154524.png>)

   - Select your istance type, here i use t3 small
    ![alt text](<Screenshot 2025-04-21 154628.png>)

   - select your key pair, if you don't have create one,
   click to learn how to create
    ![alt text](<Screenshot 2025-04-21 154717.png>)

   -  select your security group, if you don't have create one,
   click to learn how to create,
   here my security group is launch-wizard-1 which allows inbound traffic from http and ssh
   ![alt text](<Screenshot 2025-04-21 154831.png>)

   - click on advance details and navigate to user data  then add your bootstrap text
![alt text](<Screenshot 2025-04-21 155019.png>)

   here i used
    "#!/bin/bash
   yum install httpd -y
   service httpd start
   chkconfig httpd on
   hostname > /var/www/html/index.html" as my user data which install a webserver, start it , configure it and serve the hostname 
   - click on launch instance and your two instances will be launched
   ![alt text](<Screenshot 2025-04-21 155327.png>)
   

3. **Set Up the Load Balancer**:
   - on the aws console navigae to load balancer and click on create load balancer
   ![alt text](<Screenshot 2025-04-21 155356.png>)

   - Choose the type of load balancer (e.g., Application Load Balancer for HTTP/HTTPS traffic).
   ![alt text](<Screenshot 2025-04-21 155433.png>)

   here i choosed a classic load balancer
   click on classic load balancer and click on create
   ![alt text](<Screenshot 2025-04-21 155456.png>)

   - Configure the load balancer with name, security groups, listeners, and routing rules. etc
     - select your name and scheme,
   for now your scheme should be internet facing
   ![alt text](<Screenshot 2025-04-21 160410.png>)

     - make sure it is available in all availability zone available
   ![alt text](<Screenshot 2025-04-21 155637.png>)

     - select your security group
  ![alt text](<Screenshot 2025-04-21 155739.png>)

   - set your advance health check settings
   ![alt text](<Screenshot 2025-04-21 155923.png>)


4. **Register Targets**:
   - Add your EC2 instances or IP addresses to the target group.
   ![alt text](<Screenshot 2025-04-21 160010.png>)

   set your timeout(draining interval) in the attribute
   ![alt text](<Screenshot 2025-04-21 160103.png>)

5. **add your tag and create your load balancer**
![alt text](<Screenshot 2025-04-21 160523.png>)

6.  **Test the Load Balancer**:
   - Access the DNS name of the load balancer to verify traffic distribution and health checks.
   by copying the DNS name and accessing it on the browser
   ![alt text](<Screenshot 2025-04-21 161406-1.png>)

   ![alt text](<Screenshot 2025-04-21 161305-1.png>)

   we can see the load balancer is now distributing traffic to the instances



