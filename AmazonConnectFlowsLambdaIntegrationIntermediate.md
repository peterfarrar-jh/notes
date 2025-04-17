---
text: "AWS Skillbuilder"
title: "Amazon Connect Flows Lambda Integration Fundamentals"
author: "Peter Farrar"
date: 04/09/2025
description: "Intermediate learning on Amazon Connect Flows integration with Lambda"
---

# Amazon Connect Flows Lambda Integrations Intermediate

## Flows and AWS Lambda Integration

### Synchronous Process

* Recognize the pattern for implementing Lambda functions for synchronous processes.

#### Lesson introduction

Amazon Connect can invoke Lambdas synchronously. Lambda integration allows soutions for use cases like:  

* Query internal and external data sources, allowing personalized interactions, improved routing, and automated operational tasks.
* Interact with other AWS and 3rd party services, allowing customers self-service options.
* Update innternal and external data stores using information gathered within the contact flow.

#### Lambda timing

Amazon Connect can wait up to 8 seconds for a response from an AWS Lambda call. It can be configured to wait less, but not more than 8 seconds. Lambda functions also have a configurable timeout. It is important that the Amazon Connect and AWS Lambda timeout configurations match.  

#### Invoking Lambda functions for synchronous operations

##### Use case

A module calls a lambda function, passing it the phone number of the caller. The function queries DynamoDB and either returns the caller details, including prefered language, or that the customer is not found. If the lambda returns the prefered language, the flow will route appropriately. If the customer is unknown, or the lambda doesn't return in a timely manor, the customer is routed to a default route that prompts for their prefered language.  

### Asynchronous Process

* Explore design techniques for long running processes.
* Recognize use cases for asychronous operations.

#### Lesson introduction

Some Lambda calls do not need to return data to the flow. Other operations might take more than the maximum 8 seconds to complete. Asynchronous calls can help Amazon Connect execute long running processes.  

#### Invoking Lambda for asynchronous processes

Amazon Connect can only activate Lambdas synchronously. Here is the pattern to kick off async processes:  

1. Invoke a synchronous Lambda function
2. The Lambda function kicks off an asynchronous Lambda function that creates a record in Dynamo and returns the key value, which the first Lambda returns to Amazon Connect.
3. The async function does what it does, and updates Dynamo with the results
4. Later in the flow a third Lambda is invoked to retrieve the data from Dynamo

Amazon connect limits duration of a sequence of Lambda functions to 20 seconds. By breaking these into segments a designer can run processes that last longer than the limit.  

## Error Handling, Monitoring, and Troubleshooting

### Handling Integration Errors

* Recognize best practices to handle flow and Lambda integration errors.
* Identify use cases for error handling.

#### Lesson Introduction

Sometimes Lambdas are not successful. This lesson is about how to handle errors that may impact flow experience.  

#### Handling flow block errors

Flow blocks can set default routes to follow when the Lambda call returns an error.  

#### Handling Lambda function errors

By returning informational errors, Amazon Connect can make decisions based on the kind of error generated. For example:  

* Retry the Lambda 
* Try an alternative route to obtain information
* Enrich the contact with attributes
* Decide to route to a specific agent or agent group
* Decide to disconnect the contact
* Dynamically update the content of a voice prompt

### Monitoring and Troubleshooting Integrations

* Identify the Invoke AWS Lambda function flow block log event structure.
* Recognize the benefits of CloudWatch log groups, metrics, and logs insights to monitor, alert, and troubleshoot Lambda invocations from flows.

#### Lesson Introduction

Amazon Connect sends data to CloudWatch metrics. Flow logs are stored in a CloudWatch log group in the same region as the instance.  

#### Accessing flow logs

Logs are created if:  

* The Enable Flow logs setting is set in the Amazon Connect instance configuration
* The flow includes a _Set logging behavior block_ with logging set to 'enabled'

The logs are found in the _Logs_ section, _Log groups_, named `/aws/connect/<instance-alias>`  

#### Using Invoke AWS Lambda funtion block logs

Amazon Connect creates a log for each flow block that is activated durring a contact interaction.  

Here is an example of a successful _AWS Lambda function flow block_:  

```json
{
    "ContactId": "fba006bc-e6ed-4f17-b7a1-xxxxxxxxxxxx",
    "ContactFlowId": "arn:aws:connect:aws-region:xxxxxxxxxxxx:instance/ ...",
    "ContactFlowName": "Sample Flow name",
    "ContactFlowModuleType": "InvokeExternalResource",
    "Identifier": "0c51520c-6249-4ff9-9feb-xxxxxxxxxxxx",
    "Timestamp": "2024-05-04T22:28:30.474Z",
    "ExternalResults": {
           "customerName": "Arnav Desai",
           "accountTYpe": "Gold",
           "Age" : "30"
},
"Parameters": {
       "FunctionArn": "arn:aws:lambda:aws-region:xxxxxxxxxxxx:function:...",
       "ResponseValidation": "ResponseType=STRING_MAP",
       "TimeLimit": "3000"
    }
}
```

You can see useful information such as identifiers, flow name, inputs and outputs, and a timestamp.  

Here is an example of an unsuccessful _AWS Lambda function flow block_:

```json
{
    "Results": "The Lambda Function Returned An Error.",
    "ContactId": "fba006bc-e6ed-4f17-b7a1-xxxxxxxxxxxx",
    "ContactFlowId": "arn:aws:connect:aws-region:xxxxxxxxxxxx:instance/...",
    "ContactFlowName": "Sample Flow name",
    "ContactFlowModuleType": "InvokeExternalResource",
    "Identifier": "0c51520c-6249-4ff9-9feb-xxxxxxxxxxxx",
    "Timestamp": "2024-05-15T11:40:34.056Z",
    "Parameters": {
           "FunctionArn": "arn:aws:lambda:aws-region:xxxxxxxxxxxx:function:...",
           "ResponseValidation": "ResponseType=STRING_MAP",
           "TimeLimit": "3000"
    }
}
```

This Lambda has returned an error, as you can see in the `Results` element. When a Lambda returns an error, the `ExternalResults` element is absent.  

To view just the _AWS Lambda function block_ logs, filter on a pattern like: `{ $.ContactFlowModuleType = "InvokeExternalResource" }`  

#### Using log groups and metrics to monitor integration Lambda functions

Monitoring integration Lambda invocations is considered an important part of operational excellence. Two metrics of interest are:  

* **ContactFlowErrors**: The number of times the error branch for a flow was run
* **ContactFlowFatalErrors**: The number of times a flow failed to run because of a system error

CloudWatch has built-in functionality to set up [alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) or add errors to an [operational metrics dashboard](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html).  

Use CloudWatch Log Insights to query log streams for specific errors and other events.  

Examples of metrics that would be useful to monitor:  

* Overall errors in flows
* Lambda invocation errors
* Lambda responses with a failed result
* Lambda responses with a failed result and `endpointTimeout` type

