# AWS Route53 dns
Route53 is DNS service. AS you know internet is simply a interconnected nodes of many computers, when one machine wants to talk to another one it should get it's name, how to 
call him, just like in real life situation, you must know a persons name if you want to have a good chat with them.
Machines don't have names like humans do, but they have ip addresses 4 8byte expression from 0-255 that uniquely identify machines. Of course we are humans and we aint as good with
numbers as machines are, so we dont want to remember ip address of google.com lets say, so we create DNS-s servers specialized in translating IP addresses into names and vice versa.

## Route53 features
- Register domain names
- Route internet traffic for your domain
- Healthchecks of your service registered in domain registries

## Concepts in Route53
- Domain name: Human readable mapping to ip address.
- Top level domain server: servers that have records for routing .com, .org, .net and etc domain mappings.
- Subdomain: maps.google.com is subdomain fo google.com. Main host is same, main domain name is same but there is preappendend some more data.
- Domain registrar: Company accredited by ICANN to process domain registrations for TLD servers. for AWS it's AWS and Gandi.
- Domain registry: a company who can sell tld domain names, like go daddy?
- Name servers: servers in dns system that themselves translate and store ip <--> domain name mapping themselves.

## Whole process of using route53
- If you want to create a web application you must have a domain name for it. You must choose a unique/available domain name to register it in route53.
If the domain is already taken you can try changing the top level domain like .com to .org .ninja or etc.
- When you register a domain in route53 the service automatically makes itself the DNS service for the domain:
	- Creates a hosted zone that has the same name as your domain
	- Assings a set of 4 name servers, all located in unique stripes ( unique TLD-s )
	- ..
- At the end of registration AWS sends your info to Domain Rregistrat ( It's AWS itself or Gandi )
- Registrar sends your info to registry for the domain. A registry is a company that sells domain registration for one or more TLD-s such as .com.
- The registry stores the information about your domain in their own database and also stores some of the information in the public WHOIS database.

## Routing and records
Basically saying when you input domain name and create it and Route53 aoutmatically sets up dns service for you, this is the route that a traffic from anyone's machine
must travel to get to this newly created dns name servers. After reaching this point how traffic will continue to flow inside and to your AWS services or entities
is up to administrator of AWS account. All this inner routing mechanisms are implemented using different types of records that we must add into  route53 allocatted name servers.

If you open up hosted zones page, you will see there NS record with values of all name server records ( 4 values ) that hosted zone creates by default.
also there will be SOA record which is start of authority which has some metadata in it bout public hosted zone.


## Routing policies
- Simple routing policy: Use for a single resource that performs needed action, like web server from ec2 instance, or s3 for serving media files, or serving something from
behind of load balancer. For this policy you can't create several records with same naem and type. But you can create records with multiple values specified like 
multiple ip addresses, and they all will be returned in random order to originator of dns query. User can create Alias record for this policy, and with alias records
you can enjoy health checks. Also user can create non-Alias basic record, for some ip address of some resource/server, but for it you can't attach healthechk mechanism. 
- Weighted routing policy: weighted routing policy is just what is sounds like, you can create several records with same name and type and same/different 
weidhts associated with them. ( this wasn't possible in simple routing policy ). And fraction of weight to toal sum of weights percent of traffic will
be forwarded to speciific targets.    
- Latency policy: can create several A records with same name and different ip address values ( let's say for different ec2 instances in different regions ). Latency policy when getting a query will
automatically understand which ec2 instance is closer to the region of user who queried dns and will use that ip address. This determination of closer ec2 instance region is not taking place exactly at the moment
when dns query is recieved. It in the background process takes place, to have approximate idea about locations and latencies and when query is recieved the target is taken depending on these data collected by time.
- Geolocation routing policy: forward users to ip addresses of some reousrces ( let's say ec2 instances ) depending on their geo location, setup default record to cover case that user comes from the geolocation which
is not specified in any record.
- Failover routing policy: you can create two records with same name, in values you must place ip addresses of primary and secondary aws resources. Introduce healthcheck mechanism in route53 to primary resource. Once
that resource fails healthcheck will fail for that resource, which will tell route53 to provide further dns queries for this specific name with failover, secondary resource ip address.
- Multivalue answer policy: works like simple routing policy but main idea for this policy is to associate healthcheck with all resource ip addresses in this record's value and periodically check
which ones are healthy and only return healthy ones when dns query arrives. Note that if no health check is associated route53 assumes that for a record with this routing policy and no helathcheck resource is always healthy. 

## Hosted zones
There are private and public hosted zones, public obviously is for public DNS features, when you want for users from public internet to get to your servers let's say. Private is for internal VPC use. 
when you create your public hosted zones and you want to host it on route53 ( this autmoatically gets created when you create new domain name with correct config) route53 will automatically allocate 4 name servers to be responsible for your records. These are the 4 authoritative name servers that know data about
records you add. If you see TLD endings for these name servers you'll see that they are all for different TLD-s ( like .net, .com, .org ..etc )
They are called stripes and they are all independent. So when you want to create hosted zone for some domain some available name servers from these
stripes will be allocated to your needs.

## Common patterns
Let's say we have several ec2 instances of the same application, for high load purposes. Now we want to add DNS mechanism to our service. 
We have two ways to solve this problem:
1) Add elastic load balancer in front of two these ec2 instnaces ( by creating it and specifying as target of load balancer both instances ) and associate dns with
elastic load balancer using Alias record ind dns service route53
2) Directly add both of ec2 instance ip addresses as targets in dns record targets. This way when client asks for ip addresses from dns service, dns service will return
both addresses and client itself should decide which to contact ( maybe best strategy here will be to ping one till it's dead and only than automatically jump to next one )    

## SLA
Route53 guarantees 100 percent SLA, which means that all the queries sent to route53 will be answered all the time.

## Basic diagram of route 53 
![diagram](./diagram.png)

As we see from the diagram, all the main heavy lifting job is done by a DNS resolver server, which is provided mainly by ISP-s
