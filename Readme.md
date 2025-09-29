AWS Project Used in Production
=
VPC With Public-Private Subnet in Production
=
📌 Overview
=
This example demonstrates how to create a VPC that you can use for servers in a production environment.

To improve resiliency, you deploy the servers in two availability zones by using an Auto-Scaling group and an Application Load Balancer. For additional security, you deploy the servers in a private subnet. The servers receive requests through the load balancer. The servers can connect the internet by using a NAT gateway. To improve resiliency, you deploy the NAT gateway in both Availability Zones.
<img width="1056" height="830" alt="image" src="https://github.com/user-attachments/assets/7da8cd6d-0175-4975-8a24-a9aebee329bc" />

About Project:
=
<img width="882" height="1108" alt="image" src="https://github.com/user-attachments/assets/ae3def8f-98a4-43d7-a4ca-37e083bdcdf2" />

Key Concepts:
=

1. Auto Scaling Group:

  Let’s say you want to deploy your application across two availability zones. Instead of manually creating EC2 instances twice, you can configure the Auto Scaling 
  Group to maintain a minimum of two replicas. Suppose your application starts receiving more requests, and two servers are insufficient to handle the traffic.

  In that case, the Auto Scaling Group will automatically decide to scale the number of servers dynamically, based on the demand.

2. Load Balancer:

   A Load Balancer is used to distribute incoming traffic across multiple servers to ensure efficient utilization and prevent overloading any single server.

   Additionally, it supports path-based and host-based routing, allowing requests to be directed to specific targets based on the URL path or hostname.

3. Bastion Host or Jump Server:

  When EC2 instances are created in a private subnet, they do not have public IP addresses, meaning you cannot SSH into these instances directly. This is done to 

  enhance security by avoiding public exposure. Instead, a Bastion Host (or Jump Host) is created in the public subnet.

  Using the Bastion Host, you can securely connect to EC2 instances in the private subnet. This approach allows for proper auditing of who is accessing the private 

  subnet.

  Additionally, you can configure a set of rules on the Bastion Host to control and monitor the traffic that flows to the private subnet.
