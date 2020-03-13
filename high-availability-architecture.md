# Elastic Load Balancers
A physical or virtual device that is designed to help balance the network load across multiple web servers.

1. **Application Load Balancer** 
    * Best suited for load balancing of HTTP and HTTPS traffic.

    * They operate at Layer 7 and are application-aware.

    * They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

    * Cannot have Elastic IP assigned.

1. **Network Load Balancer**
    * Best suited for load balancing of TCP traffic where extreme performance is required.

    * They operate at the connection level (Level 4).

    * Are capable of handling millions of requests per second, while maintaining ultra-low latencies.

    * Use for extreme performance!

1. **Classic Load Balancer**
    * Legacy ELBs

    * Load balance HTTP/HTTPs applications

    * Use Level 7-specific features like X-Forwarded and sticky sessions

    * You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol

## Advanced Load Balancer Theory

### Sticky Sessions
Classic Load Balancer routes each request independently to the registered EC2 instance with the smallest load. Sticky sessions allow you to bind a user's session to a specific EC2 instance. This Ensures that all requests from the user during the session are sent to the same instance.

It is also possible to enable Sticky Sessions for Application Load Balancers but the traffice will be sent at the Target Group Level.

**Enable your users to stick to the same EC2 instance. Useful if you're storing information locally to that instance.**

### Cross-Zone Load Balancing
Enables you to load balance across multiple AZs.

### Path Patterns
You can create a listener with rules to forward requests based on the URL path. This is known as path-based routing. If you are running microservices, you can route traffic to multiple backend services using path-based routing. For example, you can route general requests to one target group and requests to render images to another target group. 

**Allow you to direct traffic to different EC2 instances based on the URL contained in the request.**

## Auto Scaling
1. **Groups** - Logical component. Webserver group or Application group or Database group, etc. **Groups of EC2 instances**.

1. **Configuration Templates** - Groups uses a launch template or a launch configuration as a configuration template for its EC2 instances. You can specify information such as the AMI ID, instance type, key pair, security groups, and block device mapping for your instances.

1. **Scaling Options** - Scaling Options provides several ways for you to scale your Auto Scaling groups. For example, you can configure a group to scale based on the occurrence of specified conditions (dynamic scaling) or on a schedule.
    * Maintain current instance levels at all times - maintain a specified number of running instances at all times. Auto Scaling performs a periodic health check on running instances within an EC2 Auto Scaling group. If an unhealthy one is found, it terminates it and launches a new one.

    * Scale manually - most basic. You only specify the change in max, min, or desired capacity of your group. EC2 Auto Scaling manages the process of creating or terminating instances to maintain the updated capacity.

    * Scaled based on a schedule - scaling actions are performed automatically as a function of time and date.

    * Scaled based on demand - lets you define parameters that control the scaling process. **Most popular type.**

    * Use predictive scaling - uses EC2 Auto Scaling in combination with AWS Auto Scaling to scale resources across multiple services. Predicts based on your previous performance when you're going to need scaling options.

* Components required to effectively setup Auto Scaling on the EC2 instances for a web-based application:
    * Launch Configuration

    * Elastic Load Balancer

    * AutoScaling Group

* Desired capacity - provides a target value for Auto Scaling to match. If a discrepancy between desired and actual exist, Auto Scaling will work to match the desired value

* Lifecycle Hooks - puts the instance into wait state before termination. During this wait state, you can perform custom activities, like retrieve critical operational data from a stateful instance.
    * Wait period - 1 hour

## HA Architecture
1. Always design for failure.

1. Use Multiple AZs and Multiple Regions wherever you can.

1. Know the difference between Multi-AZ and Read Replicas for RDS.
    * Multi-AZ - disaster recovery

    * Read Replicas - performance

1. KNow the difference between scaling out and scaling up
    * Scaling out is where we use Auto Scaling groups and add additional EC2 instances.

    * Scaling up - increase resources inside the EC2 instances.

### CloudFormation
A way of completely scripting the cloud environment. **Create environment templates.**

* Quick Start - a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex enviornments very quickly.

* Drift Detection - can be used to detect changes made to AWS resources outside the CloudFormation Templates. Only checks property values that are explicitly set by stack templates or by specifying template parameters. 

### Elastic Beanstalk
Quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications. Simply upload the application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

* Used to create Web Server environments and Worker environments.

## From the Quiz

* Availability - the likelihood of being able to acces a resource or service when needed.

* Resiliency - the likelyhood that a resource is able to recover from damange or disruption.

* Reliability - the likelihood that a resource will work as designed.

* Durability - the likelihood that a resource will continue to exist until you decide to remove it.