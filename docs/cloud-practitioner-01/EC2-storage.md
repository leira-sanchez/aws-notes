# EC2 Instance Storage

## EBS Volume (Elastic Block Store)

A network drive that can be attached to instances while they run.

- Allows instances to persist data, even after their termination

- For this exam, can be mounted only to one instance at a time

- Bound to a specific AZ

- Not a physical drive

- Connects to instance through the network which may cause latency

- Can be detached from an EC2 Instance and attached to another one quickly

- Must provision capacity (GB and IOPS)

## EBS Snapshots

Backup ata point in time.

- It isn't necessary to detach the volume to create the snapshot

- With snapshots, it is possible to copy across AZ or Regions.

## AMI (Amazon Machine Image)

Customization of an EC2 instance.

- Add your own software, config, OS, etc.
- Faster boot because all software is pre-packaged
- AMI are built for a specific region and can be copied across regions
- You can choose from

  1. Public AMI - provided by AWS
  1. Custom – you can make and maintain them yourself.
  1. AWS Marketplace – where people share and sell their own custom AMIs.

- AMI Process:

  1. Start an EC2 instance and customize it
  1. Stop the instance (for data integrity)
  1. Build an AMI – also creates snapshots
  1. Launch instances from other AMIs

## EC2 Image Builder

Used to automate the creation of Virtual Machines or container images.

- Automate creation, maintain, validate, and test EC2 AMIs
- Can be run on a schedule
- Free service (pay for underlying resources)

## EC2 Instance Store (Ephemeral)

High-performance hardware disk

- Better I/O performance than EBS
- EC2 Instance Store lose their data if they're stopped
- Good for buffer/cache/scratch data/temp
- Risk of data loss if hardware fails
- Backups and replication are your responsibility

## Elastic File System (EFS)

Managed NFS (network file system) that can be mounted on hundreds of EC2s

- Only works with Linux EC2 instances in multi-AZ
- Highly scalable, available, expensive
- Pay per use, no capacity planning

## EFS Infrequent Access

Storage class that is cost-optimized for files not accessed everyday

- Up to 92% lower cost compared to EFS Standard
  EFS will automatically move your files to EFS-IA based on the last time they were accessed
- Enable EFS-IA with a Lifecycle Policy
- Transparent to the applications accessing EFS

## Shared Responsibility Model for EC2 Storage

- AWS

  1. Infrastructure
  1. REplication for data for EBS volumes and EFS drives
  1. Replacing faulty hardware
  1. Ensuring their employees can't access your data

* Customer

  1. Backup/Snapshots
  1. Data encryption
  1. Responsible for any data on the drives
  1. Risk of using EC2 Instance Store

## Amazon FSx for Window File Server

- Fully managed, highly reliable, and scalable Windows native shared file system
- Supports SMB Protocol and Windows NTFs
- Integrated with Microsoft Active Directory
- Can be accessed from AWS on on-prem infra

## Amazon FSx for Lustre

- Fully managed, high-performance, scalable file storage for high-performance computing (HPC)
- Lustre = Linux + Cluster
- Scales up to 100s of GB/s, millions of IOPS, sub-ms latencies
