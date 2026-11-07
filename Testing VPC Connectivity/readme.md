# Testing VPC Connectivity


**Author:** Abhishek Iyer  
**Email:** aiyer084@gmail.com

---

## Testing VPC Connectivity

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service in AWS that allows me to create and manage my own isolated virtual network in the AWS cloud.
It gives me control over important networking components such as IP addresses, subnets, route tables, Internet Gateways, Security Groups, and Network ACLs.
It is useful because I can decide which resources can communicate with each other and which resources can access the internet.
For example, I can place a Public Server in a public subnet and a Private Server in a private subnet for better security.
This helps me build a secure, controlled, and well-organized network infrastructure for my AWS resources

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create and manage the network environment for my Public and Private Servers.
I used subnets to separate the Public Server from the Private Server and control how they communicate.
I configured route tables and an Internet Gateway so that the Public Server could communicate with the internet.
I also worked with Security Groups and Network ACLs to control and secure network traffic between the servers.
Finally, I tested the connectivity using ping and curl to verify communication between the servers and access to the internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many different AWS networking components need to work together for a simple connection to succeed.
I initially thought that having the correct IP addresses would be enough to connect the servers.
However, I learned that Security Groups, Network ACLs, route tables, subnets, and the Internet Gateway can all affect connectivity.
Troubleshooting the failed ping and connection attempts helped me understand how these components work together.
This project showed me that networking problems often require checking multiple layers of configuration instead of just one setting.

### This project took me...

This project took me around 1-2 hours to complete.
Most of the time was spent setting up the Public and Private Servers and configuring the VPC networking components.
I also spent some time testing connectivity using ping and curl.
The troubleshooting took additional time because I had to check the Security Groups, Network ACLs, route tables, and Internet Gateway.
Overall, the project was a good hands-on experience that helped me understand AWS networking and connectivity in a practical way.

---

## Connecting to an EC2 Instance

connectivity means the ability of two devices or systems to connect and communicate with each other over a network.

My first connectivity test was whether I could connect to the Public Server using its public IP address over the internet. This test helps me confirm that the server is reachable from my computer and that the network configuration, such as the security group and allowed ports, is working correctly.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is an AWS feature that allows me to securely connect to an EC2 instance through a web browser using SSH, without needing to manage or share an SSH key manually.

My first attempt at getting direct access to my public server resulted in an error, because the EC2 instance was not configured to allow the required SSH connection. The security group was blocking the SSH traffic, so EC2 Instance Connect could not establish a connection to the server.

I fixed this error by checking the EC2 instance’s security group and allowing inbound SSH traffic on port 22 from my IP address. After updating the security group rule, I tried connecting again using EC2 Instance Connect, and the connection was successful.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network utility that sends small packets of data to another device or server and checks whether it responds. I used ping to test the connectivity between my Public Server and my Private Server, so I could verify whether the Public Server could reach and communicate with the Private Server over the network.

The ping command I ran was ping <Private Server’s Private IP Address>


The first ping returned “Request timed out.” This meant that the Public Server could not reach the Private Server or was not receiving a response from it. This indicated that there was a network connectivity or configuration issue that needed to be investigated.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by checking the security group rules and the Network ACL (Access Control List) of my Private Server’s subnet. I made sure that the required ICMP traffic was allowed in both the Security Group and Network ACL. After correcting the rules, I ran the ping command again and received successful replies, confirming that the Public Server could communicate with the Private Server.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

curl is a command-line tool used to communicate with servers over a network or the internet.
It can send requests to websites, APIs, and other network services and display their responses.
It is commonly used to test whether a server can successfully reach another server or website.
In this step, I used curl to check whether my Public Server could access the internet.
If curl returns a response, it confirms that the server has working internet connectivity.

I used curl to test the connectivity between my Public Server and the internet.
It allowed me to send a request from the Public Server to an internet-based website or service.
By checking the response, I could determine whether the Public Server had working internet access.
This was useful for identifying problems in the AWS network configuration.
If the request failed, I could troubleshoot components such as the route table, Internet Gateway, Security Group, and Network ACL.

### Ping vs Curl

Ping and curl are different because they are used to test different types of network connectivity.
ping uses ICMP packets to check whether a device or server is reachable and responding on the network.
curl is mainly used to send requests to web servers and retrieve data using protocols such as HTTP or HTTPS.
Ping tells us whether a server is reachable, while curl can also confirm whether a web service or application is responding.
In this lab, I used ping to test communication between servers and curl to test whether my Public Server could access the internet.

---

## Connectivity to the Internet

I ran the curl command curl https://example.com, which returned the HTML content of the Example Domain webpage.
This showed that my Public Server was able to successfully send an HTTPS request to an external internet server.
The response confirmed that the server had working internet connectivity.
It also showed that the required network configuration was allowing outbound internet traffic.
Therefore, the successful curl request confirmed that my Public Server could communicate with the internet.

![Image](http://nextwork.ai/enthusiastic_navy_agile_cape_gooseberry/uploads/aws-networks-connectivity_8ee57662)

---

---
