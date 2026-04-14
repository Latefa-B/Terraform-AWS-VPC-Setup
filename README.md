# Step-by-Step Guide to Create a custom VPC with two subnets: a Public and a Private Subnets Using Terraform
Creating a custom VPC on AWS using Terraform as an Infrastructure as Code (IaC) tool, is a powerful approach to provision and manage such a robust Cloud Infrastructure. Deploying and managing it can be complex and time-consuming, but Terraform enables us to automate the process, in a consistent, efficient and repeatable way, reducing human errors.
This comprehensive step-by-step guide walks you through the process of  creating a custom VPC on AWS with two subnets: a Public and a Private Subnets using Terraform. From defining the configuration files to running Terraform workflow commands-line and understanding overall how to build a VPC, the role of each resource and how they function together. In this project, we will be using tools like : Terraform, AWS VPC, Subnets, Route Tables, IGW, NAT Gateway. The aim of this project is to : 
- Understand how to define a custom VPC in Terraform’s Configuration files: 
- Create and separate public and private subnets
- Connect to the internet using Internet Gateway and NAT Gateway
- Understand how routing works in AWS
- Create a custom VPC infrastructure on AWS using Terraform workflow commands-line: terraform init, terraform plan, terraform apply, terraform destroy.

## Prerequisites 
In order to proceed to the lab, we need to make sure beforehand to : 
- Install Terraform and AWS CLI. 
- Configure AWS credentials (aws configure).
- Create a new working directory : vpc-lab2 and get inside it.
- Inside the folder, create the configuration files : main.tf  variables.tf  outputs.tf
<img width="961" height="149" alt="1" src="https://github.com/user-attachments/assets/69eb4678-5a19-4a4e-a289-6f12495b14a3" />

## Step-by-Step Instructions 
# Step 1: Define the Provider
On your main.tf file, write the code below. This tells Terraform to use AWS as a provider and the region where all the resources will be created.
<img width="808" height="121" alt="2" src="https://github.com/user-attachments/assets/9e98ade6-a2df-427f-996e-f1a17a5617bc" />

# Step 2: Create a VPC
On your main.tf file, add the code below. This will create a virtual network on AWS.
<img width="916" height="235" alt="3" src="https://github.com/user-attachments/assets/6534ce46-3ee7-4d53-af42-2773de9ad7f3" />

# Step 3: Create Public and Private Subnets
On your main.tf file, add the code below. This tells terraform to configure a Public subnet that gets internet access directly.  And a Private subnet that stays internal — no direct access.
<img width="992" height="501" alt="4" src="https://github.com/user-attachments/assets/500bf29b-ee63-4deb-becc-f9cda94446f6" />


# Step 4: Create an Internet Gateway
On your main.tf file, add the code below. This tells Terraform to configure an Internet Gateway that the Public subnet will use to access the internet.
<img width="853" height="622" alt="5" src="https://github.com/user-attachments/assets/c8d62b18-5b00-4e24-8b29-6d40082d7a1e" />

# Step 5: Public Route Table
On your main.tf file, add the code below. This tells terraform to configure a public route that sends all internet traffic (0.0.0.0/0) through the Internet Gateway.
<img width="705" height="824" alt="6" src="https://github.com/user-attachments/assets/ea950dab-7f8e-4290-bc63-18d4282a1cfc" />

# Step 6: NAT Gateway (for Private Subnet)
- On your main.tf file, add the code below. In order to create first, an Elastic IP for NAT.
- Then to create the NAT Gateway itself. The NAT Gateway lets the private subnet reach the internet securely.
<img width="1160" height="240" alt="7" src="https://github.com/user-attachments/assets/4c2fccb1-d1c4-419e-b013-4dca85f4dcb1" />

# Step 7: Private Route Table
On your main.tf file, add the code below. This code gives internet access only from the private subnet via NAT — no direct exposure.
<img width="658" height="279" alt="8" src="https://github.com/user-attachments/assets/63642bba-f853-44e3-a1a6-a62af335339e" />

# Step 8: Outputs (Optional but Helpful)
On your outputs.tf file, write the code below. The output.tf configuration file is optional but helpful, it allows users to understand the configuration and review its expected outputs.
<img width="1045" height="224" alt="9" src="https://github.com/user-attachments/assets/7f2c4b35-6606-4e8e-b8d0-5778f8533b0f" />

# Step 9: Deploy 
Now that we have defined the configuration files, we will deploy the infrastructure.
- Run terraform init command : to Initialize the working directory/project, downloads the necessary plugins and prepare terraform.
<img width="596" height="312" alt="10" src="https://github.com/user-attachments/assets/f002bfb9-7d24-4f39-93cf-ed0d40ce1804" />

- Run terraform plan command : to preview what changes will happen, before Terraform applies them. 
<img width="1195" height="870" alt="11" src="https://github.com/user-attachments/assets/8e24f5f8-8e1f-4adc-8a40-2df33749b30d" />
<img width="1047" height="820" alt="12" src="https://github.com/user-attachments/assets/0f2f9847-a7b4-4e93-9800-5db2f5d4ec58" />
<img width="893" height="797" alt="13" src="https://github.com/user-attachments/assets/f463fbb8-c560-4e15-8c00-51e69473d090" />
<img width="1068" height="648" alt="14" src="https://github.com/user-attachments/assets/b0687743-ccc8-44fa-9484-dd0b5624aa04" />

**Warning** : Argument is deprecated. To correct it, use the most updated argument from the official Terraform hashicorp website.

**Correction** :
<img width="848" height="97" alt="15" src="https://github.com/user-attachments/assets/88e3da3d-53aa-4cb3-aee6-0e2f3a705ef9" />

- Run terraform apply command : to apply the changes and build the infrastructure.
- Type yes when prompted.
<img width="1269" height="526" alt="16" src="https://github.com/user-attachments/assets/1249b64c-5b0a-4f26-b78d-276b38afa628" />
<img width="1026" height="879" alt="17" src="https://github.com/user-attachments/assets/e9cb64dd-a10f-462a-9bdf-5ee1bebd866f" />
<img width="1021" height="803" alt="18" src="https://github.com/user-attachments/assets/543b87fe-835a-47b8-b303-575b5387a780" />
<img width="825" height="890" alt="19" src="https://github.com/user-attachments/assets/d8cd9abb-8663-4961-a2e7-296b1e55ae75" />
<img width="1052" height="177" alt="20" src="https://github.com/user-attachments/assets/f4806308-de42-4c63-840b-9e74085f1cfe" />
<img width="808" height="774" alt="23" src="https://github.com/user-attachments/assets/c68aff95-0fbb-4a7b-8307-0a5b0ff0679f" />

- Check your infrastructure on AWS Console. The VPC was created as well as its components : 
- **VPC**
<img width="1436" height="396" alt="25" src="https://github.com/user-attachments/assets/f7718feb-e615-4926-962c-a322c3accb76" />
<img width="1430" height="478" alt="26" src="https://github.com/user-attachments/assets/7744e994-351b-4fea-a0d6-e0fe8b3e3dcb" />

- **Subnets : a Public subnet and a Private subnet**
<img width="1434" height="461" alt="28" src="https://github.com/user-attachments/assets/c083c31d-a41d-4ca6-a548-46aff8d0a58e" />

- **Route Tables : a Private Route Table and a Public Route Table**
<img width="1435" height="390" alt="29" src="https://github.com/user-attachments/assets/4a19272d-6028-4f2d-a2e5-90e4dfe97f51" />

- **Internet Gateway**
<img width="1438" height="707" alt="30" src="https://github.com/user-attachments/assets/cadcae4e-12ed-4d3b-ab8d-b7426f481082" />

- **Nat Gateway**
<img width="1432" height="738" alt="31" src="https://github.com/user-attachments/assets/5d6b592e-d5ca-425b-9540-e795795586cb" />

# Step 10 : Destroy (Cleanup)
- Run terraform destroy command : to delete the infrastructure and removes all the resources managed by terraform.
- Type yes when prompted.
<img width="1318" height="875" alt="32" src="https://github.com/user-attachments/assets/257f63ab-fee9-482c-bc0e-1eeb3256d97a" />
<img width="1079" height="873" alt="33" src="https://github.com/user-attachments/assets/8ed5091a-f248-46e2-bdfd-b59a95431d24" />
<img width="1159" height="775" alt="34" src="https://github.com/user-attachments/assets/f0825fbf-f654-4211-b45f-f168a959c53c" />
<img width="787" height="691" alt="35" src="https://github.com/user-attachments/assets/15dfda68-d27d-4a8e-94d9-41886bfb3d5d" />

- Check your infrastructure on AWS Console. The VPC was deleted as well as its components.
<img width="1439" height="501" alt="36" src="https://github.com/user-attachments/assets/d4ff73a4-b913-4dcb-8535-9395825fc874" />


### Summary
This breakdown provides a step-by-step guide to create a Virtual Private Cloud (VPC) on AWS using Terraform. By completing this lab, we had an overview on how to : 

- Define a custom VPC in Terraform’s Configuration files from creating and separating public and private subnets, to connecting to the internet using Internet Gateway and NAT Gateway, and understanding how routing works in AWS.
- Create a custom VPC infrastructure on AWS using Terraform workflow commands-line : terraform init, terraform plan, terraform apply, terraform destroy.

Building Infrastructure with Terraform as an IaC tool is an approach that not only provision, manage, and replicate cloud resources in a predictable and automated way. But also, reduces manual errors and enhances the scalability and maintainability of the infrastructure. This approach of building infrastructure using IaC, demonstrated how it can simplify and automate the process of deploying and managing a well-structured private network environment that requires high security and scalability, but also more complex cloud infrastructures. 
