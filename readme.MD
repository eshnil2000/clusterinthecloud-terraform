Terraform configuration for Cluster in the Cloud
================================================

https://cluster-in-the-cloud.readthedocs.io

Changes required:

variables.tf

# AWS Information
variable "region" {
  default = "us-west-1"
}
```

security-groups.tf
```
resource "aws_security_group" "mgmt" {
  name        = "citc-mgmt-${local.cluster_id}"
  description = "Management node"
  vpc_id      = aws_vpc.vpc_network.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["73.48.134.89/32"]
  }
```
