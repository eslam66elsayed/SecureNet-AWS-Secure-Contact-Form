# VPC and Subnets

VPC CIDR: `10.0.0.0/16`

Public: `10.0.1.0/24`, `10.0.2.0/24`

Private App: `10.0.11.0/24`, `10.0.12.0/24`

Private DB: `10.0.21.0/24`, `10.0.22.0/24`

A subnet is public because its route table provides a route to an Internet Gateway. The app and database tiers are private to prevent direct internet exposure and reduce attack surface.
