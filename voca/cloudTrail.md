# CloudTrail

## Case 1.

- Web applications hosted in multiple VPCs in various AWS regions.
- need to set up a logging solution to track all of the changes made to their AWS resources in all regions
- use Amazon EC2 instances, Amazon S3 buckets, CloudFront web distributions, and AWS IAM.
- must ensure the security, integrity, and durability of log data
- should provide an event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and API calls.

## Solution

CloudTrail can be used for this case with multi-region trail enabled. However, CloudTrail will only cover the activities of the regional services (EC2, S3, RDS etc.) and not for global services such as IAM, CloudFront, AWS WAF, and Route 53. However, if we enable **-include-global-service-events parameter**,
it will also include activity from global services such as IAM, Route 53, AWS WAF, and CloudFront

First, creating a new AWS CloudTrail trail in a new S3 bucket using the AWS CLI and also pass both the "--is-multi-region-trail" and "--include-global-service-events" parameters, and then encrypt log files using KMS encryption. Next, **Enable Multi-Factor Authentication (MFA) Delete on the S3 bucket** and ensure that only authorized users can access the logs by configuring the bucket policies.

## References:

https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-concepts.html#cloudtrail-concepts-global-service-events

https://docs.aws.amazon.com/IAM/latest/UserGuide/cloudtrail-integration.html

https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail-by-using-the-aws-cli.html

AWS CloudTrail Cheat Sheet:

https://tutorialsdojo.com/aws-cloudtrail/
