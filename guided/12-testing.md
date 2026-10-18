# Testing Checklist

- Open CloudFront URL and submit a form.
- Check ALB `/health` returns 200.
- Verify both ALB targets are healthy.
- Query `contact_messages` in RDS.
- Confirm SNS admin email.
- Connect to EC2 using SSM.
- Check Flow Logs/Athena.
- Check CloudWatch alarms.
- Check WAF metrics.
- If Transit Gateway testing is enabled, test only approved private CIDRs.
- Remove temporary broad ICMP rules after testing.
