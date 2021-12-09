# Auto scaling
EC2 instance auto scaling mechanims in AWS assures you that at any point in time your application's scale is in accordance to
the traffic and load in that specific point in time.
What auto scalling lets users do is to update number of ec2 instances and the scale of the system dynamically without making any
straight ahead locked in decisions. This mechanism saves a lot of money and a lot of infrastructure provisioning overhead.  

In AWS Autoscalling groups you can specify min and max number of instances and depending on traffic number of ec2 instances will fluctuate
between these 2.

## Inner workings of Auto scalling
There are 2 main steps to make auto scalling up and working:
- Create a launch configuraiton. Select AMI, Add customization via User Data, Add Storage, apply security group.
- Create an autoscalling group, define group size, setup network and subnet, add load balancer. 

Scaling policies are mechanisms that decide to scale up or down current instances in instance autoscalling group
Very interesting and useful mechanisms are 1) manual, 2) shceduled, 3)on demand ( reacting to memory, network, cpu updates) scaling of auto scalling group 

You can have several policies wrapped up together among the auto scalling group.
