# Launching VPC Resources
**Author:** Abhishek Iyer  
**Email:** aiyer084@gmail.com
## Launching VPC Resources

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is an AWS networking service that enables you to create a logically isolated virtual network in the AWS Cloud where you can launch and manage resources such as EC2 instances. It allows you to define IP address ranges, create public and private subnets, configure route tables, Internet Gateways, NAT Gateways, security groups, and Network ACLs to control network traffic and access. It is useful because it provides complete control over your cloud network, enhances security through network isolation and access controls, supports scalable and highly available architectures, and allows you to securely connect resources to the internet, other AWS services, or on-premises networks as needed.

### How I used Amazon VPC in this project

I used Amazon VPC to deploy EC2 instances in both public and private subnets and to understand how different networking components work together. I configured networking settings, security groups, and routing to enable secure communication between the instances while restricting direct internet access to the private EC2 instance. I also used the Amazon VPC creation wizard to automatically build a complete VPC environment, which helped me learn how AWS simplifies the deployment of secure and scalable network architectures.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy the Amazon VPC creation wizard makes it to deploy a complete networking environment. Instead of manually creating and connecting each component, the wizard automatically configured the VPC, subnets, route tables, gateways, and other resources with the correct settings. I also didn't expect how security groups could use another security group as the source for traffic, making communication between EC2 instances more secure and easier to manage than using IP addresses.

### This project took me...

This project took me around 45 minutes

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means connecting to the EC2 instance so that you can manage, configure, and interact with its operating system. This is typically done using SSH for Linux instances or Remote Desktop Protocol (RDP) for Windows instances. Direct access allows you to install software, configure services, run commands, transfer files, troubleshoot issues, and administer the instance securely. In AWS, this access is usually controlled through key pairs, security groups, and the instance's network configuration.

### SSH is a key method for directly accessing a VM

SSH (Secure Shell) traffic means encrypted network communication between a client and a remote server or virtual machine over the SSH protocol, typically using TCP port 22. It allows users to securely log in to an EC2 instance, execute commands, transfer files, and manage the system remotely while protecting the data from interception or unauthorized access through encryption.

### To enable direct access, I set up key pairs

Key pairs are a secure authentication mechanism used to access Amazon EC2 instances. A key pair consists of a public key, which AWS stores on the EC2 instance, and a private key, which is downloaded and kept securely by the user. When connecting to an EC2 instance using SSH (or decrypting the administrator password for Windows instances), AWS verifies that the private key matches the stored public key. This provides a more secure alternative to password-based authentication and helps protect EC2 instances from unauthorized access.

A private key's file format refers to the type of file used to store the private key that authenticates a user when connecting to an EC2 instance. AWS supports different formats depending on the client being used. For example, a .pem (Privacy-Enhanced Mail) file is commonly used for SSH connections from Linux, macOS, and tools such as OpenSSH on Windows, while a .ppk (PuTTY Private Key) file is used with the PuTTY SSH client on Windows. My private key's file format was .pem, which I used to securely authenticate and access my EC2 instance via SSH.

---

## Launching a public server

I had to change my EC2 instance's networking settings by placing it in my VPC's public subnet, associating it with the appropriate security group, enabling a public IPv4 address, and ensuring it used the correct route table that provides access to the Internet Gateway. These changes allowed the instance to communicate with the internet and enabled me to securely access it using SSH while keeping access controlled through the security group's inbound and outbound rules.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it requires different access rules than the public server. The public server is designed to accept traffic from the internet, such as SSH or web traffic, while the private server should only accept traffic from trusted resources within the VPC, such as the public EC2 instance. Using a separate security group allows me to apply the principle of least privilege, restricting access to only the necessary sources and improving the overall security of the VPC.

My private server's security group's source is the security group attached to my public EC2 instance. This means that only EC2 instances associated with that security group are allowed to initiate the permitted traffic, such as SSH, to the private server. Using a security group as the source is more secure than allowing access from a public IP address because it restricts access to trusted resources within the VPC rather than exposing the private instance to the internet.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the Amazon VPC creation wizard instead of manually creating each networking component. The wizard automatically created the VPC, public and private subnets, route tables, Internet Gateway, security groups, and other required resources with the appropriate configurations. This approach was much faster, reduced the chance of configuration errors, and demonstrated how AWS can automate the deployment of a secure and functional VPC environment.

A VPC resource map is a visual representation of all the networking resources within an Amazon VPC and how they are connected. It displays components such as the VPC, public and private subnets, route tables, Internet Gateway, NAT Gateway, security groups, network ACLs, and EC2 instances. The resource map helps administrators understand the network architecture, troubleshoot connectivity issues, and verify that resources are configured correctly, making it easier to manage and maintain the VPC environment.

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because each Amazon VPC is a logically isolated virtual network. CIDR blocks only need to be unique within the same VPC, not across different VPCs. Since the two VPCs are separate and do not communicate by default, they can use identical IP address ranges without causing conflicts. However, if the VPCs need to be connected in the future using services such as VPC Peering or AWS Transit Gateway, their CIDR blocks must not overlap.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: creating either one public subnet or two public subnets. This was because the Amazon VPC creation wizard automatically creates one public subnet per Availability Zone (AZ). I could choose to use one AZ for a simpler, lower-cost setup or two AZs to improve high availability and fault tolerance by distributing resources across multiple Availability Zones.

The setup page also offered to create NAT Gateways, which are AWS-managed networking services that allow resources in private subnets to initiate outbound connections to the internet while preventing unsolicited inbound connections from the internet. NAT Gateways are commonly used to enable private EC2 instances to download software updates, install packages, or access AWS services without exposing them to direct public internet access. They provide a secure way for private resources to communicate with external services while maintaining network isolation.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-ec2_8ee57662)

---

---
