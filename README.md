# Terraform-AWS-VPC-Setup
Step-by-Step Guide to Create a custom VPC with two subnets: a Public and a Private Subnets Using Terraform


Introduction
Creating a custom VPC on AWS using Terraform as an Infrastructure as Code (IaC) tool, is a powerful approach to provision and manage such a robust Cloud Infrastructure. Deploying and managing it can be complex and time-consuming, but Terraform enables us to automate the process, in a consistent, efficient and repeatable way, reducing human errors.
This comprehensive step-by-step guide walks you through the process of  creating a custom VPC on AWS with two subnets: a Public and a Private Subnets using Terraform. From defining the configuration files to running Terraform workflow commands-line and understanding overall how to build a VPC, the role of each resource and how they function together. In this lab, we will be using tools like : Terraform, AWS VPC, Subnets, Route Tables, IGW, NAT Gateway. The aim of this lab is to : 
Understand how to define a custom VPC in Terraform’s Configuration files: 
Create and separate public and private subnets
Connect to the internet using Internet Gateway and NAT Gateway
Understand how routing works in AWS
Create a custom VPC infrastructure on AWS using Terraform workflow commands-line: terraform init, terraform plan, terraform apply, terraform destroy.
Prerequisites :

In order to proceed to the lab, we need to make sure beforehand to : 
Install Terraform and AWS CLI. 
Configure AWS credentials (aws configure).
Create a new working directory : vpc-lab2 and get inside it.
Inside the folder, create the configuration files : main.tf  variables.tf  outputs.tf


Step-by-Step Instructions : 
Step 1: Define the Provider
On your main.tf file, write the code below. This tells Terraform to use AWS as a provider and the region where all the resources will 
be created.


Step 2: Create a VPC
On your main.tf file, add the code below. This will create a virtual network on AWS.




Step 3: Create Public and Private Subnets
On your main.tf file, add the code below. This tells terraform to configure a Public subnet that gets internet access directly.  And a Private subnet that stays internal — no direct access.


Step 4: Create an Internet Gateway
On your main.tf file, add the code below. This tells Terraform to configure an Internet Gateway that the Public subnet will use to access the internet.





Step 5: Public Route Table
On your main.tf file, add the code below. This tells terraform to configure a public route that sends all internet traffic (0.0.0.0/0) through the Internet Gateway.



Step 6: NAT Gateway (for Private Subnet)
On your main.tf file, add the code below. In order to create first, an Elastic IP for NAT.





Then to create the NAT Gateway itself. The NAT Gateway lets the private subnet reach the internet securely.





Step 7: Private Route Table
On your main.tf file, add the code below. This code gives internet access only from the private subnet via NAT — no direct exposure.



Step 8: Outputs (Optional but Helpful)
On your outputs.tf file, write the code below. The output.tf configuration file is optional but helpful, it allows users to understand the configuration and review its expected outputs.





Step 9: Deploy 
Now that we have defined the configuration files, we will deploy the infrastructure.
Run terraform init command : to Initialize the working directory/project, downloads the necessary plugins and prepare terraform.

Run terraform plan command : to preview what changes will happen, before Terraform applies them. 




Run terraform apply command : to apply the changes and build the infrastructure.
Type yes when prompted.










Check your infrastructure on AWS Console. The VPC was created as well as its components : 

VPC




Subnets : a Public subnet and a Private subnet.


Route Tables : a Private Route Table and a Public Route Table


Internet Gateway


Nat Gateway

Step 10 : Destroy (Cleanup)
Run terraform destroy command : to delete the infrastructure and removes all the resources managed by terraform.
Type yes when prompted.






Check your infrastructure on AWS Console. The VPC was deleted as well as its components.


Summary
This breakdown provides a step-by-step guide to create a Virtual Private Cloud (VPC) on AWS using Terraform. By completing this lab, we had an overview on how to : 

Define a custom VPC in Terraform’s Configuration files from creating and separating public and private subnets, to connecting to the internet using Internet Gateway and NAT Gateway, and understanding how routing works in AWS.
Create a custom VPC infrastructure on AWS using Terraform workflow commands-line : terraform init, terraform plan, terraform apply, terraform destroy.
Building Infrastructure with Terraform as an IaC tool is an approach that not only provision, manage, and replicate cloud resources in a predictable and automated way. But also, reduces manual errors and enhances the scalability and maintainability of the infrastructure. This approach of building infrastructure using IaC, demonstrated how it can simplify and automate the process of deploying and managing a well-structured private network environment that requires high security and scalability, but also more complex cloud infrastructures. 
Reflection Questions :

What was one thing you found difficult in this lab?
One thing I have found challenging in this lab, was to understand how the VPC’s route tables are configured and defined in the terraform configuration file.  Configuring them manually on the AWS console is assimilated but how they are defined on the main.tf was a little challenging to understand.

Can you explain VPC and subnets in your own words?
Virtual Private Cloud (VPC) is a private network on the AWS Cloud. It is a virtual, secure and isolated infrastructure that allows us to run the cloud resources in order to deploy Applications.
Subnets are one of the components of the VPC. It is a smaller section of the network. There are public and private subnets. Workloads that need direct access to the internet are placed on Public subnets, like web servers. While workloads that contain sensitive data are placed on Private subnets that do not have direct access to the internet, resources in the private, like databases and backends.
Why is it important to destroy unused infrastructure?
Destroying unused infrastructure is important for many reasons : for cost savings, security and resource management reasons.
Cost Savings : cleaning up the unused resources, avoiding being charged for them.
Security: unused resources can be exposed to eventual attacks, if they are not actively used and supervised.
Resource management: cleaning up the unused resources can help us manage our environment better, avoiding any confusion and complexity in the infrastructure. 

Mock Interview Questions : 
What is a VPC and why is it important?
Virtual Private Cloud (VPC) is a private network on the AWS Cloud. It is a virtual, secure and logically isolated infrastructure that allows us to define and control your own virtual network. Its components consist of : subnets, route tables, internet gateway, nat gateway, security groups and NACLs. It is important because it enables us to deploy applications in a secure and private environment over the cloud. Allowing public facing and private resources to coexist in a well-structured network.

What is the difference between a public and a private subnet?
Subnets are one of the components of the VPC. It is a smaller section of the network. There are public and private subnets: 
Workloads that need direct access to the internet are placed on Public subnets, like web servers. While workloads that contain sensitive data are placed on Private subnets that do not have direct access to the internet, resources in the private subnet can be accessed only from the VPC, like databases and backends.
Public Subnet : is a subnet where resources have direct access to the internet, through an Internet Gateway.
Private Subnet : is a subnet where resources do not have direct access to the internet, such databases and backends. They can be accessed through a Nat Gateway.
The main difference between them is that the public subnet has a route to the internet through an internet gateway, while the private subnet does not have a route to the internet. They can be accessed through a nat gateway, placed in the public subnet. 
Why use a NAT Gateway?
The NAT Gateway allows resources in a private subnet to have indirect access to the internet. It is used because it allows private resources to communicate with the internet securely, without being exposed to incoming traffic from the internet.
What does a Route Table do?
A Route Table is a set of rules (routes) that determine and control where the traffic coming from subnets is directed within the VPC.  Public Route tables are associated with a Public subnet, they determine where traffic from the public subnet is directed, usually to an Internet gateway for external access. Private Route tables are associated with a Private subnet, they determine where traffic from the private subnet is directed, usually to a Nat gateway that translates the IP address and forward the traffic to the internet. 



