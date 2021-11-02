## aws glacier
AWS glacier service is a storage service just like S3 is, most of the features are the same( they both store and retrieve data ) but the main
differnece here lies in the mechanics and use cases of these features.
Glacier is created to store long term needed, infrequently accessed and large amounts of data and all of these in an inexpensive way.
If we have huuge data in S3 and we know that access rate for this data is low, we should move it to glacier since costs will decrease a lot.
Glacier has new termines from s3: vault: same as bucket, archive: same as object. So there are archives stored in vaults of aws glacier.

## variants and prices 
Glacier at the moment has two different types: Standard and Deep archive, as from the context created above or by name you
might guess, deep archive is more cost friendly alternative but the downside is that it will take from 12 to 48 hours to retrieve data store there.
So while choosing glacier types in our systems we should carefuly inspect our usecases and try to minimize costy wherever possible.
approximate costs are: storing 1 terabyte of data in glacier standard for 1 month costs: 4$ and in deep archive: 1$
