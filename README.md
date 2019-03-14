## What's this?
This is a simple multi-tenant webhosting stack implemented in CloudFormation to host multiple (PHP) websites. Please note that it's intentionally not highly available.

## High level architecture overview
- EC2 instance for serving sites / running containers with multiple encrypted EBS volumes (root, swap, data)
- Elastic IP for the instance
- Encrypted RDS MySQL instance for databases
- ElastiCache memcached instance
- All resources isolated in a VPC

## Requirements
- Latest version of Packer
- Latest version of Ansible

## Building the base image
```
ansible-galaxy install -p playbook/galaxy -r playbook/requirements.yml
packer build base-image.json
```
The resulting AMI ID should be supplied to CloudFormation when building the stack in the `InstanceAMI` parameter.

## Tooling
This stack requires [wsman][wsman] to be installed to `/data/wsman`. The tool is tailored to manage sites on a hosting stack built by this template. This will be automated in the future.


[wsman]: https://github.com/janost/wsman
