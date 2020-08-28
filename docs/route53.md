# Route53

## DNS
Converts human-friendly domain names into an Internet Protocol (IP) address.

* IP Addresses - used by computers to identify each other on the network. 
    * IPv4 
    * IPv6

* ELBs don't have IPv4 addresses. You have to resolve them with a DNS name.

* Alias

* CNAME

* Common DNS Types
    * SOA Records

    * NS Records

    * A Records

    * CNAMES

    * MX Records

    * PTR Records


## Route53 Routing Policies

1. **Simple Routing Policy** - it is only possible to have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.

1. **Weighted Routing Policy** - you set percentages of traffic that each EC2 instance gets.

1. **Latency Routing Policy** - based on user's location. They will get to the EC2 instance that provides them with fastest connection.

1. **Failover Routing Policy** - you set an active and a passive instance. If the active instance goes down, it re-routes traffice to the passive instance. It detects if the instance goes down through a health check.

1. **Geolocation Routing Policy** - it knows where the users are located and sends them to the instance as you've chosen to send them based on their location.

1. **Geoproximity Routing Policy** - allows you to route traffic based on the location of your users and your resources. It is necessary to be using Route 53 traffic flow.

1. **Multivalue Answer** - lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. Allows you to put health checks on each record set. **Simple Routing with Health checks**.

### Health Checks

* You can set health on individual record sets.

* If a record set fails a health check it will be removed from Route 53 until it passes the health check.

* You can set SNS notifications to alert you if a health check is failed.