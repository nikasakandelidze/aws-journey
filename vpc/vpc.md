# VPC ( Virtual Private Cloud )

## What is VPC
VPC is virtual private cloud is virtual and isolated network. In VPC-s we can place EC2 instances and
network resources of many othjer aws services. By default all VPC-s are isolated but we can connect them to each other or to
internet by configuring them accordingly.

When creating a VPC, you must create one specific VPC in one specific region. Each VPC created in some region will appear in
only that region and not others.
VPC is actually a kind of TCP/IP network, but scalable. and to reach this scalability point all hardware components like routers, vlans and etc.. are
abstracted away and are called different names in aws vpc.

## VPC CIDR block 
You must explicitly tell VPC that you are going to create in what ip address range will reosurces in this VPC be assigned to. For this range specification
CIDR notation is used. CIDR is classless interdomain routing mechanism which is also called prefix or ip slash mechanism and denotes number of available
ip addresses in speecific network.

If you plan to connect your VPC to another network—whether an on-premises net- work or another VPC—be sure the VPC CIDR you choose doesn’t overlap with addresses already in use on the other network.
You can’t change the primary CIDR block after you create your VPC, so think carefully about your address requirements before creating a VPC.

## Subnets
A subnet is a logical abstraction over aws resources like: ec2..etc that fall under the same network configurations.
So basically it's like a vlan, where each entity in same vlan has same network accessability, and other policies. Very frequent
use case for subnets is that in your vpc and in your system you'll have some kind of resources that you want to be accessible from the internet
like web servers and other resources that you want to be private and only limited and strongly provisioned resources can access this private ones, like databases let's say.
In these cases we'd have 2 different subnets, 1 public ( connected to internet via internet gateway ) and 1 private with strong and strict network configurations. 
