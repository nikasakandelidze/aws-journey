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

## Internet gateway
An Internet gateway serves two purposes: to provide a target in your VPC route tables for Internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

By default aws VPC and all resources located in it are isolated from public internet, in most cases any system we build we dwant some part of it to be accessible from public internet.
Internet gateway is the exact service that enables specific subnets in vpc to become public, and this means that all services/entities located in this specific usbnet also become 
public. We must create Internet gateway manually and associate it with some subnet of vpc. You can associate only one IG to one vpc.

By making some parts public using IG, aws associates public ip addresses to your resources ( let's say ec2 instances ) so this way your ec2 instance has at least 2 ip addresses
public ( from internet gateway ) and private

## Route tables
A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed.
When you create a VPC, AWS automatically creates a default route table called the main route table and associates it with every subnet in that VPC. You can use the main route table or create a custom one that you can manually associate with one or more subnets.

A subnet cannot exist without a route table association. If you do not explicitly associate a subnet with a custom route table you’ve created, AWS will implicitly associate it with the main route table.

Route table is like a real router in your peronal/home network which has many subnets and which you can configure for specifi IO packets; 

## Security groups
Security groups are also entities for securing ec2 instances network by configuring them accordingly. Unlike routing tables security groups are more local
to ec2 instances,  and more concretely to ec2-s elastic network interface. Each ENI must have according security group associated with it. Since most of the time ec2 instances
have only one ENI people assume that security groups are assigned to ec2 instances but actually if ec2 instance has multiple ENI-s attached ( which is pretty normal case ) than several security groupsmust be specified for all these unique ENI-s.
Security groups are like firewalls for ec2 instances.

## Network Access Control List
NACL is firewall like machanism like security groups, but security group is attached specifically to ENI-s of ec2 instances and NACL-s are for whole subnets.
Inbound and Outbound rules need to be configured too for NACL-s. The main usecase difference between NACL-s and Security Groups is that if you want to configure
communication in a subnet between several ec2 instances you can't do this task using NACL since it's subnet level configuration mechanism ( meaning that it can
configure comunication tasks between subnets ) but security groups can easily solve problems like these since they are instance level ( more like ENI-s level ) configuration
mechanisms 

One subnet can have only one NACL. By default in VPC there is one NACL created which is associated automatically with subnets.
Unlike a security group, which is stateful, an NACL is stateless, meaning that it doesn’t use connection tracking and doesn’t automatically allow reply traffic. This is much like an access control list (ACL) on a traditional switch or router. The stateless nature of the NACL is why each one is preconfigured with rules to allow all inbound and outbound traffic, as discussed in the following sections

## NAT
NAT is a mechanism which is used for isolating network entities and leaving them secure. Network Address Translation is a mechanism that lays between client and network and
transforms from/to ip addresses according to rules. Best usecase for NAT gateway in AWS vpc is for the case with image below.

Case study:
	Let's say we have an application with front-end and back-end. and we want to deploy it in AWS. We can create a vpc ( ofcourse with all security groups and
NACL-s in it), create 2 subnets: 1) PrivateSubnet 2) PublicSubnet. The difference between public and private subnets is that resources within public subnet will be
accessible from the internet and no resources within private subnet can be accessed in that way. We'll have client side app ( maybe react, angular, vue ), server-side app: ( Java, nodejs, Python..),
 and database ( PostgreSQL, MySQL... ). Of course since databases are always secure intensive we'll put it in private subnet so noone from internet will even have a chance to directly conenct to it 
without specific permissions. we'll put our backend app and front-end app(on web server) in the public subnet.
Since we'll need to serve our client-side app to actual client's browsers and since these clinet side app will need to communicate to our backend API fron the internet. thisbackend API will have
 specific configurations so that it will be able to communicate with database being in private subnet ( for this to happen we'll need specific
security
 group configurations for inbound and outbound rules). We'll also need to install, patch and update programs on the private subnet's instances. for this to happen securely so that only resources located in private subnet can connect to internet but not vice versa, we create NAT gateway in public subnet,
 and direct all outbound traffic from private subnet to NAT gateway and tell NAT gateway to
direct traffic to internet gateway. By specifying only these mechanisms and not inbound ones NAT will securely communicate with internet and provide all needed services to private subnet.   
[diagram](./diagram.png)
