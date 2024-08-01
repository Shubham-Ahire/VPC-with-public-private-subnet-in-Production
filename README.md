# VPC-with-public-private-subnet-in-Production

This Project demonstrate how to create a VPC that you can use for servers in a production environment.

To improve resiliency, you deploy the servers in two availablity zones, by using an Auto Scaling group and an Application Load Balancer. For additonal security we deploy the servers in private subnet. The server receive request through the Load Balancer. The servers can connect to the internet using the NAT gateway.


![image](https://github.com/user-attachments/assets/c06a56e6-e0bf-4941-86a2-21a8db037ec9)
