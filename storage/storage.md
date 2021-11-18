#AWS Storage/ Database services
AWS provides several well known services for database storage.

## RDS ( Relational Database Service ) 
RDS is an abstraction over the implementation of the specific SQL databases. RDS supports Mysql, Postgresql, OracleSql and etc.

## Licensing considerations
RDS supports 2 ways of usage:
 1) using builtin provided licenses for databases(these for mysql, postgres are free since they are open source)
 2) using your own license for database

## Database instance types
Standart: mostly this class of rds instance will be used. 
Memory optimized: Providing more memory to a database allows it to store more data in memory, which can result in faster query times.
Burstable performance: Burstable performance instances are for development, test, and other nonproduction databases. 
The latest burstable performance instance class available is db.t3

## EC2 hosted database or RDS?
One of the most important and interesting questions raise up when we understand that we can store application's persistent data using RDS but also
we can create a custom ec2 instance and ourselves manage database program there, or have database running on the same ec2 instance as ourt main program ( maybe web server )	

- Running database program on the same ec2 instance as main program like webserver: Pros: 1) Easy to set up 2)for low end/low load applications it will be cost effective.
Cons: 1) Not scalable, since you have database program on 1 machine it's hard to later scale it if load is high 2) security problem, since we have our web servers in public 
subnet its accessible from internet along with anything located in this public subnet. Storing mission critical data in public subnet where its exposd to the internet directly is
not a good idea from security side of view. 3) If ec2 machine dies, both database and webserver go with it and this is bad, we want entities to be decoupled and not be dependant
on each other's life cycles.

- Running database program on a separate ec2 instance from main ec2 of the system: Pros: 1)Maximum configuration capabilities, 2)You'll be able to have your db admins and make
them configure it in accordance to your wishes.3)Cost effective compared to RDS  Cons: 1) More work to configure 2) Admin will need to manually configure failover clusters and manage them. 3) Admin will
need to manually configure replication of the data so that if one node dies or gets corrupted no data is lost.

- Running RDS as your storage: Pros: 1)Ready of the shelf. 2)Many configuration capabilities like: replication, failover, clustering just by clicking a button. 3) No need for custom
configuration, updates, patches and provisioning of databse system, it all happens on AWS service side. Cons: 1) A bit costly if not used correctly.
