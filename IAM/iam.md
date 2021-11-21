# IAM ( Identity and Access Management )



## AWS roles
AWS roles have many usecases and they are simillar to actual user entities of aws IAM. One of the most important and interesting usecases is if
we want our specific service to access and talk to some other resource/service in aws. Best example is when we write an app that we run on ec2 instance and which needs to access
s3 bucket's resource. One of the most basic solutions for this problem that comes to mind is to have s3 publicly available and also have ec2 instance either in public subnet or
have it in a private subnet and using NAT in public subnet communicate via internet gateway to public internet resources. But let's all agree that this case is greately
simplified and there can be most usecases where we want program on private ec2 instance to communicate with other aws resource like s3.
For this last specific case the solution is to create IAM roles which will have security policies specialized to their needs ( like onlyAccessReadS3, or ReadAndWriteAccessS3 and etc. ).
After creating this role from IAM dashboard from console or via CLI we then associate already running ec2 instance from ec2 instance dashboard menu with this newly created IAM role ( from 
security configuration ). After this process, ec2 instance and all the programs running there will have explicit permission to access other AWS resources ( in this specific case s3 bucket ) 

## Idea
The main idea before mechanism of roles for accessing different aws services ( like ec --> s3 ) is that all requests, no matter from inside of vpc or outside of vpc to AWS services must
be cryptograhpically signed. ( Like if you want to write an app, like aws s3 wrapper, which using http requests of get and post to your app endpoints modifies s3 bucket. For this to work on
local or any machine your app has to use acces key on your local machine, which by default is located in your systems folder hirearchy if you have used aws cli even once). Just since it's not awlays
safe and easy to use mechanism to have access key permanent on your machine roles ( maybe profiels ) ease this process of granting temporary keys by which app can acces aws services and which will
automatically time out and they won't be persisted in storage on some machine which can be hacked. 

### Profiles
On a code  and implementaiton level it's interesting how to manage and get all the security/role config. necessary to access role assumed aws services.

## Diagram of using roles from ec2 to s3
![ec2->s3](./diagram.png)
