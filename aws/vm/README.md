## AWS Virtual Machine (Ec2) module

### Introduction

This module will create:
 - An AWS Ec2 (VM) instance;
 - An AWS Elastic (static) IP or not, based on the parameters;
 - An AWS EBS (disk) for each instance or not, based on the parameters;
 - Attach each EBS at the respective instance.

### Usage example

 ```hcl
module "aws_production_unknown_cluster" {
  source              = "git@github.com:jeanguirro/terraform-modules.git//aws/vm"
  project_name        = "${module.aws_production_vpc.project_name}"
  subnets             = "${module.aws_production_vpc.private_subnets}"
  instance_size       = "t3.medium"
  instance_of         = "unknown-cluster"
  instance_count      = 3
  use_public_subnet   = false
  create_data_volumes = true
  data_volume_size    = 50
  data_volume_type    = "gp2"
  ami_info            = "${var.default_amis["debian"]}"

  env = "${module.aws_production_vpc.environment}"
}
```
