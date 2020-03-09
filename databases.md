# Databases

## Relational Databases on AWS
1. SQL Server
1. Oracle
1. MySQL Server
1. PostgreSQL
1. Aurora
1. MariaDB


* They are:
    * Multi-AZ - for disaster recovery
    * Read Replicas - for performance

* Runs on virtual machines

* Not serverless (except for Aurora)

* You cannot access these OSs

* OLTP - Online Transaction Processing

### Backups

* When restoring from a backup, the restored version is a new RDS instance with a new DNS endpoint. 

1. **Automated** - recovers to any point in time (to a second) within a *retention period*. They take a daily snapshot and store transaction logs through the day. In recovery, AWS will choose the most recent backup and then apply the transaction logs of that day. 
    * Enabled by default
    * Backup data is stored in S2
    * Free storage space equal to the size of the database
    * The creation of backups might result in elevated latency
    * Do not persist after original RDS instance is deleted

1. **Database Sanpshots** - are done manually and stored after the original RDS instance is deleted.

### Encryption

1. **Encryption at rest** - supported for all 6 DBs. Uses the KMS service. Once encrypted, data at rest, its backups, its read replicas, and its snapshots are encrypted as well.

### Multi-Az
AWS automatically creates exact copy of the production DB in another AZ. When the production AZ fails, it will automatically failover to the replica.

**Available to all databases except Aurora which is fault tolerant by design.**

### Read Replica
Allow for read-only copies of the production database. Uses Asynchronous replication from the primary RDS instance to the read replica. Read replicas can be used primarily for very read-heavy database workloads.

* **Improves database *performance***.

* These are available for: MySQL Server, PosgreSQL, MariaDB, Oracle, Aurora.

* Used for scaling, not DR.

* Must have automatic backups turned on to deploy a read replica.

* Any database can have up to 5 read replica copies.

* It is possible to have read replicas of read replicas but latency might increase.

* Each read replica will have its own DNS end point.

* Read replicas can have Multi-AZ.

* It is possible to create read replicas of Multi-AZ databases.

* Read replicas can be their own databases but it would break replication.

* It is possible to have a read replica in a second region.

### Aurora
A MySQL and PostgreSQL-compatible relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases. Provides up to five times better performance than MySQL and three times better than PosgreSQL at a much lower price point while delivering similar performance and availability.

* Starts with 10GB and autoscales in increments of 10GB with a max of 64TB

* Can scale up to a max of 32vCPUs and 244FB of Memory

* 2 copies of the data is contained in each availability zone with at least 3 AZs to a total of 6 copies of the data

* Self-healing - data blocks and disks are continuously scanned for errors and repaired automatically

* Replicas
    * Aurora Replicas (15)

    * MySQL Read Replicas (15)

* Backups
    * Automated backups are on by default and do not affect database performance

    * It is possible to take snapshots without affecting performance

    * It is possible to share Sanapshots with other AWS accounts

## NO SQL
1. **DynamoDB** - is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data modles. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

* Stored on SSD storage

* Spread acrros 3 geographically distinct data centres

* Eventual Consistent Reads (Default) - consistency across all copies of data is usually reached within a second. Repeating a read after a short time should return the updated data. (**Best Read Performance**)

* Strongly Consistent Reads - A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read. (**Instant < 1**)

## Redshift - Data Warehousing
* Fully managed, petabyte-scale data warehouse service in the cloud. ($0.25/hr - $1k/per TB per yr)

* **OLAP**

* Advanced compression

* Massively Parallel Processing (MPP)

* Backups
    * Enabled by default

    * Max. retention period: 35 days

    * Tries to maintain at least three copies of the data (original, replica, and backup in S3)

    * Can asynchronously replicate snapshots to S3 in another region for disaster recovery

* Pricing
    * **Compute Node Hours** - total number of hours you run across all your compute nodes for the billing period. 1 unit per node per hour.

    * Backup

    * Data transfer within a VPC


1. Single Node - 160 GB
1. Multi-Node
    * Leader node that manages client connections and receives queries.

    * Compute node - store data and perform queries and computations. Up to 128 compute nodes.

* Security
    * Encrypted in transit using SSL

    * Encrypted at rest using AES-256 encryption

    * By default Redshift takes care of key management
        * HSM

        * KMS

* Availability
    * Only available in 1 AZ

    * It is possible to restore snapshots to new AZ 

## ElastiCache
Web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the performance of web apps by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases. **To seped up performance of existing databases (frequent identical queries).**

ElastiCache supports two open-source in-memory caching engines:
* Memcached

* Redis
    * Multi-AZ

    * It is possible to do backups and restores 


## From the Quiz

* It is not possible to use the secondary database as an independent read node when you have deployed an RDS database into Multiple AZs.