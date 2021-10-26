## Legal Part of AWS
AWS has a shared responsibility model when it comes to legal part of cloud infrastructure.
AWS provides it's clients with guarantees, these guarantees only cover underlying AWS platform and nothing more.
So basically sayng AWS guarantees that it's cloud infrastracture ( servers, load balancers and etc ) will work without
problems all the time but user of the cloud, for example your own business, must take care of all inner implementation details
security, correct authentication, data flow and etc.
Next grapth illustrates upper sentence:
    User is responsible for:
	Customer's data
	Access management
	OS, Network, Security
	Data encryption 

    AWS is responsible for:
	Hardware and Network maintance
	AWS global infrastructure
	Managed services

By “guarantee,” AWS doesn’t mean that service disruptions or security breaches will never occur.
 Drives may stop spinning, major electricity systems may fail, and natural disasters may happen.
 But when something does go wrong, AWS will provide service credits to reim- burse customers for
 their direct losses whenever uptimes fall below a defined threshold. Of course, that won’t help you recover customer confidence or lost business.
The exact percentage of the guarantee will differ according to service. The service level agreement (SLA) rate for
 AWS EC2, for instance, is set to 99.99 percent—meaning that you can expect your EC2 instances, ECS containers, 
and EBS storage devices to be available for all but around four minutes of each month.
The important thing to remember is that it’s not if things will fail but when. Build your applications to be geographically dispersed and 
fault tolerant so that when things do break, your users will barely notice
