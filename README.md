Ansible Role: EC2 Launch Configuration Copy
=========

This role mimics the ability in the AWS console to copy an existing launch configuration, with the added optional functionality of replacing the launch configuration associated with an ASG.  The role expects a launch configuration name identifier to run.  The launch configuration details are retrieved, and a new launch configuration is created with overrides.  Optionally, the launch configuration copy is installed in a given ASG, and then the old LC is removed.

Requirements
------------

* Ansible 2.3+
* boto3

Role Variables
--------------

| parameter                     | required | default | comments                                                            |   |
|-------------------------------|----------|---------|---------------------------------------------------------------------|---|
| ec2_lc_copy_lc_name           | yes      |         | The name of the launch configuration to copy                        |   |
| ec2_lc_copy_asg_name          | no       |         | The name of the autoscaling group to associate with the new lc      |   |
| ec2_lc_copy_boto_profile      | no       |         | The named boto/aws profile used to match credentials                |   |
| ec2_lc_copy_delete_prior_lc   | no       |   no    | Whether to delete the lc that was copied                            |   |
| ec2_lc_copy_image_id          | no       |         | The image id lc override value                                      |   |
| ec2_lc_copy_instance_profile  | no       |         | The instance profile name lc override value                         |   |
| ec2_lc_copy_instance_type     | no       |         | The instance type lc override value                                 |   |
| ec2_lc_copy_key_name          | no       |         | The ssh key name lc override value                                  |   |
| ec2_lc_copy_region            | no       |         | The AWS region of the ASG/LC.  If not specified then the value of the AWS_REGION or EC2_RN environment variable, if any, is used.                                        |   |
| ec2_lc_copy_security_groups   | no       |         | The security groups lc override (list of group ids)                 |   |
| ec2_lc_copy_user_data         | no       |         | The user data lc override                                           |   |


Dependencies
------------

None


Example Playbook
----------------

```
    - hosts: 127.0.0.1
      connection: local
      vars:
        ec2_lc_copy_lc_name: my-cool-lc
        ec2_lc_copy_region: us-east-1
      roles:
         - { role: ec2_lc_copy }
```

License
-------

BSD

Author Information
------------------

Jaime Bermudez (jaime_bermudez@harvard.edu)
