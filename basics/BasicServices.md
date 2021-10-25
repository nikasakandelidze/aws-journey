# Basic ( Must know ) services and their descriptions in AWS cloud infrastructure

## VPC
### Description
Amazon's Virtual Private Network is a mechanism that enables you to launch other AWS services in a
private network, isolated from everything in the internet or in the AWS data centers. So we can look
at VPC as network, logical level unit of isolation where you can build archutectures and then manually
open some of routes in or out of the vpc. 
### Usage
For literally any project to run on machines ( virtual ) in datacenters of AWS there must be a VPC
present. For example if you want to create new instance of EC2 ( discussed right below this topic ) 
you must first create a VPC and configure all of it's networking correctly and only after this
you can create EC2 instance and place it inside of VPC, isolated, secured private environment.



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

