# Catalogue of services with small descriptions

## Compute Services
### Elastic Compute 2
EC2 instances are same kind of virtualized servers that one might have in their own
data-centers. The best part is that one can configure resources like: RAM, CPU, network...etc
for EC2 instance according to there needsi.
### Lambda
Lambda is a service provided by AWS using which you dont need to provision and monitor
servers that are 24/7 on. AWS Lambda infrstructure has automated scaling and provisioning
, you as a user only have to specify code/function that needs to be executed accordingly and
AWS Lambda will make sure that this peace of code executes on some events ( like network calls
and etc ). After code execution is over, Lambda automatically frees all resources used for code execution so
resources get preserved and cost efficient very well. Since resources are concereved billing is also better.
### Auto Scaling
Copes of EC2 instances ( with it's configurations ) can be saved as machine image templates. Later thit
template can be used by auto scaling service to autmoatically launch new instances of the machine during the
high load on the system and then automatically scale down to reserve costs.
### Elastic Load Balancing
Load balancer service ( functionality is the same as of application level load balancers: nginx, haproxy...etc ). If we a
horizontal scalability of our application we might have several instances of our app running on several EC2 machines and
we want for all of them to stress equaly. Load balancer will balance the load between these application servers with different
algorithms like RR( round robin )..etc. 
### Elastic Bean Stalk
Elastic bean stalk is an automatic service of AWS where you just upload your code and all infrastructure configurations
are automated for you by AWS. All things: security, network, EC2 runnning, autoscaling is auto managed.
Basically value of beanstalk is that developer only needs to be concerned about writing working application and
all other concerns are takeb by AWS instead of him.

## Networking Service
### VPC ( Virutal Private Cloud )
Virtual Private Cloud is a service which allows user to have fully isolated and controlled private network, where user can
launch all the services like EC2, load balancers and etc. After launching them user should himself/herself specify communication
mechanisms/paths/routes for VPC comunicating to outer world. For this user will have to configure different subnets of VPC ( since
different parts might have different conventions/topologies of network and security). For example web service might be in a public 
subnet and database server in private subnet since no one should have direct access to database part from outer world. for public subnet
another service called public internet gateway will be used to direct all the traffic from and to public subnet to outer world.
### Route 53
Route 53 is DNS service from AWS, which makes possible for developers to setup different records in AWS-s DNS servers. record type might be:
A: url to ipv4, AAAA: url to ipv6, cname: url to url, alias: url to aws resource. Router 53 also has an ability to setup system health checks for
systems that you design in AWS infrastructure. 
### Cloud Front
Cloud Front is AWS-s CDN ( Content Delivery Network ). 
