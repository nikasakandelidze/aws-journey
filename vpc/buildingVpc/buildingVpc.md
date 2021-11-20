# In this document we'll discuss how to build VPC-s from scratch and not using vpc wizards.
Usually since common patterns of VPC-s are well known AWS allows users to create VPC-s with preconfigured mechanisms like: subnets, route tables, NACL-s, security groups
and etc. But it is also very important to  be able to create VPC-s from scratch. 

## Steps
1) Create two standalone vpcs
2) Create public and private subnets in both vpc-s
3) Create and associate Internet gateway so that vpc-s have communication with public internet ( for sshing, for patching/updating etc )
4) Create private route tables and associate them with private subnets.
5) Create public and private ec2 instances in both VPC-s
6) Create Transit Gateway
7) Create attachments for both VPC-s in transit gateway.
8) Test transit gateway via ping command for ec2 instnaces using private ip addresses of public/private instnaces.

## Notice
If we want to have mechanism to have private and public subnets in vpc-s, and to make there two vpc-s public subnets talk to each other via
transit gateway and want to isolate private subnets and ec2 instances in them, we can easily configure private subnet's reoute table to only
support destination with same cidr as subnet ( or vpc-s cidr for same cidr as vpc ) and target to local, which means that only elements from within subnet/vpc
can talk to each other.
