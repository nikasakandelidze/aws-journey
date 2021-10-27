# Elastic Cloud Compute notes
## What is EC2
EC2 is a service provided by amazon that replicates data center servers experience as closely as possible.
The core of this service is an instance of EC2 which is currently active virtual machine on server ( which we can look at as simply server ).
EC2 may be a virtualized server but all the details and  abstractions created around it make it look
like a real server. You can decide what OS, resources and etc will be used on this instance of ec2.

## AMI ( Amazon Machine Image )
AMI is simply a file containing protocol of serializing and instantiating EC2 servers with custom predefined configurations.
Amazon Machine Image is to running EC2 instance, just like a Docker image is to Docker container and what class is to an object instance from this class.
So you can create AMI for some concrete configuration of EC2 and than you can replicate instances of EC2 using these images.
When you press launch new instance on AWS UI, the first window that appears after this is window for choosing EC2 AMI. Most of us usually choose
Amazn Linux 2 AMI(HVM), SS Volume Type since it's free tier eligable.

There are different types of AMI-s: private, community, Amazon Quick Start AMI-s, AWS marketplace AMI-s.

## EC2 Instance types
There are different types of instances you can configure EC2 to use. At the moment there are approximately 75 unique types.
Choosing a correct type for your EC2 instance will be tottaly dependenat on the problem you are trying to solve and the domain
of the problem.
### Basic classification of instance types
- R.., X... - Optimized memory/RAM, which work well with memory intensive, database, caching and data analysis operations. Some of them have
up to 4 terabytes of DRAM.
- C.... - Optimized for CPU/Computing intensive applications.  Maybe be used for high end web servers and machine learning problems
where big CPU cycles are needed.
- M, T... - General purpose, Balanced family of machines, they stand between R,X and C families, so they have both memory and CPU somewhere in the middle. not too much,
not too many.
- I.... - I/O intensive and optimized machines, where local IO is needed, used for storages ( since local IO-s are mostly used in this case )
- G.... - Graphics processing optimized machines, that might be used in heavy machine learning workloads or rendering.

Some instance types will have huge RAM amount and HUGE CPU cycles, some less and you should choose wisely between them.
There are several instance type families in aws:
- General purpose family consists of types that have uniformly distributed cpu, ram, storage and etc. So basically every other resource
in this family's instance types are in the middle.

## Settings up EC2
For succesfully and securely using EC2 instances there are 3 key points to configure:
- AWS Region, in which AWS region will your EC2 instance be published, Usually for production instances Region closest to your customers is a 
correct answer. While choosing a region also an important part is that if you are have some sensitive information in your system to deploy and want
this system to fall under some specific location's ( country's ) jurisdiction than choosing AWS glolbal region closest to this location is the best solution.
EC2 resources can only be managed when you are "located within" that specific region that instance in deployed in. You can update/change location easily from console and UI.
Bear in mind that the costs and even functionality of services and features might vary between regions. It’s always a good idea to consult the most up-to-date official documentation
- VPC ( Virtual Private Cloud ) is a isolated networking entity where you must deploy your EC2 instance for securing and many more benefits. VPC have nearlly all the networking details
configurable. One common pattern for many development teams is to have several different VPC-s each for different development stage-s. let's say VPC1 - dev env. VPC2 - stage env, VPC3 - production env. This way all the environments are totally isolated frome each other and can't ahrm each other, since on development environment teams might be testing and changing configurations in an 
unpredictable manner.
- Tenancy, while creating EC2 instance you have the ability to specify tenancy model for your virtual machine.  Tenancy model is all about on how isolated physical machines you want your
programs to be run. Default tenancy model is that your program will be run on the same server that some other aws customer's. ( of course they'll be totally isolated, just simply it's sometimes the case that we need our instnaces to be run on totally isolated servers, not sharing physical servers with anyone ). with tenancy model AWS also gives you ability to configure it. 
