**Author:** Abhishek Iyer  
**Email:** aiyer084@gmail.com

## VPC Traffic Flow and Security

## Introducing Today's Project!

### What is Amazon VPC?

Answer:

Amazon VPC (Virtual Private Cloud) is a service that lets you create and manage a private, isolated virtual network within AWS where you can securely launch and organize your cloud resources. It is useful because it gives you complete control over your network configuration, including IP address ranges, subnets, route tables, security groups, and network ACLs, allowing you to build secure, scalable, and highly available cloud environments.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure virtual network by configuring a VPC, public and private subnets, an Internet Gateway, a route table, a security group, and a Network ACL. I also learned how these components work together to control network traffic, provide internet connectivity, and secure resources within the VPC.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many different components are required to make a VPC fully functional. I learned that simply creating a VPC isn't enough—you also need subnets, an Internet Gateway, route tables, security groups, and Network ACLs, all working together to provide connectivity and security.

### This project took me...

This project took me approximately one and a half hours

---

## Route tables

Route tables are a set of rules (routes) that determine where network traffic is directed within an Amazon VPC. They control how resources communicate with other subnets, the internet, or other networks by defining the destination and the next hop for each route.

Route tables are needed to make a subnet public because they include a route that directs internet-bound traffic (0.0.0.0/0) to an Internet Gateway. Without this route, resources in the subnet cannot send or receive traffic from the internet, even if an Internet Gateway is attached to the VPC.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean:

Destination is the IP address range where the traffic is intended to go (for example, 0.0.0.0/0 for all internet traffic).
Target is the resource that the traffic is sent to, such as an Internet Gateway, NAT Gateway, VPC Peering Connection, or another network interface.

The route in my route table that directed internet-bound traffic to my Internet Gateway had a destination of 0.0.0.0/0 and a target of the Internet Gateway (IGW) attached to my VPC.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are virtual firewalls that protect AWS resources, such as EC2 instances, by controlling inbound and outbound network traffic. They use rules based on IP addresses, protocols, and port numbers to allow only authorized traffic, helping secure resources while ensuring they can communicate as required.

### Inbound vs Outbound rules

Inbound rules are rules that control which incoming network traffic is allowed to reach a resource, based on factors such as IP address, protocol, and port number. I configured an inbound rule that allows HTTP (TCP port 80) traffic from 0.0.0.0/0, enabling users from anywhere on the internet to access the web application hosted on the resource.

Outbound rules are rules that control what outgoing network traffic is allowed to leave a resource. By default, my security group's outbound rule allows all outbound traffic to any destination (0.0.0.0/0 for IPv4 and ::/0 for IPv6), enabling the resource to communicate with the internet or other networks as needed.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs (Network Access Control Lists) are subnet-level virtual firewalls that control inbound and outbound traffic for an entire subnet in an Amazon VPC. They use numbered allow and deny rules based on IP addresses, protocols, and port numbers, providing an additional layer of security alongside security groups.

### Security groups vs. network ACLs

The difference between a security group and a Network ACL is that security groups operate at the resource level (such as EC2 instances) and only support allow rules, while Network ACLs operate at the subnet level and support both allow and deny rules. Additionally, security groups are stateful, meaning return traffic is automatically allowed, whereas Network ACLs are stateless, so inbound and outbound rules must be configured separately.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules allow all inbound and all outbound IPv4 and IPv6 traffic. This means resources in the associated subnet can send and receive traffic freely unless you modify the default rules by adding specific allow or deny entries.

In contrast, a custom Network ACL's inbound and outbound rules are automatically set to deny all traffic. You must explicitly add allow (and, if needed, deny) rules for the specific traffic you want to permit to enter or leave the associated subnet.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

I created additional VPC resources, including a VPC, a subnet, and an Internet Gateway. Instead of my usual region, I used ap-south-1 (Asia Pacific – Mumbai). Teams use multiple AWS regions to improve application availability, reduce latency for users in different locations, support disaster recovery, and meet data residency or compliance requirements.

EC2 Global View is a tool where you can find EC2 and VPC resources across all AWS regions from a single dashboard. I could even narrow down my search by AWS Region, resource type, or specific resource ID. Without EC2 Global View, you'd have to switch between individual AWS regions manually to locate and manage your resources, which is more time-consuming and less efficient.

Now that I've learned about EC2 Global View, I'd use it again to monitor, locate, and manage EC2 and VPC resources across multiple AWS regions from a single place. It is especially useful for troubleshooting, auditing infrastructure, and managing multi-region deployments without manually switching between regions.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-security_b03ea6162)

---

---
