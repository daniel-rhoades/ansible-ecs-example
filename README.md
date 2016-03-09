# ansible-ecs-example

Example project which uses the following roles to provision a full AWS ECS solution from scratch:

* aws-vpc: Create a VPC to hold the ECS cluster;
* aws-security-groups: Creates the security groups to apply to the EC2 instances;
* aws-ecs-autoscale: Creates an ECS cluster with an Auto Scaling EC2 group.

See the `group_vars` directory for the variables used in the obviously named playbooks (provision and decommission).