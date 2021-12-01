# EC2 Elastic Block Store
Elastic block storage is a durable persistent volume. This is the type of storage you should use for mission important data.
Several properties of EBS:
- EBS is durable which means that data is persisted even if you terminate the instance.
- EBS is flexible, which means that you can modify size, IOps and other props during the livep roduction use of ebs.
- You can choose type of ssd or either hdd
- One instance can have multiple EBS-es but one EBS can only be attached to one concrete ec2.
- EBS and ec2 that we want to attch it to must be in the same availability zone.

## High availability
AWS replicated the volume within the same AZ for high availability.

## Life-cycle
Data persists independently from the lifetime of instance until the volume is deleted explicitly. 
Detached volume can be re attached to a new ec2 instnace.
We can restart, and stopped ec2 with EBS without worrying about loosing data in ebs.

## Security
We can encrypt data in ebs volume for security.

## Snapshots
data in ebs volumes can be backedup using snapshots, these snapshots are stored in s3
Data can be backed up dynamically even when volume is attached to runnign instnace.
Volumes restored from encrypted snapshots are automatically encrypted.

Snapshot is constrained to a region where it was created.
Snapshot can be coppied in different regions.

## Types of volumes for ebs
- general purpose (gp2 and gp3 ). balanced power and price.
- io1 and io2, with more IOPS workload.
- st1, HDD which is slower but has low cost big data stroing capability.
