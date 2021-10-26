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

