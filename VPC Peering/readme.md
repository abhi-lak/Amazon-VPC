

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to establish secure communication between two separate Amazon Virtual Private Clouds (VPCs) using AWS VPC Peering. I will create and configure two VPCs with their respective subnets, route tables, and network settings. I will then establish a VPC Peering Connection between them, configure the necessary routing rules on both sides, and verify connectivity between resources hosted in the two VPCs.

I'm doing this project to understand how VPC Peering enables private communication between resources across different VPCs without requiring traffic to travel over the public internet. I also aim to gain practical experience with CIDR blocks, route tables, private IP addressing, and network connectivity testing. By completing this project, I will strengthen my understanding of AWS networking, VPC architecture, and secure cloud infrastructure management.

### What is Amazon VPC?

Amazon Virtual Private Cloud (Amazon VPC) is a networking service provided by Amazon Web Services (AWS) that allows users to create a logically isolated virtual network within the AWS Cloud. It provides complete control over the virtual networking environment, including IP address ranges, subnets, route tables, network gateways, and security configurations. Within a VPC, users can launch and manage AWS resources such as EC2 instances, databases, and applications while controlling how they communicate with each other and the internet.

Amazon VPC is useful because it provides a secure, flexible, and customizable networking environment for hosting cloud resources. It allows users to divide networks into public and private subnets, control incoming and outgoing traffic through security groups and Network ACLs, and establish private connectivity between different VPCs using VPC Peering. It also helps organizations isolate applications, manage network access, improve security, and build scalable cloud infrastructure. Overall, Amazon VPC provides the foundation for securely managing and connecting resources within AWS.

### How I used Amazon VPC in this project

used Amazon VPC to...

In today's project, I used Amazon Virtual Private Cloud (VPC) to create and configure two separate virtual networks within AWS. I created two VPCs with unique, non-overlapping IPv4 CIDR blocks (10.1.0.0/16 for VPC 1 and 10.2.0.0/16 for VPC 2), each containing a public subnet. I then established a VPC Peering Connection between these two networks, allowing them to communicate privately.

I configured the route tables of both VPCs by adding routes that directed traffic destined for the other VPC through the peering connection. I also launched EC2 instances in each VPC, configured their security groups to permit the required ICMP traffic, and used the ping command to test connectivity between them through their private IP addresses.

Through this project, I gained practical experience with VPC creation, subnet configuration, CIDR addressing, route table management, VPC Peering, EC2 deployment, and network security. I learned how separate AWS virtual networks can communicate securely while maintaining their independent network environments.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that establishing a VPC Peering Connection alone would not automatically enable communication between two VPCs. I initially thought that once the peering connection became active, the EC2 instances would be able to communicate directly. However, I learned that additional configurations, such as updating route tables, configuring security group inbound rules, and allowing the required network traffic, are equally important.

Another unexpected learning was the importance of assigning a public IPv4 address to an EC2 instance for browser-based access through EC2 Instance Connect. I also encountered an issue where an EC2 instance was launched in the wrong VPC, resulting in an unexpected private IP address. Troubleshooting this helped me understand the importance of selecting the correct VPC and subnet during instance creation.

Overall, this project taught me that successful cloud networking depends not only on establishing connections but also on correctly configuring every component involved in network communication.

### This project took me...

This project took me around 1 hour to complete

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two separate Amazon Virtual Private Clouds (VPCs) using the AWS VPC Wizard and its visual VPC resource map. I will configure each VPC with its own IPv4 CIDR block, public and private subnets, route tables, and other essential networking components as required. Using the VPC resource map will make the creation process faster and help me understand how different AWS networking resources are connected within a VPC.

I am performing this step because establishing two independent VPC environments is the foundation of the VPC Peering project. Creating separate VPCs will allow me to understand how isolated cloud networks operate and how their network configurations can be managed independently. These two VPCs will later be connected through a VPC Peering Connection to enable private communication between resources hosted in different networks.

### Step 2 - Create a Peering Connection

In this step, I will establish an Amazon VPC Peering Connection between the two VPCs that I created in the previous step. I will select one VPC as the requester and the other as the accepter, initiate the peering request, and accept it to establish the connection between both virtual networks.

I am performing this step because VPC Peering allows two separate Amazon VPCs to communicate with each other using their private IPv4 addresses without requiring traffic to pass through the public internet. Establishing this connection is an important step towards creating communication between resources hosted in different VPCs. It will also help me understand how AWS enables private network connectivity between isolated cloud environments while maintaining their independent configurations and security boundaries.

### Step 3 - Update Route Tables

In this step, I will configure the route tables of both VPCs to enable network traffic to travel between them through the VPC Peering Connection. I will add appropriate routing entries to the route table of VPC 1, specifying the CIDR block of VPC 2 as the destination and the VPC Peering Connection as the target. Similarly, I will update the route table of VPC 2 by adding a route to the CIDR block of VPC 1 through the same peering connection.

I am performing this step because creating a VPC Peering Connection alone does not automatically enable communication between the two VPCs. Route tables must be configured on both sides so that AWS knows where to forward traffic destined for the other VPC. These routing rules will allow resources in both VPCs to communicate using their private IP addresses. Through this step, I will understand how AWS route tables control network traffic and how proper routing configuration enables secure, private connectivity between separate virtual netwo

### Step 4 - Launch EC2 Instances

In this step, I will launch two Amazon EC2 instances, one in each VPC, to create virtual machines that will be used to test the VPC Peering Connection. While launching the instances, I will select the appropriate VPC and its corresponding public subnet for each EC2 instance. I will also configure the necessary instance settings, security groups, key pairs, and network access permissions to ensure that the instances can communicate as required.

I am performing this step because EC2 instances will act as test resources for verifying whether the VPC Peering Connection is functioning correctly. By placing one instance in VPC 1 and another in VPC 2, I can test communication between two separate virtual networks using their private IP addresses. This will help me understand how AWS EC2 instances interact across peered VPCs and how networking configurations, routing rules, and security group permissions work together to establish connectivity.

## Multi-VPC Architecture

I started my project by launching two separate Amazon Virtual Private Clouds (VPCs) using the AWS VPC Wizard and its visual VPC resource map. Each VPC was configured with its own IPv4 CIDR block and independent networking resources.

I created two public subnets in total, with one public subnet in each VPC. I also configured the associated route tables and Internet Gateways to provide internet connectivity to resources within the public subnets. Both VPCs initially operate as independent network environments.

These VPCs will later be connected through a VPC Peering Connection, allowing resources in both networks to communicate securely using their private IP addresses without routing traffic through the public internet.

The IPv4 CIDR blocks for VPC 1 and VPC 2 are unique and non-overlapping, meaning that each VPC has a different range of private IP addresses. They have to be unique because AWS VPC Peering requires the IPv4 CIDR blocks of the two VPCs to not overlap. If both VPCs use overlapping IP address ranges, AWS cannot establish proper routing between them because it would become difficult to determine which VPC a particular IP address belongs to.

Using unique CIDR blocks ensures that each VPC has its own distinct IP address space, allowing route tables to direct network traffic to the correct destination. This makes communication between the two VPCs possible through a VPC Peering Connection and helps prevent IP address conflicts, routing ambiguity, and network connectivity issues.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances because I do not need SSH access to the instances for the purpose of this project. The primary objective is to test connectivity between the two VPCs and verify whether the VPC Peering Connection is working correctly, rather than remotely accessing and managing the EC2 instances through SSH.

For this project, I will use the instances mainly to perform network connectivity tests, such as checking communication between their private IP addresses. Therefore, creating and downloading SSH key pairs is not necessary for the planned testing activities.

This approach also avoids managing additional private key files and simplifies the EC2 launch process. However, if SSH access is required in the future, I can configure an appropriate key pair or use AWS Systems Manager Session Manager for secure instance access.

![Multi-VPC Architecture](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_11111111)

## VPC Peering

A VPC Peering Connection is a networking connection between two Amazon Virtual Private Clouds (VPCs) that allows resources in both VPCs to communicate with each other using their private IPv4 or IPv6 addresses. It enables direct, private communication between two VPCs without requiring traffic to pass through the public internet, a VPN connection, or a separate physical network gateway.

VPC Peering uses AWS infrastructure to facilitate communication between the connected VPCs. To establish a peering connection, one VPC sends a request (known as the requester VPC), and the other VPC must accept that request (known as the accepter VPC). After the connection is established, administrators must update the route tables of both VPCs to direct traffic through the peering connection.

The CIDR blocks of the two VPCs must not overlap to ensure proper routing. VPC Peering can connect VPCs within the same AWS account or across different AWS accounts and Regions. It is also a non-transitive connection, meaning that if VPC A is peered with VPC B, and VPC B is peered with VPC C, VPC A cannot automatically communicate with VPC C through VPC B.

In short, VPC Peering provides a private and efficient way to connect separate AWS virtual networks while maintaining control over their individual network configurations and security settings.

connections to...

VPCs use peering connections to enable private communication and data exchange between two separate Amazon Virtual Private Clouds (VPCs). By default, VPCs are isolated from one another, meaning that resources in one VPC cannot directly communicate with resources in another VPC. A VPC Peering Connection overcomes this limitation by creating a private networking link between the two virtual networks.

Peering connections are useful when organizations need applications, servers, databases, or other cloud resources hosted in different VPCs to communicate securely. For example, an application server in one VPC can access a database hosted in another VPC using private IP addresses without exposing the communication to the public internet.

They also help organizations maintain separate network environments for different departments, applications, development, testing, and production systems while still allowing controlled communication between them. Overall, VPC Peering provides a simple and efficient way to connect isolated AWS networks, improve resource accessibility, and support secure communication across multiple VPCs.

The difference between a Requester and an Accepter in a VPC Peering Connection is based on their roles during the connection establishment process.

A Requester is the VPC that initiates the VPC Peering Connection by sending a peering request to another VPC. It acts as the starting point of the connection and requests permission to establish private communication with the target VPC.

An Accepter is the VPC that receives the peering request from the requester. The owner or administrator of the accepter VPC must review and accept the request before the peering connection becomes active.

For example, if VPC 1 sends a peering request to VPC 2, VPC 1 acts as the Requester, while VPC 2 acts as the Accepter. Once VPC 2 accepts the request, the peering connection is established and becomes active.

In short, the Requester initiates the connection, whereas the Accepter approves it. Both roles are essential for establishing a VPC Peering Connection successfully.

![VPC Peering](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_1cbb1b88)

## Updating route tables

After accepting a VPC Peering Connection, my VPCs' route tables need to be updated because establishing a peering connection alone does not automatically enable network communication between the two VPCs. Route tables determine where network traffic should be directed based on its destination IP address.

I added a new route to the route table of each VPC, specifying the CIDR block of the other VPC as the destination and the VPC Peering Connection as the target. This configuration tells AWS to forward traffic destined for the other VPC through the established peering connection instead of sending it to the internet gateway or another network destination.

For example, VPC 1's route table directs traffic intended for VPC 2 through the peering connection, while VPC 2's route table contains a corresponding route back to VPC 1. Both routing entries are necessary to enable two-way communication.

Therefore, updating the route tables ensures that resources in both VPCs can communicate using their private IP addresses, enabling secure and direct network connectivity without routing traffic through the public internet.

My VPCs' new routes have a destination of the IPv4 CIDR block of the opposite VPC. In the route table of VPC 1, I added the CIDR block of VPC 2 as the destination, and in the route table of VPC 2, I added the CIDR block of VPC 1 as the destination.

The routes' target was the VPC Peering Connection (pcx) that I established between the two VPCs. This tells AWS to forward all traffic destined for the other VPC through the peering connection.

By configuring these routes in both VPCs, I enabled bidirectional private network communication between their resources using private IP addresses, without sending traffic over the public internet.

![Updating route tables](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_4a9e8014)

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to establish a connection to my first Amazon EC2 instance through the AWS Management Console. I will select the EC2 instance launched in VPC 1 and attempt to access its terminal without requiring a locally stored SSH key pair. During this process, I will also troubleshoot and resolve any connection errors that may occur due to network configurations, security group rules, or instance connectivity settings.

I am performing this step because I need access to the EC2 instance's terminal to execute network commands and test communication between the two VPCs. EC2 Instance Connect provides a convenient and secure way to connect to an instance using SSH through the AWS Console. Successfully accessing the instance will allow me to perform further connectivity tests and verify whether the VPC Peering Connection and associated routing configurations are working as expected.

### Step 6 - Connect to EC2 Instance 1

In this step, I will attempt to connect to Instance 1 (NextWork VPC 1) again using Amazon EC2 Instance Connect after associating an Elastic IP address with it. I will access the EC2 console, select the instance, and use the Connect option to establish a browser-based SSH session. If another connection error occurs, I will investigate the network configuration and troubleshoot the issue by checking the security group rules, SSH permissions, and network connectivity settings.

I am performing this step because assigning a public IPv4 address alone does not guarantee successful connectivity. The instance must also have the correct security configurations and allow inbound SSH traffic on TCP port 22. This step will help me understand how public IP addressing, security groups, and network access work together to enable secure remote access to EC2 instances.

### Step 7 - Test VPC Peering

In this step, I will use Instance 1 (abhi VPC 1) to establish communication with Instance 2 (abhi VPC 2) through the VPC Peering Connection. I will access the terminal of Instance 1 using EC2 Instance Connect and use network diagnostic commands, such as ping, to send test messages to Instance 2 using its private IPv4 address. I will also troubleshoot any connectivity issues that prevent communication between the two instances and configure the necessary security group rules to allow the required inbound and outbound traffic.

I am performing this step because I want to verify whether the VPC Peering Connection is functioning correctly and whether resources in both VPCs can communicate with each other. This will help me understand how route tables, private IP addresses, security groups, and network access control work together to enable communication between separate AWS networks. Successfully sending and receiving test messages will confirm that the two VPCs can exchange network traffic through their private connection without relying on the public internet.

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to securely access my Amazon EC2 instance directly through the AWS Management Console without needing to configure or manage a permanent SSH key pair on my local computer. EC2 Instance Connect provides browser-based SSH connectivity, allowing me to open a terminal session and execute commands on my instance.

I am using this service because I need to access the EC2 instance to perform network connectivity tests and verify whether the VPC Peering Connection is functioning correctly. Through the terminal, I can execute commands such as ping, traceroute, and other network diagnostic commands to check communication with the EC2 instance in the second VPC.

It also helps simplify remote instance access and troubleshoot potential connectivity issues related to security groups, routing tables, and network configurations.

I was stopped from using EC2 Instance Connect because the Auto-assign Public IP option was set to Disable during the EC2 instance launch. As a result, my EC2 instance was not assigned a public IPv4 address, which is required for establishing a browser-based SSH connection through EC2 Instance Connect over the internet.

To resolve this issue, I allocated an Elastic IP address from Amazon's IPv4 address pool and associated it with my EC2 instance. An Elastic IP provides a static public IPv4 address that remains associated with my AWS account until it is released.

After associating the Elastic IP with the instance, it received a public IPv4 address, allowing me to use EC2 Instance Connect and access the instance's terminal successfully.

![Troubleshooting Instance Connect](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7685490c)

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static, public IPv4 addresses provided by Amazon Web Services (AWS) that can be allocated to an AWS account and associated with resources such as EC2 instances. Unlike automatically assigned public IPv4 addresses, which are generally dynamic and can change when an instance is stopped and started, Elastic IP addresses remain allocated to the AWS account until they are explicitly released.

Elastic IP addresses are useful when an application or server needs a consistent public IP address to remain accessible over the internet. For example, websites, web applications, and other internet-facing services can use Elastic IPs to maintain a fixed network address even when an EC2 instance is restarted or replaced.

In this project, I allocated an Elastic IP address from Amazon's public IPv4 address pool and associated it with my EC2 instance. This provided the instance with a public IPv4 address, allowing me to establish a connection using EC2 Instance Connect and continue with the VPC Peering connectivity tests.

Associating an Elastic IP address resolved the connection error because my EC2 instance initially did not have a public IPv4 address, which was required to establish a connection using EC2 Instance Connect over the internet.

By allocating an Elastic IP address from Amazon's public IPv4 address pool and associating it with my EC2 instance, I provided the instance with a static public IPv4 address. This made the instance reachable through its public network interface, allowing EC2 Instance Connect to establish an SSH connection through the AWS Management Console.

Unlike a dynamically assigned public IPv4 address, an Elastic IP remains allocated to my AWS account until it is released. This ensures consistent public addressing and makes remote access more reliable.

Therefore, associating the Elastic IP resolved the missing public IPv4 address issue and allowed me to access my EC2 instance successfully.

![Elastic IP addresses](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_45663498)

## Troubleshooting ping issues

To test VPC Peering, I ran the ping command from the terminal of Instance 1 using the private IPv4 address of Instance 2 as the destination.

The command was:\
ping 10.2.1.XX

Here, 10.2.1.XX represents the private IPv4 address assigned to Instance 2 in VPC 2.

The ping command uses the ICMP protocol to send test packets to the destination instance and check whether it responds. Receiving replies confirms that network communication is working between the two VPCs through the VPC Peering Connection.

Using the private IP address ensures that the communication takes place through the private AWS network rather than through the public internet.

A successful ping test would validate my VPC Peering Connection because it confirms that network traffic can travel between two separate Amazon VPCs using their private IP addresses. When I execute the ping command from an EC2 instance in VPC 1 to the private IP address of an EC2 instance in VPC 2, ICMP Echo Request packets are sent through the VPC Peering Connection. If the destination instance receives these packets and sends ICMP Echo Reply packets back, it confirms that bidirectional network communication is working.

A successful ping test also verifies that the essential networking configurations are functioning correctly, including the VPC Peering Connection, route table entries, security group permissions, and Network ACL rules. It demonstrates that the two VPCs can exchange traffic without relying on public IP addresses or routing through the public internet.

Therefore, a successful ping test provides practical confirmation that the VPC Peering Connection is correctly established and that resources in both VPCs can communicate privately using their internal IP addresses.

I had to update my second EC2 instance's security group because, by default, its inbound rules might not allow ICMP traffic from resources located in another VPC. Even though the VPC Peering Connection and route tables were correctly configured, the security group needed permission to accept incoming ping requests from Instance 1.

I added a new inbound rule with the following configuration:\
\- Type: All ICMP - IPv4\
\- Protocol: ICMP\
\- Port Range: All\
\- Source: 10.1.0.0/16 (VPC 1 CIDR block)\
This rule allows ICMP traffic originating from VPC 1 to reach my second EC2 instance in VPC 2. It enables Instance 1 to send ping requests and receive responses from Instance 2 through the VPC Peering Connection.

Updating this security group rule was essential for allowing communication between the two instances while maintaining control over which network traffic is permitted.

![Troubleshooting ping issues](https://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7a29d352)
