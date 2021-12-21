# Elastic Container Service
ECS is aws-s container cluster management service. to stop, restart, pull up/down containers according to some predefined conditions ( it's just like kubernetes but from Amazon ).
It is an interesting problem to solve how to manage containers correctly, how do you know that you have enough resources on available VM-s to run new container there or you need to pull up a new VM for it?
ECS helps us answer these quesiton easily.

AWS Fargate is basically an alternative to using ec2 instnaces with ECS clusters. As you understand in this case you have to controll and manage host instances manually. If you want to avoid
managing and provisioning ec2 instnaces manually you can use aws fargate which takes care of both: container cluster managemenet and host instance provisioning.
It is a serverless way of running a container.   
