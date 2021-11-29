# Ec2 finance models, purchasing options and etc.
There are multiple purchasing and use plans for ec2 instances. We'll review all of them in this document.

## EC2 on demand instances
Most expensive and most widely used one.
- Pay for compute capacity used by second, without a long-term commitment
- Able to stop/terminate instance at any time
- Full control over instance lifecycle ( strat, stop, hibernate, terminate )
- Price is fixed for every second ec2 instance is in a running state.
-  Good for short term workloads that can not /must not be interrupted.
- If in stopped state you don't pay for ec2 istance but you will pay for ebs volume attached ( if you have ofc )


## EC2 savings plan
Flexible model to save money spent on ec2
aws offers some discounts.
There are two kinds of saving plangs:
- Compute savings plan: commit to just $/hour and reduce costs up to 66 percents. During this plan
ec2 instance type and region doesn't matter, you just need to commit to compute to hour.
- EC2 instance saving plans: reduces cost up to 72 percent, but in this case you must commit to 
some famility type of ec2 instance and region in which it's deployed. ( let's say m5 in us-east-1 ). 
- Ec2 instance saving plans are just like Reserved instances. They offer up to 66% doscount and same mechanism of commitment.
It automatically normalizes your commit plan to your compute usage.


## EC2 reserved instances
Reserced instances is not a physical instnace. they are simply a billing discount applied to on demand pricing of ec2.
On demand instances must match some attributes. such as instnace type and region of deployment.
Variables that detemine reserved instnace pricing:
- instance attributes: instnace type, region, OS
- Term commitment: one-year or three years
- Payment options: all upfront, partial upfront, no upfront
- Offering class: standard, convertible.
- If you purchase a Reserved Instance and you already have a running On-Demand Instance that matches the specifications of the Reserved Instance, the billing discount is applied immediately and automatically. You do not have to restart your instances. If you do not have an eligible running On-Demand Instance, launch an On-Demand Instance with the same specifications as your Reserved Instance
- If you reserve instance for t2.medium and then run 2 t2.small-s, then it will also be covered by reservation since small = large / 2.
and also if you run Xlarge then half of it will be covered by discount of reservation. This mechanism is called a reservation.
- Reserved Instances are automatically applied to running On-Demand Instances provided that the specifications match. If you have no running On-Demand Instances that match the specifications of your Reserved Instance, the Reserved Instance is unused until you launch an instance with the required specifications.



## Ec2 spot instances
Spot instnaces are like auctions for spare ec2 compute power, you are bidding actively to use compute power.
If you are running some stuff on bidded/won instance might terminate in case someone iverbids your last bid.
So basically using spots might benefit usecases where restarting the process is not a big deal.
AWs sends rebalance recommendation when your ec2 instance is about to temrinate

## Dedicated host
Physical server with ec2 capacity on it fully dedicated to you.
This is the way if you want to use your own licenses for some software.  
On dedicated host variant you can see number of cores on machine and number of sockets ( in other cases you can't access this info )
Dedicated host also allows you to consistently deploy ec2 instances to the same host ( in dedicated instance you can't do that ) 
Automatic instance recovery is supported for dedacted host and also for dedicated instnace.

## Ec2 capacity reservation
Reserve capacity in a region without entering several year term agreement.


## interesting
Ec2 can be in two subnets simultanisl by attaching two ENI-es to same ec2 and having those eni-s in different subnets.
