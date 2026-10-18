# SNS

Topic: `SecureNet-Admin-Notifications`.

Flow:

```text
POST -> validate -> RDS INSERT -> COMMIT -> SNS publish -> admin email
```

The EC2 IAM role needs least-privilege `sns:Publish` permission scoped to the topic ARN. AWS credentials must never be placed in frontend JavaScript.
