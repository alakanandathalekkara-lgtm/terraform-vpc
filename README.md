# Terraform: AWS VPC

Creates a VPC with two public and two private subnets across two availability zones,
an internet gateway, and public/private route tables. Subnet IDs are output.

## Usage
    terraform init
    terraform plan
    terraform apply
    terraform output
    terraform destroy

## Variables
`region`, `project`, `vpc_cidr`, `public_subnet_cidrs`, `private_subnet_cidrs`
(all have defaults, see `variables.tf`).

## Credentials
No keys in code. Terraform uses an IAM role attached to the EC2 instance
(`AmazonVPCFullAccess`).

## Design note
The public route table sends `0.0.0.0/0` to the internet gateway. The private route
table has only the local route, so those subnets have no internet access. A NAT gateway
was left out because it is billed hourly.
