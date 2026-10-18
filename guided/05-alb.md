# Application Load Balancer

The ALB receives HTTP application traffic and forwards it to the target group on port `5000`.

Health check: `/health`.

If an EC2 target becomes unhealthy, the ALB removes it from normal traffic distribution and uses healthy targets.
