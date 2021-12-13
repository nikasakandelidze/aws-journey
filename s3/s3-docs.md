# Simple Storage Service
AWS s3 is an object storage service that offers scalable, highly avaiable store for any kind of data.

## Storage classes
- S3 Standard, general purpose - is used in most of the use cases, it offers high availability, durability, low latency for retrievals and etc.
This is the most widely used configuration class for s3. Offers nine 9-s SLA.
- AWS S3 Intelligent Tiering - storage class that automatically decides most useful and propper class of aws s3 storage and moves your data there.
Decision of moving data is always depnded on it being most cost effective, and all this ceremonial of updating storage class used is without any additional charges.
This mechanism with cost also looks at frequency of access and using these results decides whether to move them to lower freq. access tiers or move upwawrds.
- S3 standart Infrequent access - low cost ( by infrequest access ) and high speed of access whenever needed. This mechanism is also replicated and highlt available. 
- S3 one zone infrequent access - same as above but not highly avaiable, you can save this class which uses only 1 AZ, by compromising avaiablitiy you can save
funds. Of course this class should be used only if data stored there is not mission critical.
- S3 glacier classes are used for archiving data. Data which will be needed very very infrequently. Here are also types when glacier data whenever accessed
will need instant access or will not care about it and etc.

## Buckets and Objects
The abstractions that you work with in S3 storage are called buckets and objects. Relation between them is that you store as many objects you want in a bucket.
AWS s3 bucket name must be globally unique. You must specify a region that AWS s3 bucket will use upon creation.

#### Security of s3 buckets
All kind of access for s3 buckets are controlled over ACL-s, bucket policies or both. For ease of use aws s3 provides capability to block all public access to s3.
Public access blocking mechanism can override acl-s and policies. 
#### Bucket configurations
AWS allows you to configure tons of properties for s3 buckets manually like:
- CORS policy
- Event notifications
- lifecycle: rules that react to some lifecycle callback. 
- Versioning helps you recover accidental overwrites and deletes.We recommend versioning as a best practice to recover objects from being deleted or overwritten by mistake.

