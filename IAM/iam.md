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

### Profiles
On a code  and implementaiton level it's interesting how to manage and get all the security/role config. necessary to access role assumed aws services.

## Diagram of using roles from ec2 to s3
![ec2->s3](./diagram.png)
