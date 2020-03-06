# VPC
Virtual Private Cloud - lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creating of subnets, and configuration of route tables and network gateways.

## What can we do with a VPC?

* Launch instances into a subnet of your choosing

* Assign custom IP address ranges in each subnet

* Configure route tables between subnets

* Create internet gateway and attach it to our VPC

* Much Better security control over your AWS resources

* Instance security groups

* Subnet network access control lists (ACLS)

## Default VPC vs Custom VPC

* Default VPC is user friendly, allowing you to immediately deploy instances.

* All Subnets in a default VPC have a route out to the internet.

* Each EC2 instance has both a public and a private IP address.

## VPC Peering

* Allows you to connect one VPC with another via a direct network route using private IP addresses.

* Instances behave as if they were on the same private network.

* You can peer VPC's with other AWS accounts as well as with other VPCs in the same account.

* Peering is in a star configuration: 1 central VPC peers with 4 others. **No transitive peering!** You can't peer from one VPC through another. You must set a direct peering relationship between the VPCs you want to peer. 

* 1 Subnet = 1 Availability Zone

* Security Groups are *stateful*. Network Access Control Lists (NACL) are *stateless*.

* When you create a VPC, it also creates *defaults* of:
    * Route Table

    * Network Access Control List (NACL)

    * Security Group

    * *No* subnets

## Network Address Translation (NAT)

### NAT Instances 
Individual EC2 instances in private subnets that are able to communicate with the internet gateway without making the subnets public. About to be deprecated.

* When creating a NAT instance, Disable Source/Destination Check on the instance.

* Must be in a public subnet.

* There must be a route out of the private subnet to the NAT instance in order for this to work.

* The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.

* You can create high availability using Autoscaling Groups, multiple subnets in different AZs, and a script to automate failover.

* They are always behind a security group.

### NAT Gateways
Highly available that connects to the internet without becoming public, spread across multiple availability zones. Do not depend on a single instance.

* Redundant inside the AZ.

* You can only have one NAT Gateway in one AZ.

* Preferred by the enterprise.

* Starts at 5GBps and scales currently to 45 GBps

* No need to patch

* Not associated with security groups

* Automatically assigned a public ip address

* Remember to updated your route tables

* No need to disable Source/Destination checks

* If you only have one NAT Gateway and its AZ goes down, resources in the other AZs lose internet access.

### Network Access Control Lists

* Rules changes take effect immediately

* Inbound/outbound rules are evaluated in numerical order

* They have separate inbound and outbound rules. Each can deny or allow traffic.

* Network ACLs are statelss; response to allow inbound traffic are subject to the rules for outbound traffice and vice versa

* If you have a deny first, it's always going to deny even if you allow it later

* NACLs are always evaluated before security groups

* If you deny a specific port on your NACL, it's never going to reach the security group

* VPCs automatically come with a default NACL that, by default, allows all outbound and inboud traffic

* Custom NACLs, by default, deny all inbound and outbound traffic until you add rules

* Each subnet in the VPC must be associated with a NACL. If you don't explicitly associate a subnet with a NACL, the subnet is automatically associated with the default NACL

* IP Addresses must be blocked using NACLs not Security Groups

* You can associate a NACL with multiple subnets but a subnet can only be associated with one NACL at a time. When you associate a NACL with a subnet, the previous association is removed