# ansible-ecs-example

Example project which uses the following roles to provision a full AWS ECS solution from scratch:

* aws-vpc: Create a VPC to hold the ECS cluster;
* aws-security-groups: Creates the security groups to apply to the EC2 instances;
* aws-elb: Creates an ELB for an example ECS service;
* aws-route53-elb: Registers a custom domain name for the ELB;
* aws-ecs-autoscale: Creates an ECS cluster with an Auto Scaling EC2 group.

See the `group_vars` directory for the variables used in the obviously named playbooks (provision and decommission).

Run the provisioning playbook by:

```
$ ansible-playbook provision.yml --private-key=<my-private-key>.pem -u ubuntu -vvv -e my_route53_zone=<my-domain> -e ssh_key_name=<my-key-name>
```

You'll need need to provide your own:

* `<my-private-key>` location of the pem file which corresponds to;
* `<my-key-name>` name of the key/pair registered with AWS to use for the EC2 instances;
* `<my-domain>` custom domain you have setup in route 53 which the ELB will register to.

The last step doesn't matter too much - you can make up whatever domain name up you like.  But obviously you'll only be able to access the ELB from the normal ELB DNS name not a custom one.

## Dependencies

This project requires Ansible 2.1, which at present has not yet been release.  You can use the development version of Ansible and build your own release.  To greatly simplify this process use a Vagrant file like this project https://github.com/daniel-rhoades/ansible-environment

Additionally, even the development branch isn't enough because AWS security groups is currently broken pending https://github.com/ansible/ansible-modules-core/pull/3117 once this is merged all will be well.  In the meantime, the patched file is included in the `library` directory of this project and automatically used by Ansible.