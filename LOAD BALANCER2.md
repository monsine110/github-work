# Integrating load balancers with an auto-scaling group ensures efficient distribution of traffic while dynamically scaling server instances based on demand. Here’s a step-by-step guide to implement this setup #
## Step-by-Step Method ##

1. ## create a launch template ##
- On the aws console navigate to launch template and click on lauch template

- put the launch template name and version
![alt text](<Screenshot 2025-04-21 163808.png>)

- input your tag
![alt text](<Screenshot 2025-04-21 164105.png>)
- select you AMI (Amason Machine Image)
![alt text](<Screenshot 2025-04-21 164158.png>)
![alt text](<Screenshot 2025-04-21 164242.png>)
- select your instance type and your key pair (create a new key pair if you don't have)
![alt text](<Screenshot 2025-04-21 164418.png>)
- select your security group (create if you don't have)
![alt text](<Screenshot 2025-04-21 164451.png>)
-  click on advance details and navigate to user data  then add your bootstrap text
 here i used

    "#!/bin/bash
   yum install httpd -y
   service httpd start
   chkconfig httpd on
   hostname > /var/www/html/index.html" as my user data which install a webserver, start it , configure it and serve the hostname 
   - click on launch templates to launch your template
   ![alt text](<Screenshot 2025-04-21 165259.png>)
2. **Set Up the Load Balancer**:
   - on the aws console navigae to load balancer and click on create load balancer
   ![alt text](<Screenshot 2025-04-21 155356.png>)

   - Choose the type of load balancer (e.g., Application Load Balancer for HTTP/HTTPS traffic).
   ![alt text](<Screenshot 2025-04-21 155433.png>)

   - here i choosed a classic load balancer
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


   - set your timeout(draining interval) in the attribute
   ![alt text](<Screenshot 2025-04-21 160103.png>)

   - add your tag and create your load balancer**
![alt text](<Screenshot 2025-04-21 160523.png>)


3. ## Set Up Your Auto Scaling Group ##
- on the aws console, navigate to the autoscaling group and click on create auto scaling group
- add the name , launch template and the version
![alt text](<Screenshot 2025-04-21 165554.png>)

- select all availabilty zones available and click next
![alt text](<Screenshot 2025-04-21 165641.png>)

- attach your load balancer by selecting from classic load balancer
![alt text](<Screenshot 2025-04-21 165809.png>)

- turn on elastic load balancing health check and set your Health check grace period and click on next
![alt text](<Screenshot 2025-04-21 165921.png>)

- set your scaling limit and set your average CPU utilization and the time for your instance warm up and click next
![alt text](<Screenshot 2025-04-21 170212.png>)

![alt text](<Screenshot 2025-04-21 170347.png>)

- add your tags and click on next
![alt text](<Screenshot 2025-04-21 170633.png>)

- review and create auto scaling group
![alt text](<Screenshot 2025-04-21 170648.png>)

## CHECKING OR TRIGGERING THE AUTOSCALING ##
To check or trigger the auto scaling, we have to simulate the CPU utilization to be greater than 70% i.e we set the CPU utilization to be 70%,
 To do the we have to loging the instance on mobaxterm application (download if you dont have)
- on the mobaxterm homepage click on session and click on SSH
![alt text](<Screenshot 2025-04-21 171621.png>)

- copy your instance ip and paste it on remote host, write the username as ec2-user because all instance in the aws has ec2-user as the username, then select your private key and press ok
![alt text](<Screenshot 2025-04-21 171734.png>)

- your instance will be logged in your mobaxterm 
![alt text](<Screenshot 2025-04-21 171753.png>)

- type the top command to see the CPU utilization

![alt text](image.png)
- use this command to simulate the CPU usage
" sudo yum install https://dl.fedoraproject.org/pub/epel/9/Everything/x86_64/Packages/e/epel-release-9-9.el9.noarch.rpm -y

sudo yum install stress -y

sudo stress --cpu 80 "
- this is the first command it finds the location of the package
![alt text](<Screenshot 2025-04-21 174132.png>)

- second command install the package
![alt text](<Screenshot 2025-04-21 174307.png>)

- third command simulate the CPU to 80%
![alt text](<Screenshot 2025-04-21 174618.png>)

- use the "top" command to see the CPU usage
![alt text](<Screenshot 2025-04-21 174636.png>)

- navigate to the AWS console, other instances will be created after some minutes
![alt text](<Screenshot 2025-04-21 175541.png>)

-  Access the DNS name of the load balancer to verify traffic distribution and health checks.
   by copying the DNS name and accessing it on the browser
    ![alt text](<Screenshot 2025-04-21 161406-1.png>)

![alt text](<Screenshot 2025-04-21 161305-1.png>)
