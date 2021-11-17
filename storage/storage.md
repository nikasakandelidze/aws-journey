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

	
