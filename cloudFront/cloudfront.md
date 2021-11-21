# AWS Cloudfront basics
Cloudfront is a mechanism in AWS which replicates mechanism of regional cache, which means that it sets up in predefined regions called edges ( aws datacenters ) cache mechanisms
which will cache data fetched by user, the data might be requested from s3, ec2 and other aws services. Let's say we have our server  deployed in US-east and customers from europe
request same video/image from our server many times a day. By default if users request content for N times, request for this content must go through whole network from one continent
to another one for fetching data N times, and this is also not a great result since data is traversing via public netwrok which might have very high load and even increase delay even more.

## Services/entities cloudFront can be applied to
- AWS S3
- Elastic load balancers ( web servers )
- AWS media channel package endpoint
- AWS mediaStore container endpoint

To solve this problem we can setup cloudfront location in europe where the data will be cached first time its requested from the server of US-east and all subseuquent requests for this
file will be handled from this cache from datacenter which will dramatically decrease time of serving users and will lead to better UX.

## Interesting details 
One of the most interesting points in Cloudfront caching mechanisms is that even the first request, when the actual first copy of the data requested must be fetched from original server
is much faster with cloudfront than it is with regular network, since on the first request user asks cloud front if there is cached data and if not, cloudfront, using aws-s  network will fetch data from s3,ec2 or whatever service was requested.  Since this first network call will also be using aws network and not public network ( which is not fully reliable ) the process will be much faster.

## Creating cloud front service
When creating cloud front service instnace on your account there are quite a few intersting properties to specify
- origin domain: name/identifier of a service you want your cloudfront service to link to ( which service's data you want to cache ).
- origin path: Optional property, specifically for s3 bucket, here you can specify some subdirectory of s3 and cloud front willalways forward traffic for 
fetching from that subfolder. Common practice with s3 is to have different subfolders in same s3 for different env-s. like production and development. 
and use cloudfront to use content from /production subfolder of s3. Since in deveopment mode cloudFront isnot needed.
- S3 bucket access: common pattern with s3 and cloudFront is to make s3 bucket non public and enable Origin access identity ( OAI ) which will only allow
cloud front to access data in s3 buckets. If we don't specify OAI then s3 must be made public.
For this mechanism to work you must create explicitly new Origin access identity or use already precreated one, associate it with cloudFront. When associating
this Origin access identity to cloudFront we also need to update S3 secutiy policies to only allow this OAI. CloudFront creation allows you to automatically
manage this creds. or you can manually do it later.
General mechanism for OAI is to restrict all unsecured/other way access to s3 but access through cloudfront url and cloudfront-s forwawrding mechanism.
- Custom headers: When creating cloudfront you can specify custom headers, which cloudfront will always put when forwarding request to origin service.
We might use this mechanism let's say to only grant read permissions from s3 to requests that have this specified header in them.

## Default cache behaviour configurationI
- Path pattern:
- Automatic Compression
- Viewer protocol policy: HTTP and HTTPS, HTTP -> HTTPS, HTTPs only
- Allowed HTTP method
- Restrict Viewer access
