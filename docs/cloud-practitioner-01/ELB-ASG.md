# Elastic Load Balancer & Auto Scaling Groups

## Scalability

A system's ability to adapt to changing load.

1. Vertical – increase size of instance
1. Horizontal – increase number of instances.

   - Implies distributed systems

1. High Availability – running application in at least 2 AZ
   - The goal is to survive a data center loss

## Elasticity

Ability to auto-scale based on load

## Load Balancers

Servers that forward internet traffic to multiple servers (EC2 instances) downstream.

### Benefits of a Load Balancer

1. Spread load across multiple downstream instances
1. Expose a single point of access (DNS) to your application
1. Seamlessly handle failures of downstream instances
1. Do regular health checks to your instances
1. Provide SSL termination (HTTPS) for your websites
1. HIgh availability across zones

### Elastic Load Balancers (ELB)

An AWS-managed load balancer.

- AWS guarantees it will be working
- AWS takes care of upgrades, maintenance, high availability
- AWS provides only a few configuration knobs
- Cheaper to make one yourself but a lot more effort
- 3 Kinds

  - Application Load Balancer – Layer 7

  - Network Load Balancer – Layer 4

  - Classic Load Balancer – retiring

## Auto-Scaling Group

- Scale out (add EC2) to match an increase in load
- Scale in (remove EC2) to match a decreased load
- Ensure we have a minimum and a maximum number of machines running
- Automatically register a new instance to a load balancer
- Replace unhealthy instances
- Cost savings – only run at an optimal capacity

### Scaling Strategies

1. Manual – update the size of an ASG manually
1. Dynamic – respond to changing demand (simple/step scaling)
1. Target tracking – you give a target to maintain
1. Scheduled – anticipate scaling based on known usage patterns
1. Predictive – uses Machine Learning to predict future traffic ahead of time
