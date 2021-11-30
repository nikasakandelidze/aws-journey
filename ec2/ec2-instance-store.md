# EC2 instance store volume
Ec2 instance store volume is a temporary storage drive that is directly attached to host computer where ec2
instance is running and is removed as soon as  ec2 instance is removed.
These instance store volumes are backed by ephemeral volumes that are present from ephemeral[0-23] on the host computer.   

Buffer, caches, and other temporary content are good to store into instance store volume. 
You can't attach instance store volume to another instance like ebs.

Data in instance store is lost if next condition appear:
- Disk drive fails
- The instance stops
- The instnace hibernates
- The instance terminates

## Adding instance store volume to ec2
You must choose ec2 instance stored volume depending on ec2 type.
You can't make an instance store volume available after you launch the instance.

