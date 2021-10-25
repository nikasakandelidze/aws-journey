# Basic ( Must know ) services and their descriptions in AWS cloud infrastructure

## VPC
### Description
Amazon's Virtual Private Network is a configurable networking layer for EC2 instances.
VPC is a wrapper service that enables you to launch other AWS services in a
private network, isolated from everything in the internet or in the AWS data centers. So we can look
at VPC as network, logical level unit of isolation where you can build archutectures and then manually
open some of routes in or out of the vpc.

#### Very cool description from Stack overflow:
At a high level, you can think of a VPC in AWS as a logical container that separates resources you create
from other customers within the Amazon Cloud. It is you defining a network of your own within Amazon.
You can think of a VPC like an apartment where your furniture and items are analogous to databases and instances.
The walls of your apartment isolate and protect your things from being accessible to other tenants of the apartment complex.

Subnets would then be analogous to the different rooms in your apartment. They are containers within your VPC that segment off a slice of the CIDR block you define in your VPC.
Subnets allow you to give different access rules and place resources in different containers where those rules should apply. 
You wouldn't have a big open window in your bathroom on the shower wall so people can see you naked, much like you wouldn't put a database with secretive information in a public 
subnet allowing any and all network traffic. You might put that database in a private subnet (i.e. a locked closet).

### Usage
For literally any project to run on machines ( virtual ) in datacenters of AWS there must be a VPC
present. For example if you want to create new instance of EC2 ( discussed right below this topic ) 
you must first create a VPC and configure all of it's networking correctly and only after this
you can create EC2 instance and place it inside of VPC, isolated, secured private environment.
### Concepts
Virtual Private Cloud  - virtual network dedicated to your organizationa/private account.

Subnet - sub structure of VPC with own autonomius network configuration. So to understand well, all AWS services grouped
by same broad network configurations go into same subnets. 

Route table - structure, table where rules of network packet routings are configured/specified ( in-out traffic )

### Billing
There's no additional charge for using a VPC. There are charges for some VPC components, such as NAT gateways, Reachability Analyzer, and traffic mirroring.

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
#Billing
Your Amazon EC2 usage is calculated by either the hour or the second based on the size of the instance, operating system,
 and the AWS Region where the instances are launched. Pricing is per instance-hour consumed for each instance, from the time an instance is launched until it is terminated or stopped.

