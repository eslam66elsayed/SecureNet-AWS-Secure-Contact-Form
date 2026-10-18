# SSM and VPC Endpoints

EC2 administration uses Systems Manager Session Manager instead of public SSH.

Interface endpoints:

- `com.amazonaws.us-east-1.ssm`
- `com.amazonaws.us-east-1.ssmmessages`

The endpoint Security Group must allow TCP 443 from the EC2/App Security Group. Private DNS should be enabled.

S3 uses a Gateway VPC Endpoint, which is different from PrivateLink interface endpoints.

Troubleshooting Session Manager: confirm the node is online, IAM role includes `AmazonSSMManagedInstanceCore`, endpoints are Available, endpoint SG allows 443, and DNS/network settings are correct.
