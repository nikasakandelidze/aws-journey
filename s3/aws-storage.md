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

## S3 pricing
Price: Price of storage you use + price of additional fetch/update/upload for already stored files.

## Uploading large files
Uploading large files/objects into aws s3 might be problematic. There are several limitations placed by aws itself on this service, which are:
- single object might not be larger than 5tb ( tera bytes )
- individual uploads can't be larger than 5 gb-s
Even though these numbers of limitaitons are quite high there are some specific good to follow practices which specify that:
it's recommended to use mutli part upload when working with files/objects bigger than 100 mb-s. Multi part upload is specific mechanism/api implemented 
to help with working with big giles with s3 service.
main benefits for multi part upload is:
- Improved throughput - You can upload parts in parallel to improve throughput.
- Quick recovery from any network issues - Smaller part size minimizes the impact of restarting a failed upload due to a network error.
- pause and resume object uploads - You can upload object parts over time. After you initiate a multipart upload, there is no expiry;
  you must explicitly complete or stop the multipart upload
- Begin an upload before you know the final object size - You can upload an object as you are creating it.

## Protecting data on S3
Common practice is to secure data saved on s3, there are several mechanisms for doing it and all of them are using some kind of an encryption so that
no raw data lays in s3 buckets.
Main categories for s3 data securty are next:
- client side encryption - encrypting data before sending it to s3 object store to maximaize security. Good choice if data you are storing on s3 is very
sensitive and must stay safe. This way even if AWS employee looks directly into your s3 buckeet they won't make any sense from data there since it would be encrypted and no
decryption key would be known to them.
- server side envryption - send data to s3 store in a raw mannet/format and let s3 bucket itself manage encrypting data before it stores, and right before fetching data form
s3 objects decrypt them. So basically client level APi fro this kind of security stays same since all security steps happen on server side. Usually KMS ( key management service ) is used for this kind of tasks.

## Logging
By default logging information for aws s3 storage is off. You can turn this logging mechanism on and it will save all actions with speecified s3 buckets.
The main configuration options you must specify is which s3 bucket you want to configure/mintor/watch and where/in which s3 bucekt to save these logs. We shouldn't
always turn logging mechanisms on since it generated quite a lot of data and it won't be always optimal. S3 generated logs might have a slight delay before appearing in files
and they'll have usually next pieces of data:
	- The account and IP address of the requestor
	- The source bucket name
	- The action that was requested (GET, PUT, POST, DELETE, etc.)
	- The time the request was issued
	- The response status (including error code)

## Durability, Reliability and availability
### Durability
As aws states, s3 has 99.99999 percent reliability ( which means that there is very small chance for you to loose your data ). Good thing about data stored in s3 buckets is that they are automatically replicated within different availability zones in the same region. S3 buckets are replicated across availability zones within the same region by default, except the One Zone class. However, S3 supports cross-region replication (CRR), wherein S3 buckets are asynchronously copied to different regions.
### Availability
Your data stored on aws s3 storage will be up and available 99.99999 percent of the time during the whole year, which means during 1 year maximum 9 hours of
downtime might occur for s3 storage objects.

## Data consistency
Aws s3 has some specifics with data consistency. This topic basically arises, since s3 is under the hood distributed storage. S3 storage has 2 different
consistency models for 2 different use cases:
- Every PUT ( creating new object ) request is guaranteed to have "Strong read after write" consistency, Which means that if we request serach data right
after inserting it into datbase we will get updated data without any problems or inconsistencies of stale  data.
- Amazon S3 offers eventual consistency for overwrite PUTS and DELETES in all Regions. Updates to a single key are atomic. For example, if you PUT to an existing key, a subsequent read might return the old data or the updated data, but it never returns corrupted or partial data.

Eventual consistency: faster but has a chance of getting stale and out of date data.
Strong consistency: slower ( since nodes are blocked from reading until data updates to all nodes ) but always guarantee new data. 
