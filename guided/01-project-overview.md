# Project Overview

SecureNet is a layered AWS contact-form application. The frontend is private S3 content delivered by CloudFront. API traffic is routed through CloudFront to an ALB, then to private EC2 Flask servers. Flask writes to private RDS MySQL and publishes an SNS notification after the database commit.

The project demonstrates defense in depth: network segmentation, Security Groups, IAM roles, private endpoints, WAF, logging, monitoring, and controlled VPC-to-VPC connectivity.
