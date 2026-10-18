# SecureNet AWS Secure Contact Form

Secure, highly available AWS contact-form application using CloudFront, private S3, WAF, ALB, private EC2 Flask/Gunicorn application servers, private RDS MySQL, SNS, SSM, VPC endpoints, Flow Logs, Athena, CloudWatch, and Transit Gateway.

## Architecture

```text
User -> CloudFront + WAF
          |-> private S3 frontend (OAC)
          |-> /api/* -> ALB -> private EC2 #1/#2 -> RDS MySQL
                                            |
                                            +-> SNS admin notification

Private administration: SSM Session Manager -> SSM/SSMMessages interface endpoints
Private AWS access: S3 Gateway VPC Endpoint
Observability: VPC Flow Logs -> S3 -> Athena, CloudWatch metrics/alarms
Networking: VPC 10.0.0.0/16 <-> Transit Gateway <-> VPC 10.1.0.0/16
```

## Repository structure

```text
SecureNet-AWS-Secure-Contact-Form/
├── README.md
├── .gitignore
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   ├── .env.example
│   └── systemd/contact-api.service
├── images/
│   ├── architecture.svg
│   └── README.md
└── guided/
    ├── 00-resource-reference.md
    ├── 01-project-overview.md
    ├── 02-vpc-and-subnets.md
    ├── 03-security-groups-and-routing.md
    ├── 04-ec2-backend.md
    ├── 05-alb.md
    ├── 06-rds.md
    ├── 07-s3-cloudfront-waf.md
    ├── 08-ssm-and-vpc-endpoints.md
    ├── 09-flow-logs-athena-cloudwatch.md
    ├── 10-sns.md
    ├── 11-transit-gateway.md
    ├── 12-testing.md
    └── 13-interview-questions.md
```

## Application flow

1. User opens CloudFront.
2. CloudFront serves the private S3 frontend through OAC.
3. Frontend sends `POST /api/contact`.
4. CloudFront routes `/api/*` to the ALB.
5. ALB forwards to a healthy private EC2 target on port 5000.
6. Flask validates the request.
7. Flask inserts into RDS table `contact_messages`.
8. After commit, SNS publishes the admin notification.
9. API returns the result to the frontend.

## Environment variables

```env
DB_HOST=your-rds-endpoint
DB_PORT=3306
DB_NAME=securenet
DB_USER=admin
DB_PASSWORD=your-password
AWS_REGION=us-east-1
SNS_TOPIC_ARN=arn:aws:sns:us-east-1:ACCOUNT_ID:SecureNet-Admin-Notifications
```

Never commit `.env`, passwords, access keys, or private keys.

## Database table

```sql
CREATE TABLE IF NOT EXISTS contact_messages (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(120) NOT NULL,
    email VARCHAR(255) NOT NULL,
    subject VARCHAR(255) NOT NULL,
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Backend

The application uses Flask + Gunicorn and listens on port 5000.

```bash
gunicorn --workers 3 --bind 0.0.0.0:5000 app:app
```

Health check:

```bash
curl http://127.0.0.1:5000/health
```

## Security model

```text
Internet -> ALB SG -> App SG:5000 -> RDS SG:3306
```

EC2 instances are private and are administered with SSM Session Manager instead of public SSH. RDS has Public Access disabled. S3 blocks public access and is accessed by CloudFront OAC.

## Known project values

- Region: `us-east-1`
- VPC: `Secure-Network-VPC`
- VPC CIDR: `10.0.0.0/16`
- Public subnets: `10.0.1.0/24`, `10.0.2.0/24`
- Private app subnets: `10.0.11.0/24`, `10.0.12.0/24`
- Private DB subnets: `10.0.21.0/24`, `10.0.22.0/24`
- S3 bucket: `secure-network-origin-123`
- CloudFront distribution ID: `E1YUP14VLB6ENI`
- ALB DNS: `contactform-ALB-1366953573.us-east-1.elb.amazonaws.com`
- RDS endpoint: `secure-rds.c6tem6koux1i.us-east-1.rds.amazonaws.com`
- RDS DB: `securenet`
- RDS user: `admin`
- RDS port: `3306`
- SNS topic: `SecureNet-Admin-Notifications`

## Upload to GitHub

```bash
git init
git add .
git commit -m "Initial SecureNet AWS project"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/SecureNet-AWS-Secure-Contact-Form.git
git push -u origin main
```
