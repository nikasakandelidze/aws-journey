# Here are some more advanced topics of ec2
## Instnace Templates
AWS allows users to create an ec2 instance-s template from scratch or from already running ec2 instance. What this template allows you to do is
to recreate instance state ( configurations, os, volume configs, network configs ) in an instant and to replicate this behaviour in as many instances as needed.

## Auto scalling
Auto scalling is AWS-s ec2 service-s feature where templates from above topic are used very intensively. Autoscalling is a mechanism using which
new ec2 instnaces, based on some preconfigured templates, can be spawned automatically and even load balanced ( with just simple configuration from UI or cli ).
User can specify desired, min and max number of ec2 instances active and depending on traffic and load auto scalling group will be managed automatically, also
custom logic alarms can be set to trigger auto scalling mechanism of ec2. Using this service of aws you can be sure that your cluster of machines running some
business logic will be safe and ok on every kind of situation and workloads. 
Scalling policies can be on cpu. network, some custom metrics or even simply scheduled ( since some businesses might know their customers usage patterns better )

## AWS systems manager
AWS systems manager provides an ability to user to automate some scripting/maintanence and provisioning steps for ec2 instances. things like upading packages,
patching installed os, creating new AMI-s after some specific logic condition gets invoked, disabling public access to different resources ( like s3 and etc ).
Systems manager provides 2 mechanisms for automations:
	- actions
	- insights
1) Actions Let you automate some logical actions against your AWS resources. There actions must be defined inside of documents.
There are 3 types of actions in aws ssm:
	- automation - action for different aws resources ( like restarting or running new ec2 instances )
	- command - actions against ec2 instnaces, commands for which to execute in other cases you would need to log in with according privileges.
	- policy - defined processes to collect data from instnaces
2) Insights - are mechanisms that collect, aggregate and monitor health and other types of data for your active, running resources in aws.
