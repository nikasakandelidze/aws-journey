# AWS S3 Storage mechanism
## What is AWS s3
AWS S3 also known as simple storage service, is a service provided by Amazon for creating easy to use, high level abstraction for
stroing files and data in reliable and consistent manner. Best use cases for aws s3 are next:
- Maintaining backup archives, log files, and disaster recovery images
- running analytics for data at rest
- static website hosting

## AWS s3 vs EBS ( block storage )
AWS s3 is a storage system, we shouldn't misinterpret it for EBS ( block storage service ) which is low level volume management system, where data
is always chuncked into blocks and file systems underneath handle persistnece of these blocks. These block storage mechanisms are bundled with
ec2 instances and are there for more database like use cases, where intensive writings take place.

On the other hand s3 service is more of a high level, easy to use mechanism for storing any kind of data from anywhere. Most use cases for s3 object storage
is for read heavy usecases ( where write once read many times situation arises ). Like: storing movies, images, documents and etc.
The simple design of s3-s api avoids some of the OS-related complications of block storage and allows anyone easy access to any amount of professionally
designed and maintained storage capacity.
When we write data into s3 alongside our actual data some metadata is also associated with it which has some security and access information in it stored.
