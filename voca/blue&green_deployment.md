# Blue/green deployments

## Case 1.

Four large banks in the country have collaborated to create a secure, simple-to-use, mobile payment app that enables users to easily transfer money and pay bills without much hassle. With the new mobile payment app, anyone can easily pay another person, split the bill with their friends, or pay for their coffee in an instant with just a few taps in the app. The payment app is available on both Android and iOS devices, including a web portal that is deployed in AWS using OpsWorks Stacks and EC2 instances. It was a big success with over 5 million users nationwide and has over 1000 transactions every hour. After one year, a new feature that will enable the users to store their credit card information in the app is ready to be added to the existing web portal. However, due to PCI-DSS compliance, the new version of the APIs and web portal cannot be deployed to the existing application stack.

How would the solutions architect deploy the new web portal for the mobile app without having any impact on 5 million users?

### Explanation

`Blue/green deployments` provide near zero-downtime release and rollback capabilities. The fundamental idea behind blue/green deployment is to shift traffic between two identical environments that are running different versions of your application. The blue environment represents the current application version serving production traffic. In parallel, the green environment is staged running a different version of your application. After the green environment is ready and tested, production traffic is redirected from blue to green. If any problems are identified, you can roll back by reverting traffic back to the blue environment.

`AWS OpsWorks` has the concept of stacks, which are logical groupings of AWS resources (EC2 instances, Amazon RDS, Elastic Load Balancing, and so on) that have a common purpose and should be logically managed together. Stacks are made of one or more layers. A layer represents a set of EC2 instances that serve a particular purpose, such as serving applications or hosting a database server. When a data store is part of the stack, you should be aware of certain data management challenges.

Next, create the green environment/stack with the newer version of the application. At this point, the green environment is not receiving any traffic. If Elastic Load Balancing needs to be pre-warmed, you can do it at this time.

When it’s time to promote the green environment/stack into production, update DNS records to point to the green environment/stack’s load balancer. You can also do this DNS flip gradually by using the Amazon Route 53 weighted routing policy.

To implement this technique in AWS OpsWorks, bring up the blue environment/stack with the current version of the application.

### Solution

`Deploy a new OpsWorks stack that contains a new layer with the latest web portal version. Shift traffic between existing stack and new stack, running different versions of the web portal using Blue/Green deployment strategy by using Route53. Route only a small portion of incoming production traffic to use the new application stack while maintaining the old application stack. Check the features of the new portal; once it's 100% validated, slowly increase incoming production traffic to the new stack. If there are issues on the new stack, change Route53 to revert to the old stack.`

If you forcibly deploy the new web portal to the existing application stack and there is an issue on the deployment, then there would be some inevitable downtime in order for you to fix the system and revert back to the original version. It is better to use blue/green deployments instead.

Although the current application stack can still be used if something goes wrong, the risk of service disruption is quite high when you direct all incoming traffic to the new portal. If something did go wrong, there would be a downtime in order for you to switch back to the old stack.

## References:

https://d0.awsstatic.com/whitepapers/AWS_Blue_Green_Deployments.pdf

https://docs.aws.amazon.com/whitepapers/latest/blue-green-deployments/clone-a-stack-in-aws-opsworks-and-update-dns.html

https://docs.aws.amazon.com/opsworks/latest/userguide/best-deploy.html

Check out this AWS OpsWOrks Cheat Sheet:

https://tutorialsdojo.com/aws-opsworks/
