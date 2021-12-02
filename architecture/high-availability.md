# High availability and resiliency.

Reliability, also called resilliceny denotes an ability of system to tolerate failures and in case of human, programmatic, infrastrucutural
error get back to the working state as quickly as possible, so that end users of the system won't notice this error at all.
In simple words we always need to build highly available system in cloud environments, since modern day requirements don't tolerate failures.

After you decide how available you want your application to be for end users you should start thinking about parts of the systems you are going to use.
since even AWS services don't provide 100% up time, and you'll definetly need to prepare for mechanisms to avoid services shutdown or even total availability zones shutdown.
Here we'll discuss both how to be ready for these kinds of failures so that we design fault tolerant systems, and also how to recover quickly from these kinds of errors ( high availabilty).

## Availability
Availability is a quantity usually measured in percentages which denote how much time during the year your service works as expected. Usual amounts are > 99.00%
So it's conventions to just count nines after whole part of the 99. ( 99.999% is called 3 nines and etc.).

Availability percentate |  Time unavaiable during the year
   99%                    3 days, 15 hours, 19 minutes
   99.9%                  8 hours, 45 minutes
   99.95%                 4 hours, 22 minutes
   99.999%                5 minutes

## Availability difference in traditional vs cloud native application
Mainly there are 2 types of applications. Traditional and cloud native applications.

#### Traditional applpications
are more like monolithic applications, which mainly can't benefit from all the features that modern cloud infrastructures provide.
These kind of applications are stateful ( so that we can't spawn new instances for horizontal scaling ). Main flag that application is more like
a traditional one than cloud native is that if you can use your app on basic servers and on cloud in the same way without having much benefits than it is a traditional type 
of app.

Case study: let's say we have ec2 instance in one AZ running traditional app and it is backed by multi AZ AWS RDS. Whole system availability depends on availability of both: ec2 and rds.
Both of these are mainly called hard dependencies. Total availability will be: availability(ec2) * availability(rds) == .9 * .9995 == 89.955% whcih is 36 days off during a year which
is not a totally good result. For this result to increase we can create multiple ec2 instances and with load balancer balance between them. Total availabilty for e2 instance now increases
100% – 10% 10% 10% 99.9% this is about 9 hours of down time per year. We must also consider load balancers and rds-s availabilities and multiply them to get availaibility of the whole system. result is 99.84 percent which is 14 hours of downtime a year.  We can further increase by adding second databse or more ec2 instances. 


#### Cloud native applications
Cloud native apps are written to use cloud-s specific tools and benefit from them drastically. They can be using aws lambda or simply ec2, s3 dynamo db and etc.

Case study: let's say we have 3 ec2 instances running in one AZ and also have DynamoDb which has single region availability of 99.99 percent. Three ec2-s have 99.9 availability.
This system will have availability of 99.79 percent. which is 18 hours of downtime a year. We can achieve even greater result if we add more ec2 instances all in different
availability zones ( 6 ec2 instances in 6 AZ-s ). This way we'll have a result of 2hours of downtime per year. We can even make this better if we use several regions with this
system and balance through them using route53 weighted routing policy. this way we'll reduce downtime to 5 minutes per year. ( route53-s downtime is 0 )

 
