# VPC security using Security Groups and NACL
Resources in VPC need to be secured. Since they compose of networking primitives inbound and outbound traffic for all the systems
will need to be configured. 
VPC has 2 important security primitivies: SecurityGroups and Network Address Control List they kinda do the same thing, which is
imitating Firewall for some system upfront but they operate at different levels.

## NACL
NACL-s operate at subnet level, they are virtual firewalls for subnets( each subnet they are associated with ). In AWS NACL has
table using which user can configure very specifically according to their needs. 
NACL is stateless, which means that response for sent request from some VPC resource like ec2 instance needs to be explicitly allowed, and nacl doesn't
save state of to which request does this specific response correspond to and to enable it or not according to that.

## Security Group
Security groups are ec2 instance level, more like Elastic network interface level entities for security ( there interfaces are connected to ec2 instances ). 
Security groups are stateful, which means that responses to sent request are allowed automatically disregarding fact that these responses might have been explicitly
denied in security group tables.
You can specify up to 5 security groups to ec2 instance.

If you don't specify ec2-s security group explicitly it will attach itself to default(main) security group 
By default newly created security group doesn't allow any inbound trafiic but allow outbound traffic.

## Differences between Security groups and NACL
Abstraction Levels:
- Security groups operate at instance level, which means that if you want custom rules between communications of ec2 instances, you will need to use secuirty groups
Securty groups allow or deny traffic that NACL allowed in a subnet.
- NACL-s operate at subnet level, which means that its firewall for a whole subnet, and its traffic. 
NACL-s allow or deny traffic before secuirty groups. So traffic/packets to reach to security groups it must first go through NACL-s.

Internet----->IGW----->NACL------->Security Group ---> ENI ---> EC2

Processing type
- Security groups process rules via groups
- NACL process rules one at a time, from lowest number to highest. First applied rule overrides later applied rule to same contextual configuration.

Deny/Allow rules
- Security groups are deny by default and only allow allow rules to be specified.
	By default Security groups deny all inbound rules and allow all outbound rules.
- NACL allow both allow and deny rules.
	By default NACL-s deny all inbound and outbound rules.
