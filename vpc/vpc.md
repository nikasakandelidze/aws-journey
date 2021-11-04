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

## Availability Zones
line we said above that each VPC must be only in single Region, each subnet must me in one availability zone. As you remember availability zones
are physically decoupled data centers in one region. Decoupled in a way that outage in one datacenter doesn't effect the second one. So to be maximally
safe if you want to have several ec2 instances we must create several subnets in several different availability zones and deploy instances of ec2 there.

## Elastic network interface
Elastic network interface is cirtual network interface immitating physical network interfce for ec2 critual machine.
Every ec2 instance must have primary ENI, this is exactly the feature that allows users to ssh into remote instance. 
Every ENI must be assigned to exactly one subnet, this is exactly why you can't start ec2 instance without a subnet. since ec2 instance must have
a network interface to opearte with and in aws framework network interface must be assigned to some concrete subnet.

User can't later change primary ENI that he initialized ec2 instnce with. This instance's ENI must have ip address form the range
of concrete subnet that it's attached to. And this will be ec2-s default primary ip address. Of course user can also attacj seconday ENI-s to ec2 instance
so this way ec2 instance might have several ip addresses. These several ENI-s can be assigned to different subnets, so that one machine can be in several subnets with
different eni-s located in different subnets but all these subnets must be in the same availability zone.

## Lifecycle of Elastic network interfaces
ENI-s lifecycle can be wider than that of ec2 instance's. ENI can be created and presetn without any ec2 instances, by itself. and basically can be attached
to some concrete ec2 instance after it's created.

## Interesting
Basically network packets that we think that we send to ec2 instances are actually transfered and sent to Elastic network interfaces located/attached to that ec2 instance.
So actually in case our ec2 instance dies and we have an ENI created with independent lifecycle,  we can simply  re attach this network interface to a new replicated ec2 instnace and if we do
this fast enough no user will understand that actual original machine broke down.  ( OF course if our app serving on ec2 instance is stateless )
