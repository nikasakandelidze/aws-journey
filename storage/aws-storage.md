# AWS S3 Storage mechanism
## What is AWS s3
AWS S3 also known as simple storage service, is a service provided by Amazon for creating easy to use, high level abstraction for
stroing files and data ( all the different kinds of data stored abstarcted under object type, that's why it's called obejct storage )  in reliable and consistent manner. Best use cases for aws s3 are next:
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
When we write data into s3 alongside our actual data some metadata is also associated with it which has some security and access information in it storedi.

## Usecases
Generally AWS s3 can be an excellent alternative to all the cases where file system on propertary data center servers were used. Storing all the files retriecing them and etc.
In some cases S3 might be an even better alternative since it's data is reliable ( replicated ) and safe. and also has bunch of custom configuration possibilites for specializing
base mechanisms of s3 for: frequent reads, frequent writes and etc...

## S3 server architecture
The way user can create and later interact with s3 storage is by creating buckets.A bucket is a container for objects. An object is a file and any metadata that describes that file.
To store an object in Amazon S3, you create a bucket and then upload the object to the bucket. When the object is in the bucket, you can open it, download it, and move it.
With Amazon S3, you pay only for what you use.
User can have maximum 100 buckets for each aws account and as for all other services if yoour reach this limit you can ask aws support for custom increase of this limit ( smth like
custom plan ).
You can have aws specific s3 bucket only in a certain region, and one more interesting and must know fact is that the name for aws bucket you create must be globally unique in whole aws
s3 bucket names. ( There’s some logic to this; you’ll often want your data located in a particular geographical region to satisfy operational or regulatory needs.
But at the same time, being able to reference a bucket without having to specify its region simplifies the process. )
Each bucket-s url you create with your account will follow next pattern: s3.amazonaws.com/bucketname/filename

## Prefixes and Delimiters 
As you’ve seen, S3 stores objects within a bucket on a flat surface without subfolder hierar- chies. However, you can use prefixes and delimiters to give your buckets the appearance of a more structured organization.
A prefix is a common text string that indicates an organization level. For example, the word contracts when followed by the delimiter / would tell S3 to treat a file with a name like contracts/acme.pdf as an object that should be grouped together with a second file named contracts/dynamic.pdf.
S3 recognizes folder/directory structures as they’re uploaded and emulates their hierar- chical design within the bucket, automatically converting slashes to delimiters. That’s why you’ll see the correct folders whenever you view your S3-based objects through the console or the API.
