# Here we discuss two common ways of connecting to VPC from on premise networks. VPN and DirectConnect
This file mainly talks about hybrid clouds, where on premises datacenters also need to talk to AWS cloud in a reliable manner.

## Direct Connect
Direct connect is using aws-s dedicated networks for connecting from your on premise network to AWS services. 
For this to work you need to be in a specific location whwere aws has their centers where you can put your servers in rack. So basically
direct connect uses direct physical link to aws network.
This mechanism uses direct optical fiber connection to connect your datacenter with AWS direct connect location. Because of this this mechanism
is very fast ( 1 - 10 Gbps)

#### How it works
From your datacenter you connect to direct connect location and aws direct connection location itself manages connection via backbone network to AWS cloud.

You might want a highly available connection to aws cloud from a private network. In this case instead of using one direct conenct location you can use 2 separate
ones and have failover mechanism ready.

#### Cons
- reduced network costs
- very fast
- more consistent than vpn mechanism since it doesn't use public internet to route traffic.


## VPN
it uses private ipsec tunnel to conenct to AWS cloud but over the public internet so the performace is not guaranteed
