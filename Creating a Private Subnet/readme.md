

# Creating a Private Subnet

**Author:** Abhishek Iyer  
**Email:** aiyer084@gmail.com

## Creating a Private Subnet

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is an AWS networking service that allows you to create a logically isolated virtual network in the AWS Cloud. Within a VPC, you can define your own IP address ranges, create public and private subnets, configure route tables, internet gateways, NAT gateways, security groups, and network ACLs, and control how resources communicate with each other and with the internet. It is useful because it gives you complete control over your cloud network, improves security by isolating resources, enables secure communication, and provides the flexibility to design scalable, highly available, and well-organized network architectures for different applications and workloads.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create and configure a private subnet within my VPC. I created a dedicated private route table and associated it with the private subnet to ensure it had no direct route to the Internet Gateway. I also created and associated a private Network ACL to control inbound and outbound traffic at the subnet level. This helped me understand how Amazon VPC can be used to securely isolate sensitive resources, such as databases and backend servers, from direct internet access while allowing secure communication within the VPC.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is that creating a private subnet alone does not automatically make it private. I learned that a subnet's behavior depends on its route table, specifically whether it has a route to an Internet Gateway. I also learned that every subnet is initially associated with the VPC's default route table and Network ACL, so creating dedicated ones is necessary to apply custom routing and security rules. This helped me better understand how different Amazon VPC networking components work together to secure cloud resources.

### This project took me...

This project took me around 30 minutes to complete

---

## Private vs Public Subnets

The difference between public and private subnets is that a public subnet has a route to an Internet Gateway, allowing resources such as web servers or bastion hosts to communicate directly with the internet if they have a public IP address. In contrast, a private subnet does not have a direct route to an Internet Gateway, so resources within it cannot be accessed directly from the internet. Private subnets are typically used for sensitive resources such as databases, backend application servers, and internal services, providing an additional layer of security by keeping them isolated while still allowing communication with other resources inside the VPC.

Having private subnets is useful because they provide a secure environment for hosting sensitive resources that should not be exposed to the public internet. By isolating databases, backend application servers, and internal services from direct external access, private subnets reduce the attack surface and improve the overall security of an application. Resources in a private subnet can still communicate with other resources within the VPC and, when necessary, access the internet securely through services such as a NAT Gateway, while remaining protected from unsolicited inbound internet traffic.

My private and public subnets cannot have the same IP address range (CIDR block). Each subnet within a VPC must use a unique, non-overlapping CIDR block so that AWS can correctly route network traffic between them. Although they can exist within the same VPC and share resources such as the VPC, security groups, and network ACLs (if configured), their IP address ranges must always be different.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the VPC's main route table when it is first created. It remains associated with the main route table until I explicitly associate it with a separate private route table that contains the routing rules required for the private subnet.

I had to set up a new route table because the private subnet requires different routing rules from the public subnet. A public route table includes a route to the Internet Gateway, allowing internet access, while a private route table does not. Creating a separate route table ensures that resources in the private subnet remain isolated from direct internet access while allowing traffic to be routed according to the subnet's security and networking requirements.

My private subnet's dedicated route table only has one route that allows traffic to be routed locally within the VPC. It contains the default local route, which enables communication between resources in the same VPC, but it does not include a route to an Internet Gateway. As a result, resources in the private subnet can communicate with other resources inside the VPC while remaining inaccessible from the public internet.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the VPC's default Network ACL when it is created. The default Network ACL allows all inbound and outbound traffic. I created and associated a dedicated private Network ACL so I could define custom traffic rules and apply more specific security controls to the private subnet.

I set up a dedicated Network ACL for my private subnet because it allows me to apply custom inbound and outbound traffic rules specifically for that subnet. This provides an additional layer of security beyond security groups by filtering traffic at the subnet level. Using a separate Network ACL also lets me enforce different security policies for the private subnet than for the public subnet, ensuring that sensitive resources remain protected while only the necessary network traffic is allowed.

My new Network ACL has two simple rules—it allows all inbound traffic and all outbound traffic, while the implicit * (deny) rule at the end blocks any traffic that does not match an allow rule. These default allow rules ensure that resources in the private subnet can communicate as required, while the Network ACL remains ready to be customized with more restrictive rules as security requirements evolve.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-private_1ed2cb07)

---

---
