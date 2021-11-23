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
- Domain registrar: Company accredited by ICANN to process domain registrations for TLD servers.
- Domain registry: a company who can sell tld domain names, like go daddy?
- Name servers: servers in dns system that themselves translate and store ip <--> domain name mapping themselves.

## Basic diagram of route 53 
![diagram](./diagram.png)

As we see from the diagram, all the main heavy lifting job is done by a DNS resolver server, which is provided mainly by ISP-s
