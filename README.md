In this project, I evolved the architecture of a Wordpress application from a single instance to a scalable and reliant architecture using AWS RDS, EFS, ASG and ALB.

## What I Learnt

 - RDS
 - Elastic File System
 - Auto Scaling Groups
 - Application Load Balancer
 - Systems Manager Parameter Store

## Process

1. An EC2 instance is provisioned and Wordpress is installed it. The wp-config file is configured to use the DB username and DB password stored in SSM Parameter Store. There are many drawbacks with this:

   i. The application and the database are on the same instance, neither can scale without the other
   ii. The IP of the instance is hardcoded into the database
   iii. The application and the database were built manually
  
2. In this stage, a launch template was created to automate the build of Worpress. The configuration steps were added to Userdata within so that the steps need not be done manually.

3. In this stage, the database was split from the EC2 instance and was changed to RDS running a MySQL engine. The data was migrated from the existing MariaDB on the instance to RDS.

4. In this stage, an EFS file system was created to store the wordpress locally stored media. This could be shared by multiple instances created in future steps.

5. In this stage, an Load Balancer was added along with an Auto Scaling Group with a scaling policy. 