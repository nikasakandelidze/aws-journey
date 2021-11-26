# Ec2 finance models, purchasing options and etc.
There are multiple purchasing and use plans for ec2 instances. We'll review all of them in this document.

## EC2 on demand instances
Most expensive and most widely used one.
- Pay for compute capacity used by second, without a long-term commitment
- Able to stop/terminate instance at any time
- Full control over instance lifecycle ( strat, stop, hibernate, terminate )
- Price is fixed for every second ec2 instance is in a running state.
-  Good for short term workloads that can not /must not be interrupted.


## EC2 savings plan
Flexible model to save money spent on ec2
zs:1: command not found: claer
aws offers some discounts.
There are two kinds of saving plangs:
- Compute savings plan: commit to just $/hour and reduce costs up to 66 percents. During this plan
ec2 instance type and region doesn't matter, you just need to commit to compute to hour.
- EC2 instance saving plans: reduces cost up to 72 percent, but in this case you must commit to 
some famility type of ec2 instance and region in which it's deployed. ( let's say m5 in us-east-1 ). 

## EC2 reserved instances
Reserced instances is not a physical instnace. they are simply a billing discount applied to on demand pricing of ec2.
On demand instances must match some attributes. such as instnace type and region of deployment.
Variables that detemine reserved instnace pricing:
- instance attributes: instnace type, region, OS
- Term commitment: one-year or three years
- Payment options: all upfront, partial upfront, no upfront
- Offering class: standard, convertible.
