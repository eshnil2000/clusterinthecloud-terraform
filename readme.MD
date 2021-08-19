Terraform configuration for Cluster in the Cloud
================================================

https://cluster-in-the-cloud.readthedocs.io

Changes required:

variables.tf
```
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
    cidr_blocks = ["YOUR.IP.ADDRESS/32"]
  }
```


After install script complete, add Management Instance IP address to the security group (created manually) of the Packer instance: 
```
sudo /usr/local/bin/run-packer
sudo -i
/root/run_ansible --skip-tags=packer
```

useful references:
* Speed up ratio
**** https://researchcomputing.princeton.edu/support/knowledge-base/slurm#multithreaded
* scaling analysis
**** https://researchcomputing.princeton.edu/support/knowledge-base/scaling-analysis
* cluster usage
**** https://github.com/eshnil2000/hpc_beginning_workshop_slurm_cluster/tree/master/05_effective_usage

* Sample Slurm file:
* https://github.com/eshnil2000/clusterinthecloud-terraform/blob/master/test.slm
