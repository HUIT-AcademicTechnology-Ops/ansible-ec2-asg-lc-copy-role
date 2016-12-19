EC2 Autoscaling Group Launch Configuration Override
=========

This role mimics the ability in the AWS console to copy an existing launch configuration.  The use case for this role requires that the launch configurations be associated with an autoscaling group.  The launch configuration details are retrieved  new launch configuration is created with overrides, installed in the ASG, and then the old LC is deleted.

Requirements
------------

* Ansible 1.8+
* awscli
* Boto3

Role Variables
--------------

| parameter                         | required | default | comments                                                            |   |
|-----------------------------------|----------|---------|---------------------------------------------------------------------|---|
| ec2_asg_lc_copy_asg_group_name    | yes      |         | The name of the autoscaling group associated with the launch config |   |
| ec2_asg_lc_copy_asg_lc_name       | yes      |         | The name of the launch configuration to copy                        |   |
| ec2_asg_lc_copy_boto_profile      | no       |         | The named boto/aws profile used to match credentials                |   |
| ec2_asg_lc_copy_delete_prior_lc   | no       |   yes   | Whether to delete the lc that was copied                            |   |
| ec2_asg_lc_copy_image_id          | no       |         | The image id lc override value                                      |   |
| ec2_asg_lc_copy_instance_profile  | no       |         | The instance profile name lc override value                         |   |
| ec2_asg_lc_copy_instance_type     | no       |         | The instance type lc override value                                 |   |
| ec2_asg_lc_copy_key_name          | no       |         | The ssh key name lc override value                                  |   |
| ec2_asg_lc_copy_region            | no       |         | The AWS region of the ASG/LC.  If not specified then the value of the AWS_REGION or EC2_REGION environment variable, if any, is used.                                        |   |
| ec2_asg_lc_copy_security_groups   | no       |         | The security groups lc override (list of group ids)                 |   |
| ec2_asg_lc_copy_user_data         | no       |         | The user data lc override                                           |   |


Dependencies
------------

The ec2_asg_facts Ansible extras module is handy to get the required group name and launch config name if you want to operate on a set
of ASGs at once.

Example Playbook
----------------

```
    - hosts: 127.0.0.1
      connection: local
      vars:
        ec2_asg_lc_copy_asg_group_name: my-cool-asg
        ec2_asg_lc_copy_asg_lc_name: my-cool-lc
        ec2_asg_lc_copy_region: us-east-1
      roles:
         - { role: ec2_asg_lc_copy }
```

License
-------

BSD

Author Information
------------------

Jaime Bermudez (jaime_bermudez@harvard.edu)
