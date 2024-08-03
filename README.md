# VPC-with-public-private-subnet-in-Production

This Project demonstrate how to create a VPC that you can use for servers in a production environment.

To improve resiliency, you deploy the servers in two availablity zones, by using an Auto Scaling group and an Application Load Balancer. For additonal security we deploy the servers in private subnet. The server receive request through the Load Balancer. The servers can connect to the internet using the NAT gateway.


![image](https://github.com/user-attachments/assets/c06a56e6-e0bf-4941-86a2-21a8db037ec9)

# Overview

Here we create VPC having public subnets and private subnets in two Availability Zones.

Each public subnet contains a NAT gateway and a load balancer node.

The server run in the private subnets, they are launched and terminated using the Auto scaling group, and receive traffic from the load balancer.

The servers can connect to the internet by using the NAT gateway.

# <b>Steps to perform:</b>

# Part 1 Creating the VPC

AWS -> VPC & more -> No. of AZ 2 -> No. of public subnet 2 -> No. of private subnets 2 -> NAT gateway 1 per AZ -> VPC Endpoint none -> Create VPC


![VPC overview](https://github.com/user-attachments/assets/f7c64658-d4e8-4d2f-af55-de1174afa194)


# Part 2 Creating Auto Scaling groups

<b>Create a Launch Template</b> 

EC2 -> Auto scaling -> Create -> Launch template -> just keep the VPC you created in the option -> Edit the security groups; add SSH and port no. 8000 as we are going to host the python application there.

Now, create the Auto scaling group, by selecting the created launch template, keep the created VPC in the option & now choose the availability zone as both private subnet as we deploy the EC2 into the private subnets.

And create the Auto Scaling groups.

![Auto scaling groups](https://github.com/user-attachments/assets/78681425-4ecd-4757-902c-1cf9d8eb2b4e)

Now we will create a bastion host(jump server) in the same VPC allowing SSH access to connect to our EC2 instance in the private subnet.

And we will host a static python server in one of the Instance.

![Instance](https://github.com/user-attachments/assets/f8f170ca-d3f0-4608-9ce2-34263e7e0494)


# Part 3 Create Application Load Balancer

Now create a Application Load Balancer by selecting both the public subnet

Create a Target group by selecting both the instance in which one of the instance we have hosted the application.

![Target group](https://github.com/user-attachments/assets/0d385b8e-0d21-4f6b-b433-82ca353466a0)


Allow HTTP port 80 access from the security group of Load Balancer.

![Load Balancer](https://github.com/user-attachments/assets/3eb31573-c1e8-4051-bde9-ed52691c0f4a)


And try to connect it from the internet

![Screenshot 2024-08-03 161813](https://github.com/user-attachments/assets/cfaf646a-3011-4ed5-a5c5-d02b204bd4b0)

<b> Here we have demonstrated to create a VPC that you can use for servers in Production Evironment
