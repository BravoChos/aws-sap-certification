# CloudFront

## Case 1.

A global financial company is launching its new trading platform in AWS which allows people to buy and sell their bitcoin, ethereum, ripple, and other cryptocurrencies, as well as access to various financial reports. To meet the anti-money laundering and counter-terrorist financing (AML/CFT) measures compliance, all report files of the trading platform must not be accessible in certain countries which are listed in the Financial Action Task Force (FATF) list of non-cooperative countries or territories. You were given a task to ensure that the company complies with this requirement to avoid hefty monetary penalties.

In this scenario, what is the best way to satisfy this security requirement in AWS while still delivering content to users around the globe with lower latency?

## Explanation

We can use `geo restriction` - also known as `geoblocking` - to prevent users in specific geographic locations from accessing content that you're distributing through a CloudFront web distribution. To use geo restriction, you have two options:

Use the `CloudFront` geo restriction feature. Use this option to restrict access to all of the files that are associated with a distribution and to restrict access at the country level.

Use a third-party geolocation service. Use this option to restrict access to a subset of the files that are associated with a distribution or to restrict access at a finer granularity than the country level.

When a user requests your content, CloudFront typically serves the requested content regardless of where the user is located. If you need to prevent users in specific countries from accessing your content, you can use the CloudFront geo restriction feature to do one of the following:

Allow your users to access your content only if they're in one of the countries on a whitelist of approved countries.

Prevent your users from accessing your content if they're in one of the countries on a blacklist of banned countries.

For example, if a request comes from a country where, for copyright reasons, you are not authorized to distribute your content, you can use CloudFront geo restriction to block the request.

## Solution

Create a CloudFront distribution with Geo-Restriction enabled to block all of the blacklisted countries from accessing the trading platform is correct. CloudFront can provide the users low-latency access to the files as well as block certain countries on the FTAF list.

Blocking all of the IP addresses of each blacklisted country in the Network Access Control List entails a lot of work and is not a recommended way to accomplish the task. Using CloudFront geo restriction feature is a better solution for this.

Route 53 only provides Domain Name Resolution and sends the requests based on the configured entries. It does not provide low-latency access to users around the globe, unlike CloudFront.

`Geolocation` routing policy is used when you want to route traffic based on the location of your users while `Geoproximity` routing policy is for scenarios where you want to route traffic based on the location of your resources and, optionally, shift traffic from resources on one location to resources in another.

## Reference:

https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html

Check out this Amazon CloudFront Cheat Sheet:

https://tutorialsdojo.com/amazon-cloudfront/

Latency Routing vs Geoproximity Routing vs Geolocation Routing:

https://tutorialsdojo.com/aws-cheat-sheet-latency-routing-vs-geoproximity-routing-vs-geolocation-routing/

Comparison of AWS Services Cheat Sheets:

https://tutorialsdojo.com/comparison-of-aws-services-for-udemy-students/
