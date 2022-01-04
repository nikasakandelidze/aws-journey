# AWS step functions
AWS step functions are mechanisms to orchestrate AWS lambda chained functions and other AWS services to create solutions
for mission critical applications. One of the most useful features here is that step functions have visual interface creator
which helps you build and visualize step function workflows.
AWS step function uses States language which is workflow as a code mechanism.

These step function workflows are basically state machines. You can make step functions run AWS lambda functions or controll other
AWS services and etc. 

## Workflow types/mechanisms
There are 2 types of workflows in step functions:
- Standard workflow: runs exactly once and can run for up to one year time. Good for long running tasks, auditable workflows as they show the execution history for debugging.  
- Express workflow: runs at least once and can run up to 5 minutes. Express workflow is excellent for short running, high event rate tasks such as streaming mechanism analyzing and emitting
	- Asynchronous: return confirmation that workflow was started but dont wait for it, client can periodically feetch cloudWatch logs of the service.  
	- Synchronous: wait synchronously for workflow to complete.

## Typical AWS Step function usecases
- Function orchestration: If you create a workflow like a chain of lambda functions. Output of one serves as the input of another function. You can visualize build and optimize
systems like this via AWS step functions. 
- Branching: Using a Choice state you can invoke next, predefined kind of lambda function depending on the output of the current one. 
- Error handling: With retry statements you can invoke lambda functions several times in casae of failures or unsuccessful requests. 
- Human in the loop: pause workflow before some task token is returned to the step function system.  
- Parallel processing: using this you can do parallel tasks like if a user uploads some video to your streaming system, you can encode this video into different
resolutions parallely. Or converting mass number of images into different formats and resolutions for thumbnails and etc. 
- Dynamic paralellism:

## States Language and common states
AWS step functions are written in Amazon states language. there are several predefined states specified in specification of this langauge.
For State machine structure JSON code structure: StartAt and States key values are mandatory all other ones are optionals.

Common states:
- Pass state: Passes input to output without performing any work. Pass states are useful when debugging. Optional parameters: Result, ResultPath, Paremters.
Example:
"No-op": {
  "Type": "Pass",
  "Result": {
    "x-datum": 0.381018,
    "y-datum": 622.2269926397355
  },
  "ResultPath": "$.coords",
  "Next": "End"
}

Input: 
{
  "georefOf": "Home"
}

Output:
{
  "georefOf": "Home",
  "coords": {
    "x-datum": 0.381018,
    "y-datum": 622.2269926397355
  }
}

- Task state: Unit of work performed by a state machine. Tasks are units of work like lambda function invocations or other aws service calls. Mandatory Parameters: Resource. Optional
parameters: Parameters, Result, ResultPath ...etc.
Example:
{

 "StartAt": "BATCH_JOB",
 "States": {
   "BATCH_JOB": {
     "Type": "Task",
     "Resource": "arn:aws:states:::batch:submitJob.sync",
     "Parameters": {  
       "JobDefinition": "preprocessing",
       "JobName": "PreprocessingBatchJob",
       "JobQueue": "SecondaryQueue",
       "Parameters.$": "$.batchjob.parameters",
       "RetryStrategy": {
          "attempts": 5
        }
     },
     "End": true
    }
  }
}


- Choice state: adds branching logic to a state machine. Required parameter: Choices array ( where it is specified to which choice to jump next )
In each choice there must be a logical condition of checking some value and also Next state specified where to move in case of truth conditional.
Example:

"ChoiceStateX": {
  "Type": "Choice",
  "Choices": [
    {
      "Not": {
        "Variable": "$.type",
        "StringEquals": "Private"
      },
      "Next": "Public"
    },
    {
      "Variable": "$.value",
      "NumericEquals": 0,
      "Next": "ValueIsZero"
    },
    {
      "And": [
        {
          "Variable": "$.value",
          "NumericGreaterThanEquals": 20
        },
        {
          "Variable": "$.value",
          "NumericLessThan": 30
        }
      ],
      "Next": "ValueInTwenties"
    }
  ],
  "Default": "DefaultState"
}

- Wait state: delays execution of the state machine.
- Succeed: stops an execution succesfully.
- Fail: stops an executions with failing.
- Parallel:  can be used to create parallel branches of execution in your state machine. Required parameter: Branches which specifies  array of objects of parallel jobs of
state machines to work out.
Example:
{
  "Comment": "Parallel Example.",
  "StartAt": "LookupCustomerInfo",
  "States": {
    "LookupCustomerInfo": {
      "Type": "Parallel",
      "End": true,
      "Branches": [
        {
         "StartAt": "LookupAddress",
         "States": {
           "LookupAddress": {
             "Type": "Task",
             "Resource":
               "arn:aws:lambda:us-east-1:123456789012:function:AddressFinder",
             "End": true
           }
         }
       },
       {
         "StartAt": "LookupPhone",
         "States": {
           "LookupPhone": {
             "Type": "Task",
             "Resource":
               "arn:aws:lambda:us-east-1:123456789012:function:PhoneFinder",
             "End": true
           }
         }
       }
      ]
    }
  }
}

- Map:  
