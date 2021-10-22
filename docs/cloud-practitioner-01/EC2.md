# EC2 - Elastic Compute Cloud

- Infrastructure as a Service (IaaS)

## Capabilities:

- Renting virtual machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across machines (ELB)
- Scaling the services using an auto-scaling group (ASG)

## EC2 Configuration Options

- OS: Linux, Windows, MacOS
- Compute power and cores (CPU)
- Random-Access Memory (RAM)
- Storage space:

  1. Network-attached (EBS + EFS)
  1. Hardware (EC2 Instance Store)

- Network card – speed of the card, Public IP address
- Firewall rules – Security Group
- Bootstrap script – EC2 User Data

## Types of EC2 Instances

### General Purpose

- Great for a variety of workloads
- balance between compute, memory, and networking

### Compute Optimized

- Great for compute-intensive tasks that require high performance processors
- The Cs (name)

### Memory Optimized

- Fast performance for workloads that process large data sets in memory

### Storage Optimized

- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage

## Security Groups

Network security in AWS.

- Control how traffic is allowed into or out of our EC2 instances
- Only contain **allow** rules
- Rules can reference by IP or by a Security Group
- They regulate:

  1. Access to ports
  1. Authorized IP ranges (IPv4-IPv6)
  1. Control of inbound network
  1. Control of outbound network

- Can be attached to multiple instances
- Locked down to a region/VPC combination
- Lives outside EC2 – if traffic is blocked the EC3 instance won't see it
- Good practice to maintain one separate Security Group for SSH access
- If your application times out, then it's a Security Group issue
- _Connection Refused_ error – application error
- By default:
  - All **inbound traffic** is **blocked**
  - All **outbound traffic** is **authorized**
