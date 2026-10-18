# Flow Logs, Athena and CloudWatch

VPC Flow Logs record network metadata such as source/destination, ports, protocol, packets, bytes, and ACCEPT/REJECT action. They do not capture packet payloads.

Flow Logs are stored in S3 and can be queried with Athena.

CloudWatch is used for metrics, logs and alarms such as EC2 CPU, ALB unhealthy targets/5xx responses, and RDS health indicators.
