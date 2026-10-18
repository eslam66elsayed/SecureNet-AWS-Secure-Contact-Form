# Transit Gateway

Main VPC: `10.0.0.0/16`.

Second VPC: `10.1.0.0/16`.

The main VPC route table sends `10.1.0.0/16` to the Transit Gateway. The second VPC sends `10.0.0.0/16` to the Transit Gateway.

Transit Gateway provides centralized private connectivity and scales better than maintaining many individual VPC peering relationships as the network grows.
