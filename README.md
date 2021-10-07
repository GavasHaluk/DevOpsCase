# DevOps-Case-Study

For this case study I have chosen to use CodeDeploy, CodePipeline and EC2 to host my webapplication

Step 1 coding the application:

- The first step is to create a webapplication, for this step I haven't spent a lot if time and just used a simple application that displays text.

Step 2 setting up EC2 and IAM users:

- For this step I have created an two IAM users one called EC2SuperUser which has ECS, VPC, EKS, S3, IAM privileges and CodeDeploy privileges.
- After doing so I have created a linux EC2 instance on aws using my newly created user. 
- The installation script for this is as follows:
```
#!/bin/bash
sudo yum -y update
sudo yum -y install ruby
sudo yum -y install wget
cd /home/ec2-user
wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
sudo chmod +x ./install
sudo ./install auto
```
- After the above steps are done all I had left to do was to create tags and a security group
- For the security group I have added HTTP 80 for the internet access and port 3000 to acces the website
- Finally added a keypair for debugging

Step 3 Setting up the CodeDeploy:

- For the CodeDeploy setup I have kept things mostly defauly and i hvae chosen On-premises instances.
- After that I have created a new pipeline for the webapp.
- I have connected the pipeline with Github version 2 where my code is at.
- After giving the neccesary permissions on Github and selectiong the AWS CodeDeploy as my deploy provider the webapp pipeline has been successfully created.

Difficulties and challenges:

- At this point the pipeline is working as intended it deploys from github every time a new push has been made.
- However due to an error on my application_stop script it is failing, I tried deleting it with the same result.
- After researching this it seems that this is a common bug with the CodeDeploy module.

TODO:

- Use a different deployment provider.
