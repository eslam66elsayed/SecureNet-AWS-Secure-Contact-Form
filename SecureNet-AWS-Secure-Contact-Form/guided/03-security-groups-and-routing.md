# Security Groups and Routing

Traffic model:

```text
Internet -> ALB SG
ALB SG -> App SG : TCP 5000
App SG -> RDS SG : TCP 3306
```

Security Groups are stateful. Keep RDS 3306 and app port 5000 restricted to the required source Security Groups.

Route tables determine the next hop. Examples include `0.0.0.0/0 -> IGW`, `10.1.0.0/16 -> Transit Gateway`, and the S3 prefix list -> S3 Gateway Endpoint.
