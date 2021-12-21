# Elastic Container Service
In the modern software world container are pretty common. In microservices world every app on every VM runs in a container, for sevearl container managing them manually is not a big problem.
But for big number of containers it becomes a pain in the neck.
ECS is aws-s container cluster management service. to stop, restart, pull up/down containers according to some predefined conditions ( it's just like kubernetes but from Amazon ).
It is an interesting problem to solve how to manage containers correctly, how do you know that you have enough resources on available VM-s to run new container there or you need to pull up a new VM for it?
ECS helps us answer these quesiton easily.

## AWS Fargate
AWS Fargate is a service to be able to run container using ECS without having to manage ec2 instances in the cluster.
AWS Fargate is basically an alternative to using ec2 instnaces with ECS clusters. As you understand in this case you have to controll and manage host instances manually. If you want to avoid
managing and provisioning ec2 instnaces manually you can use aws fargate which takes care of both: container cluster managemenet and host instance provisioning.
It is a serverless way of running a container.   

## Task definitions
Task definitions are configurations in json format for running Docker containers in ECS clusters.
Some of the most convinient properties to specify there are:
- The Docker image to use with each container in your task
- How much CPU and memory to use with each task or each container within a task
- The launch type to use, which determines the infrastructure on which your tasks are hosted
- The Docker networking mode to use for the containers in your task
- The logging configuration to use for your tasks
and etc. 

## Architecture
As we already said there are 2 types of ECS usage types:
- Fargate launch type: serverless pay as you go option, without infrastructure management.
- EC2 launch type: configure and run containers on ec2 instances

#### Fargate launch type
Most usecases for fargate launch type:
- Large workloads that need to be optimized for low overhead
- Small workloads that have occasional burst
- Batch workloads
- Tiny workloads
Main question is whether you should use one task definition for multiple contianer or use separate tasks for each of them.
Main pattern here is: 
- If containers' lifecycles are hardly coupled use one task definition.
- If your container !must! run on the same machine ( like if one containers service is referencing another container using localhost )
- You want containers to share resources.
- Your containers share data volumes.
Otherwise you must deploy them in a separate task definitions.

#### EC2 launch type
This type is for good performance/price optimization.
You should always group containers that are used for one and the same purpose.
