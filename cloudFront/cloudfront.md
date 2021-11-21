# AWS Cloudfront basics
Cloudfront is a mechanism in AWS which replicates mechanism of regional cache, which means that it sets up in predefined regions called edges ( aws datacenters ) cache mechanisms
which will cache data fetched by user, the data might be requested from s3, ec2 and other aws services. Let's say we have our server  deployed in US-east and customers from europe
request same video/image from our server many times a day. By default if users request content for N times, request for this content must go through whole network from one continent
to another one for fetching data N times, and this is also not a great result since data is traversing via public netwrok which might have very high load and even increase delay even more.

To solve this problem we can setup cloudfront location in europe where the data will be cached first time its requested from the server of US-east and all subseuquent requests for this
file will be handled from this cache from datacenter which will dramatically decrease time of serving users and will lead to better UX.

## Interesting details 
One of the most interesting points in Cloudfront caching mechanisms is that even the first request, when the actual first copy of the data requested must be fetched from original server
is much faster with cloudfront than it is with regular network, since on the first request user asks cloud front if there is cached data and if not, cloudfront, using aws-s  network will fetch data from s3,ec2 or whatever service was requested.  Since this first network call will also be using aws network and not public network ( which is not fully reliable ) the process will be much faster.
