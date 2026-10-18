# S3, CloudFront and WAF

S3 stores the frontend and remains private. CloudFront accesses it through Origin Access Control.

Typical CloudFront routing:

```text
Default -> S3
/api/* -> ALB
```

API caching should not be used for POST requests.

WAF inspects HTTP requests and can block malicious patterns. Shield Standard provides baseline DDoS protection for supported AWS services.
