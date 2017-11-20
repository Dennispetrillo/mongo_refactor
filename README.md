# mongo_refactor

The goal here was to refactor mongodb1 by using cookbooks available from the supermarket.

For this effort I used sc-mongodb cookbook version 1.0.0 from the supermarket https://supermarket.chef.io/cookbooks/sc-mongodb#knife

Implementation consisted of 3 parts:
- Adding an attribute file to contain some default attributes to capture the name of the package (mongodb-org) 
- Including the sc-mongodb cookbook::recipe in the default recipe
- Modifying the metadata.rb to include depends on sc-mongodb and the version

## Background

This cookbook is using the following software versions:
- Chef Develpment Kit version: 2.3.4
- Chef-client version: 13.4.19
- berks version: 6.3.1
- kitchen version: 1.17.0
- inspec version: 1.36.1
- Mongo 3.4 Community Edition

Cookbook developed locally and uploaded to chef-server

Bootstrapped to ec2 node using SSH

Node = AWS ec2 RHEL 7.4 64-bit instance

## setup (assuming chefdk and tools are on the workstation)

- Fork this repo to your cookbooks directory within your chef-repo directory
- Upload cookbook to chef server
- Create an ec2 instance
    - RHEL 7.4 64-bit
    - Create a .pem key when creating the instance if one not already created.  Option available when creating the instance         and needed for bootstrapping the node and accessing the node in local mode using the methods below.
    - Store the .pem in ~/.ssh/YourPemName.pem
- Bootstrap the node (here is one format that may be used at the command line of the local workstation)
  knife bootstrap IDPADDRESS --ssh-user ec2-user --sudo --identify-file ~/.ssh/YourPemFileName.pem -N NODENAME --run-list 'cookbook::recipe'
- The above should compile, converge and perform a chef client run
- Log in to the node remotely.  Here is one format that may be used at the command line of the local workstation
        ssh -i ~/.ssh/YourPemKeyFileName.pem ec2-user@IPADDRESS-OF-THE-NODE
- Enter mongo and a connection to mongodb shell should be initiated

