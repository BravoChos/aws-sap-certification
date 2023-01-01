# Description

A retail company hosts its web application on an Auto Scaling group of Amazon EC2 instances deployed across multiple Availability Zones. The Auto Scaling group is configured to maintain a minimum EC2 cluster size and automatically replace unhealthy instances. The EC2 instances are behind an Application Load Balancer so that the load can be spread evenly on all instances. The application target group health check is configured with a fixed HTTP page that queries a dummy item on the database. The web application connects to a Multi-AZ Amazon RDS MySQL instance. A recent outage caused a major loss to the company's revenue. Upon investigation, it was found that the web server metrics are within the normal range but the database CPU usage is very high, causing the EC2 health checks to timeout. Failing the health checks, the Auto Scaling group continuously replaced the unhealthy instances thus causing the downtime.

Which of options should the Solution Architect implement to prevent this from happening again and allow the application to handle more traffic in the future?

## Explanation

`Amazon Route 53` health checks monitor the health and performance of your web applications, web servers, and other resources. Each health check that you create can monitor one of the following:

- `The health of a specified resource, such as a web server` - You can configure a health check that monitors an endpoint that you specify either by IP address or by the domain name. At regular intervals that you specify, Route 53 submits automated requests over the Internet to your application. You can configure the health check to make requests similar to those that your users make, such as requesting a web page from a specific URL.

- `The status of other health checks` - You can create a health check that monitors whether Route 53 considers other health checks healthy or unhealthy. One situation where this might be useful is when you have multiple resources that perform the same function, such as multiple web servers, and your chief concern is whether some minimum number of your resources are healthy.

- `The status of an Amazon CloudWatch alarm` - You can create CloudWatch alarms that monitor the status of CloudWatch metrics, such as the number of throttled read events for an Amazon DynamoDB database or the number of Elastic Load Balancing hosts that are considered healthy.

After you create a health check, you can get the status of the health check, get notifications when the status changes, and configure DNS failover. To improve resiliency and availability, Route 53 doesn't wait for the CloudWatch alarm to go into the ALARM state. The status of a health check changes from healthy to unhealthy based on the data stream and on the criteria in the CloudWatch alarm.

<img src="./assets/sapsap_route53_failover_sns_sam.png" width="60%">
<br/>

`Application Load Balancer` periodically sends requests to its registered targets to test their status. These tests are called health checks. Each load balancer node routes requests only to the healthy targets in the enabled Availability Zones for the load balancer. Each load balancer node checks the health of each target, using the health check settings for the target groups with which the target is registered. After your target is registered, it must pass one health check to be considered healthy. After each health check is completed, the load balancer node closes the connection that was established for the health check. If a target group contains only unhealthy registered targets, the load balancer nodes route requests across its unhealthy targets.

Each health check will be executed at configured intervals to all the EC2 instances so if the health check query page involves a database query, there will be several simultaneous queries to the database. This can increase the load of your database tier if there are many EC2 instances and the health check interval period is very quick.

`Amazon ElastiCache` is a web service that makes it easy to set up, manage, and scale a distributed in-memory data store or cache environment in the cloud. It provides a high-performance, scalable, and cost-effective caching solution. At the same time, it helps remove the complexity associated with deploying and managing a distributed cache environment.

ElastiCache for Memcached has multiple features to enhance reliability for critical production deployments:

- Automatic detection and recovery from cache node failures.

- Automatic discovery of nodes within a cluster enabled for automatic discovery, so that no changes need to be made to your application when you add or remove nodes.

- Flexible Availability Zone placement of nodes and clusters.

- Integration with other AWS services such as Amazon EC2, Amazon CloudWatch, AWS CloudTrail, and Amazon SNS to provide a secure, high-performance, managed in-memory caching solution.

## Solution

`Change the target group health check to a simple HTML page instead of a page that queries the database. Create an Amazon Route 53 health check for the database dummy item web page to ensure that the application works as expected. Set up an Amazon CloudWatch alarm to send a notification to Admins when the health check fails`

Changing the target group health check to a simple HTML page will reduce the queries to the database tier. The Route 53 health check can act as the “external” check on a specific page that queries the database to ensure that the application is working as expected. The Route 53 health check has an overall lower request count compared to using the target group health check.

`Reduce the load on the database tier by creating an Amazon ElastiCache cluster to cache frequently requested database queries. Configure the application to use this cache when querying the RDS MySQL instance`

Since this is a retail web application, most of the queries will be read-intensive as customers are searching for products. ElastiCache is effective at caching frequent requests which overall improves the application response time and reduces database queries.

Creating read replicas is recommended to increase the read performance of an RDS cluster. However, the Amazon RDS MySQL does not have a single reader endpoint for read replicas. You must use Amazon Aurora for MySQL to support this.

An Application Load Balancer does not support a TCP health check. ALB only supports HTTP and HTTPS target health checks.

Recovering the database instance results in downtime. If you have the Multi-AZ enabled, the standby database will shoulder all the load causing it to crash too. It is better to scale the database by creating read replicas or adding an ElastiCache cluster in front of it.

## References:

https://docs.aws.amazon.com/elasticloadbalancing/latest/application/target-group-health-checks.html

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-types.html

https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/WhatIs.html

Check out these Amazon ElastiCache and Amazon RDS Cheat Sheets:

https://tutorialsdojo.com/amazon-elasticache/

https://tutorialsdojo.com/amazon-relational-database-service-amazon-rds/
