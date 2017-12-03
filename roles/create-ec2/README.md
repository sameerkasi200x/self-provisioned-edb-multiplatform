Role Name
=========

This role is to launch a new EC2 Instance and add to the inventory. You can use it for creating an instance with a particular name and then later use another playbook/role to perform tasks on that server e.g. install web server etc.


Requirements
------------
 * Python
 * Boto must be installed on the node where the role will be invoked. 
 * The node where the role will be invoked should be an EC2 Instance which has a role assigned with enough previleges to create another EC2 Instance. 
 * Currently it mandates you to pass ami, subnet, region and security group for creating the server. 

To do 
--------------

 * Going forward optional variables will be added to provide AWS Access Key and AWS Secret Key. This will allow this role to be invoked when invoking EC2 servers don't have appropriate role or when invoking server is not in EC2.
 * Allow users to add an array of volumes.
 * Going forward the variable will made optional and a subnet and security group will be created on the fly.
 * Provide a variable to control whether in the end Ansible inventory and host variables should be updated or not.

Role Variables
--------------
Below is a list of mandatory variables-
 * ami: Defines the AMI which has to be used for creating the instance. Default is ami-1fbad07c ([community Centos 7 Image](https://aws.amazon.com/marketplace/pp/B00O7WM7QW) )
 * sec_group: Defines the security group to be used for new instance. This is a mandatory parameter.
 * region: Region in which the new instance will be created. Default is ap-southeast-1 (Singapore). [Valid values are provided on AWS official documentation on region and availability zone](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-available-regions)
 * subnet: Subnet in which the new instance will be created. CUrrently this role does not offer facility to choose Availability Zone, hence you must have a subnet in desired availability zone and use it here. This is a mandatory parameter.
 * server: Server name. An entry of this name will be added to host_vars and file indicated by variable {{ inventory_file_path }}
 * ssh_key: SSH Key to be added to the instance. Default is MyEC2KeyPair.
 * instance_size: Size of instance. Default is t2.small. Refer [online documentation for other valid instance size](https://aws.amazon.com/ec2/instance-types/)
 * vol_size_gb: Size of the root device to be added. Default is 20 (unit is alway GB).
 * vol_type: Type of volume to be used for root device. Default is gp2.
 * ami_user: User to be used for ssh, as per the AMI. Default is centos.
 * ami_os: Os of your AMI. Default is CentOS.
 * ami_os_version: Version of the Operating System. Default is 7.

Dependencies
------------
This role does not need any other role.

Example Playbook
----------------
    hosts: localhost
    connection: local
    vars:
      ami: ami-1fbad07c
      sec_group: sg-77602f11
      region: ap-southeast-1
      subnet: subnet-9d05befe
      server: my_server
    roles:
      - create-ec2

An example for using this role for deploying a a Web Application is over here in my other GitHub repository [Basic Web Application with Ansible](https://github.com/sameerkasi200x/basic-web-app-with-ansible)


License
-------

GNU

Author Information
------------------
sameer.kasi200x@gmail.com
sameer.kumar@ashnik.com

Twitter: @sameerkasi200x
