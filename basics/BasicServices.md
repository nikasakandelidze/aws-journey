# Basic ( Must know ) services and their descriptions in AWS cloud infrastructure

## EC2
### Description:
EC2 instance is simply a server, machine in some availability zone in some gobal region of AWS business.
By default each account can have max of 20 separate EC2 instances in each region. For more than 20 instances
per region direct approval/communication from AMAZON is required. 
### Usage:
For nearly every software project this is the basic building block, since this is a actual server 
( more like a virutal machine on a server ) Where you can install dependencies from the web 
like: python, node, docker, java, nginx, haproxy, etc and run them.

### Creation:	
Upon creating EC2 instance from either AWS-CLI or AWS-UI you can specify a property for AWS to create keys for you.
you can later download and use these keys to SSH into remote machine and do anything you want there like you would do
on your own one using terminal.
