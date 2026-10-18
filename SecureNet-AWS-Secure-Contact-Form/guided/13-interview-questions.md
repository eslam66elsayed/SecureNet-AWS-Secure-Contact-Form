# Discussion Questions

### Why private EC2?
To avoid direct internet exposure and force application traffic through controlled entry points.

### Why ALB?
HTTP load balancing and health checks across multiple application servers.

### Why private RDS?
The database should only be reachable by the application tier.

### Why Security Groups?
Stateful resource-level network filtering.

### Why SSM instead of SSH?
Managed administration without exposing port 22 publicly.

### Why VPC endpoints?
Private connectivity from private subnets to supported AWS services.

### Is S3 Gateway Endpoint the same as PrivateLink?
No. S3 Gateway Endpoint is route-table based; interface endpoints use PrivateLink and ENIs.

### Why CloudFront?
Edge delivery, HTTPS, central entry point, and integration with WAF.

### Why WAF?
Layer-7 HTTP request filtering.

### Why Flow Logs?
Network visibility and investigation of accepted/rejected traffic.

### Why SNS?
Decoupled administrator notifications.

### What if one EC2 fails?
ALB health checks remove the unhealthy target and continue with the healthy target.

### What if RDS fails?
New submissions cannot be persisted; the application returns an error and monitoring should expose the failure.

### What is defense in depth?
Multiple independent controls across network, identity, application, edge, and monitoring layers.
