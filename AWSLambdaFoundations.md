---
text: "AWS Skillbuilder"
title: "AWS Lambda Foundations"
author: "Peter Farrar"
date: 04/09/2025
description: "Learning basics on AWS Lambdas"
---

<div>
  <style class="zebra-striped-list-box">
    .wrapper {
        border: 1px solid #666;
    }
    .heading {
      background-color: #222;
      color: #DDD;
      padding: 1rem;
      border: 1px solid #666;
      font-size: 1.2rem;
      text-align: center;
    }
    .table-wrapper {
      padding: 5%;
    }
    table {
      margin: 0 auto;
      width: 100%; 
    }
    th {
      padding: 1rem;
    }
    li.invisible {
      list-style-type: none;
    }
    td.row-number {
      text-align: center;
      width: 10%;
    }
    .top {
        vertical-align: top;    
    }
    .half {
      width: 50%;
    }
  </style>
</div>

# AWS Lambda Foundations

[The AWS Lambda Developers Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html). can provide more details on the topics covered in this course.  

## Course Introduction

Objectives:  

* Define Lambda and describe how it works
* Describe the benefits of using Lambda use cases
* Examine Lambda function permissions and security
* Demonstrate best practices for writing Lambda functions
* Deploy and test your serverless applications
* Explore Lambda configuration considerations
* Monitor and troubleshoot Lambda functions

## Introduction to Serverless

Serverless applications allow developers to create event driven functions without consideration for the operating system or hardware platform.  

### Serverless operational tasks

<div class="wrapper">
  <style>
    .row-header {
      width: 55%;
    }
    .plumb th {
        background-color: rgb(94, 20, 111);
        color: white;
        vertical-align: top;
    }
    .white td {
        background-color: white;
        color: rgb(62, 61, 61);
        font-weight: 500;
    }
    .center {
        text-align: center; 
        vertical-align: middle;    
    }
    .border-lt td, th {
        border-collapse: collapse;
        border: 1px solid #999;
    }
  </style>
  <div class="heading">
  Traditional vs. Serverless
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="">Deployment and Operational tasks</th>
          <th class="">Traditional<br />Environment</th>
          <th class="">Serverless</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="row-header">Configure an instance</td>
          <td class="center">YES</td>
          <td class="center">-</td>
        </tr>
        <tr class="">
          <td class="row-header">Update operating system (OS)</td>
          <td class="center">YES</td>
          <td class="center">-</td>
        </tr>
        <tr class="">
          <td class="row-header">Install application platform</td>
          <td class="center">YES</td>
          <td class="center">-</td>
        </tr>
        <tr class="">
          <td class="row-header">Build and deploy apps</td>
          <td class="center">YES</td>
          <td class="center">YES</td>
        </tr>
        <tr class="">
          <td class="row-header">Configure automatic scaling and load balancing</td>
          <td class="center">YES</td>
          <td class="center">-</td>
        </tr>
        <tr class="">
          <td class="row-header">Continuously secure and monitor instances</td>
          <td class="center">YES</td>
          <td class="center">-</td>
        </tr>
        <tr class="">
          <td class=" row-header">Monitor and maintain apps</td>
          <td class="center">YES</td>
          <td class="center">YES</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

### Aws serverless platform

The AWS serverless platform includes a number of services tightly integrated with Lambda.  

Services in the AWS serverless platform:  

* Compute
  * AWS Lamnda
* Orchestration
  * AWS Step Functions
* Storage
  * Amazon S3
* Data Stores
  * Amazon DynamoDB
* Event Bus
  * Amazon EventBridge
* Interprocess Messaging
  * Amazon SNS
  * Amazon SQS
* API Integration
  * Amazon API Gateway
  * AWS AppSync
* Developer Tools
  * AWS Cloud Development Kit (AWS CDK)
  * AWS Serverless Application Model (SAM)

### What is AWS Lambda

Lambda is a compute service. It maintains all the compute resources including server and OS maintenance, capaity provisioning and auto scaling, code monitoring, and logging.  

Benefits include:  

* You can **run code** without provisioning or maintaining servers
* It **initiates functions** for you in response to events
* It **scales** Automatically
* It provides built-in code **monitoring and logging** via Amazon CloudWatch

### AWS Lambda features

Six main features:  

1. _Bring your own code_: Supports multiple langauges and is not tightly coupled to AWS. Easy to port code in and out of Lambda.
2. _Integrates with and extends other AWS services_: Do anything traditional applications do, including calling AWS services, or third party services.
3. _Flexible resource and concurrency model_: Lambda scales in response to events. Configure memory settings and AWS handles the other details
4. _Flexible permissions model_: Lambda uses the AWS IAM permissions model to grant fine grained access to resources
5. _Availability and fault tolerance are built in_: Lambda is a fully managed service. No configuration is required for availability.
6. _Pay for value_: Lambda functions only run when they are triggered by an event. Charges are based on the compute time consumed. Billing is on a 1-millisecond incremental basis.

### Event-driven architectures

Actions are initiated by events. Events could be changes in a log file, a message on a message queue, a change in application state.  

### Producers, routers, consumers

Most AWS servers generate events. Lambdas cosume events, and possibly generate more events. The pattern is:  

```
Event producer -> Event router -> Event consumer
```

Producers:  
 
* Mobile app
* Retail website
* Point-of-sale

Routers are:  

* Amazon Event Bridge

Consumers are:  

* Warehouse Mgmt DB
* Finance System
* Customer Service

### What is a Lambda function?

The code Lambda runs is called a _Lambda function_. They are stateless. Many copies can be launched to scale for the rate of incoming events.  

AWS Lambda can configure an event source, such as an S3 bucket event, a Kinesis stream, a Simple Notification Service (SNS) notification.  

## How AWS Lambda Works

### Invocation models for running Lambda functions

There are three general patterns for invoking Lambda functions:  

<div class="wrapper">
  <div class="heading">
  Invocation models for running Lambda functions
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="">Invocation</th>
          <th class="">AWS services</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="top">Sychronous</td>
          <td class="">
            <ul>
              <li>Amazon API Gateway</li>
              <li>Amazon Congnito</li>
              <li>AWS CloudFormation</li>
              <li>Amazon Alexa</li>
              <li>Amazon Lex</li>
              <li>Amazon CloudFront</li>
            </ul>
          </td>
        </tr>
        <tr>
          <td class="top">Asynchronous</td>
          <td class="">
            <ul>
              <li>Amazon SNS</li>
              <li>Amazon S3</li>
              <li>Amazon EventBridge</li>
            </ul>
          </td>
        </tr>
        <tr>
          <td class="top">Polling</td>
          <td class="">
            <ul>
              <li>Amazon DynamoDB</li>
              <li>Amazon Kinesis</li>
              <li>Amazon MQ</li>
              <li>Amazon Managed Streaming for Apache Kafka (MSK)</li>
              <li>self-managed Apache Kafka</li>
              <li>Amazon SQS</li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

### Invocation model error behavior

<div class="wrapper">
  <div class="heading">
  Invocation model error behavior
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="">Invocation</th>
          <th class="">Error Behavior</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="top">Sychronous</td>
          <td class="">No retries</td>
        </tr>
        <tr>
          <td class="top">Asynchronous</td>
          <td class="">Built in - retries twice</td>
        </tr>
        <tr>
          <td class="top">Polling</td>
          <td class="">Depends on event source</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

### Lambda execution environment

Lambda invokes functions in a secure and isolated environment that manages the required resources for each function, as well as lifecycle support and any external associated extensions.  

Execution environment lifecycle:  

1. INIT phase
2. INVOKE phase
3. SHUTDOWN phase

#### INIT phase

The INIT phase executes in three sub-phases:  

1. Extention init - starts all extensions
2. Runtime init - bootstraps the runtime
3. Function init - runs the function's static code

#### INVOKE phase

In the INVOKE phase the function handler is invoked. When the lambda finishes, the Lambda waits for the next invocation.  

#### SHUTDOWN phase

After a set period of time, if no more invocations are received, the Lambda shuts down the runtime, triggers the extensions to shut down cleanly, and removes the environment.  

Nore information about the execution environment lifecycle is available [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html).  

### Performance optimization

Although the Lambda service manages scaling automatically, functions can be optimized to reduce latency and increase throughput.  

#### Cold start

When a function hasn't been invoked for sometime, the first invocation requires the INIT phase before the function can be executed.  

#### Warm start

When a function has been invoked recently, the INIT phase doesn't need to be run, and so the response time is faster.  

#### Best practice: Minimize cold start times

Optimize functions with the latency of a cold start in mind.  
**Provisioned concurrency** keeps functions initialized and worm by preparing multiple, concurrent, execution environments. More information is available [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html).  

#### Best practice: Write functions to take advantage of warm starts

1. Store and reference dependencies locally.
2. Limit re-initialization of variables.
3. Add code to check for and reuse existing connections.
4. Use tmp space as transient cache.
5. Check that background processes have completed.

## AWS Lambda Function Permissions

Permissions and security in your Lambda functions.  

There are two sides that define the scope of permissions for lambda functions:  

* Permission to invoke the Lambda function
* Permissions of the Lambda function to act upon other services

Invocation permissions are controlled with an IAM resource-based policy. An execution role controls what the function can do with other services.  

### Execution role

The execution role provides the function with permissions to interact with other services. This role is provided when the function is created and the Lambda service assumes this role when it executes the function. The role must include a `AssumeRole` trust policy is necessary to allow the Lambda service to assume it.  

When creating a role for a Lambda function, remember to use the _principle of least privilege_.  

[The IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html) may help identify permissions required for the execution role.  

More information on Lambda permissions can be found [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html).  

### Resource-based policy

A resource policy tells the Lambda service which _principals_ can invoke the function. A _principle_ can be a user, role, AWS service, or an AWS account.  

A resource-based policy is an easier option to allow invoking of the Lambda function. It can be modified in the lamdba console.  

Resource policies and resource-based policies have a limit to the number of accounts it can add. If the limit is exceeded, an execution role would beed to be used instead.  

<div class="wrapper">
  <div class="heading">
  Policy comparison
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="">Resource-Based Policy</th>
          <th class="">Execution Role</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="top half">
          Lambda resource-based (function) policy:<br />
            <ul>
              <li>Associated with a "push" event source such as Amazon API Gateway</li>
              <li>Created when you add a trigger to a Lambda function</li>
              <li>Allows the event source to take the <i>lambda:InvokeFunction</i> action
              </li>
            </ul>
          </td>
          <td class="top half">
          IAM execution role<br />
            <ul>
              <li>Role selected or created when you create a Lambda function</li>
              <li>IAM policy includes actions you can take with the resource</li>
              <li>Trust policy that allows Lambda to <i>AssumeRole</i></li>
              <li>Creator must have permissions for <i>iam:PassRole</i></li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

### Ease of management

AWS SAM can help manage policies.  

### Accessing resources in a VPC

Accessing resources inside a virtual private cloud (VPC) requires additional configurations with VPC-specific information and an execution role with permissions to create, describe, and delete elastic network interfaces. More information can be found [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html).  

#### Lambda and AWS PrivateLink

A private connection between a Lambda function and a VPC requires a VPC endpoint, powered by AWS PrivateLink. This connection doesn't leave the AWS network. More information about this can be found [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc-endpoints.html).  

## Authoring AWS Lambda Functions

###  AWS Lambda programming model: Use your own code

<div class="wrapper">
  <style>
    td.tall {
      padding-top: 1rem;
      padding-bottom: 1rem;
    }
  </style>
  <div class="heading">
  AWS Lambda programming model
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="center">Supported Languages</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="center tall">Node.js</td>
        </tr>
        <tr>
          <td class="center tall">Python</td>
        </tr>
        <tr>
          <td class="center tall">Java</td>
        </tr>
        <tr>
          <td class="center tall">Go</td>
        </tr>
        <tr>
          <td class="center tall">C#</td>
        </tr>
        <tr>
          <td class="center tall">Ruby</td>
        </tr>
        <tr>
          <td class="center tall">PowerShell</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
&nbsp;

AWS provides plugins for most popular IDEs, including:  

* VS Code
* Eclipse
* IntelliJ
* PyCharm

(nothing for Vim?)  

#### Start with the handler method

The Lambda function handler is the method that processes events. The handler takes two parameters, the event object and the context object. (so where does the callback come from?).  

##### Event Object

* The event object is required
* When the Lambda function is invoked, the event object is passed in
* The event object differs in structure and content depending on which source created it
* The contents of the event parameter include all of the data and metadata the function needs to drive its logic
  
For more information, see [The Event Object](https://aws.amazon.com/lambda/serverless-architectures-learn-more/) in "Serverless Architectures with AWS Lambda" whitepaper.  

##### Context Object

* The context object allows the function code to interact with the Lambda execution environment
* The contents and structure of the contexxt object vary, based on the language runtime the Lambda function uses. At minimum it contains:
  * AWS RequestID - Used to track specific invocations
  * Runtime - The amount or time in milliseconds remaining before a function timeout
  * Logging - Information about which Amazon CloudWatch Logs stream log statements will be sent to

For more information, see [The Content Object](https://aws.amazon.com/lambda/serverless-architectures-learn-more/) in "Serverless Architectures with AWS Lambda" whitepaper.  

### Design best practices

Seperate business logic from the handler method. This is better for writing unit tests. Make the Lambda modular. Seperate functionality like compression, encryption, etc. Follow the same principles as would be applied to developing microservices. Remember, Lambda functions are stateless. Services like DynamoDB, ElastiCache, and S3 can be used to store data between executions. Minimize the size and startup time by only including what is needed. For AWS, choose modules for specific functionality, rather than importing the entire SDK. The [_AWS Lambda Developers Guide_](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html) has more information on best practices.  

### Best practices for writing code

#### Include logging statements

Logging statements are written to CloudWatch. For example:  

```python
import os
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
  logger.info('## ENVIRONMENT VARIABLES')
  logger.info(os.environment)
  logger.info('## EVENT')
  logger.info(event)
```

#### Use return coding

Functions should give Lambda information about the results of their actions. Use return appropriate values when exiting the code.  

```javascript
exports.handler = async function(event, context) {
  console.log("EVENT: \n" + JSON.stringify(event, null, 2))
  return context.logStreamName
}
```

#### Provide environment variables

Environment variables are useful to pass updated configuration settings without haveing to change code. They are also useful for storing sensitive data, like passwords and secrets. Lambda uses encryption keys to protect those values. More information is available [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html).  

#### Add secret and reference data

_AMS Secrets Manager_ helps organize and manage important configuration data like credentials and license keys.  

_Parameter Store_ integrates with Secrets Manager to retrieve secrets for Lambda. This allows for a secure and consistant process for calling and using secrets and reference data in Lambda functions and configuration scripts. Parameter Store integrates with IAM for fine-grained access control.  

_AWS AppConfig_ can source, validate, deploy, and monitor configurations in Parameter Store, System Manager Document Store, S3, and more. More information is available [here](https://docs.aws.amazon.com/appconfig/latest/userguide/what-is-appconfig.html).  

#### Avoid recursive code

Avoid functions that call themselves. If you set the concurrent execution limit to zero, it will throttle requests. Use this if a recursive call is accidentally depolyed.  

#### Gather metrics with Amazon CloudWatch

The Embedded Metric Format (EMF) is a JSON specification used by CloudWatch. The metrics they store can be used to build graphs and set alarms. More information is available [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Embedded_Metric_Format_Specification.html).  

#### Reuse execution contetxt

1. Store dependencies locally
2. Limit re-initialization of variables
3. Reuse existing connections
4. Use tmp space as transient cache
5. Check that background processes have completed

### Building Lambda Functions

There are three ways to build and deploy Lambda functions:  

1. The Lambda console editor
2. Deployment packages
3. Automation tools

#### Lambda console editor

Building functions in the Lambda console is the best place to start learning to code lambdas. This assumes your code doesn't require custom libraries other than the AWS SDK.  

#### Deployment packages

Lambda supports two types of deployment pacakges: Container images and zip file archives. Zip files can be uploaded to an S3 bucket or a container image apdh pushed to Amazon Elastic Container Registry (Amazon ECR). More information is avialble in [Using container image support for AWS Lambda with AWS SAM](https://aws.amazon.com/blogs/compute/using-container-image-support-for-aws-lambda-with-aws-sam/) in the AWS Compute Blog.  

#### Automate using tools

Lambda serverless applications are a combination of functions, event sources, and other resources defined using AWS SAM. SAM can be used to automate deployment, as well as AWS CodeBuild, AWS CodeDeploy, and AWS CodePipeline.  

More information is available in the [Deploying serverless applications](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-deploying.html) section of the _AWS Serverless Application Model Developers Guide_.

### What is AWS SAM?

AWS SAM is an open-source framework for building serverless applications. It has a short-hand syntax for expressing functions, APIs, databases, and event source mappings. Applications are defined using YAML. SAM transforms these instructions into an AWS CloudFormation template.  

### AWS SAM prebuilt policies

Predefined, commonly used tempates can be used to build for least privilege security access. These can be used to scope the permissions of a Lalmbda function to only the resources it needs. More information is available in [AWS SAM policy templates](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-policy-templates.html) in the _AWS Serverless Application Module Developer Guide_.  

### AWS SAM CLI helps you test and deploy

SAM launches a Docker container that it interacts with to test and debug Lambda functions.  

#### AWS SAM CLI for testing

SAM CLI can do the following for testing:  

* Invoke functions and run automated tests locally
* Generate sample event source payloads
* Run API Gateway locally
* Debug code
* Review Lambda function logs
* Validate AWS SAM templates

### AWS SAM CLI

Key SAM CLI commands:  

#### init

Initializes a serverless application.  

#### local

Runs your application locally.  

#### validate

Validates an AWS SAM template.  

#### deploy

Deploys an AWS SAM application.  

Using the `--guided` flag puts the `deploy` in an interactive mode. This walks through the options for the deploy and saves them in a configuration file for later use.  

CloudFormation deployments require an A3 bucket for the Lambda deployment package. SAM CLI creates and manages this.  

#### build

Builds the serverless application. Running `sam build` processes the AWS SAM template file, application code, and languge-specific files and dependencies. It also copies build artifacts in the format and location expected for subsequent steps in the workflow.  

Additional information can be found [here](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-build.html).  

### Serverless CI/CD pipeline

Additional tools can be incorporated to create an automated CI/CD pipeline for serverless applications that integrate with SAM.  

* CodeBuild - Automates packaging code and running tests pre-deployment.
* CodeDeploy - Ensures safe deployments busing version management options.

&nbsp;

---

## Configuring Your Lamda Functions

When building a function, there are three primary configuration settings:  

* Memory
* Timeout
* Concurrency

To find the right values for these requires monitoring your production environment and adjusting settings accordingly to optimize costs while ensuring the desired customer experience.  

#### Memory

Lambdas can be configured for up to 10 GB of memory. Lambda allocates CPU and other resources linearly in proportion to the allocated memory. More information is available in the [_AWS Lambda Power Tuning tool_](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:451282441545:applications~aws-lambda-power-tuning)  

#### Timeout

The maimum timeout allowed for a Lambda function is 900 seconds (15 minutes). It's recomended in most situations to allow the function to fail fast, rather than waiting for the timeout. Load testing is the best way to determine the correct timeout value for a function.  

### Lambda billing costs

Charges for Lambdas are based on the number of invocations and the functions runtime in milliseconds increments. Price depends on the amount of memory allocated.  

Useful resources:  

* [AWS Pricing Calculator](https://calculator.aws/#/)  
* [Lambda specific pricing](https://aws.amazon.com/lambda/pricing/)  

### The balance between power and duration

Sometimes more memory causes faster job completion, leading to lower costs. The Lambda Power Tuning tool (see above) can help find the best configuration for a function. It visualizes the memory and power configuration, and supports three optimization strategies:  

* Cost
* Speed
* Balanced

### Concurrency and scaling

#### Concurrent invocations

This is the number of instances that can run at the same time.  

### Concurrency types

#### Unreserved concurrency

The amount of cuncurrency that is not allocated to any specific set of functions. The minimum is 100 unreserved concurrency. This allows functions that do not have any provisioned concurrency to still be able to run. If all concurrency is provisioned to one or two functions, there is no concurrency left for any other functions. So no other functions can run.  

#### Reserved concurrency

The guarenteed maximum number of concurrent instances for a function. Reserved concurrency is only used by the function for which it is reserved.  

#### Provisioned concurrency

A requested number of pre-initialized environments for a function. The charge for this is based on the number of concurrencies and the period of time durring which they exist.  

#### Reasons for setting concurrency limits

<div class="wrapper">
  <div class="heading">
  Reasons for setting concurrency limits
  </div>
  <div class="table-wrapper">
    <table class="border-lt">
      <thead>
        <tr class="plumb">
          <th class="center">Limit Concurrency</th>
          <th class="center">Reserve Concurency</th>
        </tr>
      </thead>
      <tbody class="white">
        <tr>
          <td class="top half">
            Limit a function's concurrency to achieve the following:
            <ul>
              <li>Limit costs</li>
              <li>Regulate how long iit takes you to process a batch of events</li>
              <li>Match it with a downstream resource that cannot scale as quickly as Lambda</li>
            </ul>
          </td>
          <td class="top half">
            Reserve function concurrency to achieve the following:
            <ul>
              <li>Ensure that you can handle peak expected volume for a critical function</li>
              <li>Address invocation errors</li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

### How concurrency bursts are managed

A burst is a sudden increase in the number of instances needed to fullfill incoming requests. The burst concurrency quota is not per function. It applies to all functions in the region.  

#### Burst quotas by region

* 3000 - US West (Oregon), US East (N. Virginia), Europe (Ireland)
* 1000 - Asia Pacific (Tokyo), Europe (Frankfurt), US East (Ohio)
* 500 - Other regions

After the initial burst, functions' concurrency can scale an additional 500 instance per minute until there are enough to serve all requests, or a concurrency limit is reached.  

More information is available in the [AWS Lambda function scaling](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html) section of the _AWS Lambda Developer Guide_.  

### CloudWatch metrics for concurrency

Lambda sends metrics about each invocation to CloudWatch. These can be used to build graphs and dashboards in the CloudWatch console. You can also set alarms to respond to use, performance, and error rates.  

CloudWatch has two built in metrics to help determine concurrency:  

#### `ConcurrentExecutions`

Historical data on function performance, including the number of concurrent invocations at a point in time. This can focus on all functions in the account, or functions with custom concurrance limits.  

#### `UnreservedConcurrentExecutions`

The number of concurrent functions that don't have a custom concurrency limit.  

### Testing concurrency

* Run performance tests that simulate peak levels
* Determine whether the existing backend can handle the speed of requests
* Cerify error handling works as expected

---

## Deploying and Testing Serverless Applications

CloudFormation defines every detail of the Lambda function and the environment required for the function to run in the CloudFormation template.  

### Server-based development environments

Basic workflow:  

1. Author code
2. Test and debug changes in isolation
3. Merge code into larger application codebase and perform application testing

Server based workflow:  

1. pull down local copy of application
2. Work localy in IDE
3. Test and debug code
4. check in to source control

### Serverless development environment

* Code, bundled with any necessary dependencies
* CloudFormation template

CloudFormation templates can be lengthy. 100 lines is not unusual. They include IAM roles, API Gateway endpoints, connections to other services.  

#### A key difference in the developer workflow i how the code and the application are tested

The applicatoin can not be checked out and tested locally. Developers must have access to the cloud resources. Applications are deployed in cloud environments.  

#### AWS SAM makes serverless development easier

SAM uses a simplified instruction set to create a CloudFormation template.  

#### Ensures environmental parity

SAM streamlines creating and deploying a stack to multiple environments.  

#### Simplicies experimentation

SAM can easily try out different feature branches.  

--- 

Useful SAM command. Call from root of project to validate the `template.yaml` file:  

```bash
% sam validate
```

---

### Reduce risk using versions and aliases

Because Lambdas go live the moment they are pushed, it's advised that versioning and aliases are used to prevent accidentally promoting code to production without testing.  

#### Versioning

Versions can be created to help manage the deployment of functions. A new version is created whenever a function is pushed. The latest version is called $LATEST:

```
arn:aws:lambda:aws-region:acct-id:function:funtionname:$LATEST
```

#### Publish

Enable versioning to create immutable snapshots of functions when published.

* Publish as many versoins as needed
* Each version results in a new sequential version number
* Add the version number to the function ARN to reference it
* The snapshot becomes the new version and is immutable

```
arn:aws:lambda:aws-region:acct-id:function:funtionname:21
```

#### Aliases

An alias is like a pointer to a specific version. An alias points to a version ARN. It can not point to another alias:  

```
arn:aws:lambda:aws-region:acct-id:function:funtionname:Test
```

### Test using alias routing

Routing can be configured to send only a percentage of the traffic to a specific version. This can be used to test new changes before routing all traffic to the new version.  

* Both versions must have the same runtime role
* Both versions must have the same dead-letter queue configuratoin, or no dead-letter queue configuration
* Both versions must be published. The allias cannot point to $LATEST

### Integrate with AWS CodeDeploy

CodeDeploy supports multiple traffic shifting methods.

* **Canary** - traffic is shifted in two increments. If the first increment is successful, the second is completed based on the time specified in the deployment.
* **Linear** - With linear traffic shifting, traffic is slowly shifted in a predetermined percentage every _X_ minutesbased on how it is configured.
* **All-at-once** - Shifts all traffic from the original lambda function to the updated lambda function version at once.

Additional testing options in AWS CodeDeploy:  

* **Alarms** - These instruct CloudWatch to monitor the deployment and trigger an alarm if any errors occurred durring rollout. Any alarms would automatically roll back your development.
* **Hooks** - Give you the option to run pre-traffic and post-traffic test functions that run sanity checks before traffic-shifting starts to the new version and after traffic-shifting completes.

**Note:** When rollbacks are triggered by a hook or alarm, the entire CloudFormation template is rolled back. It's best practice to keep AWS SAM templates and CloudFormation templates as concise as possible.  

## Shift traffic for Lambda using AWS CodeDeploy

SAM can configure CodeDeploy traffic-shifting options.  

`AutoPublishAlias` directs SAM to publish an alias and increment the version on every deployment.  
`DeploymentPreference` specifies the traffic-shifting option to use.  
`Alarms` instructs CloudWatch to monitor the deployment and trigger an alarm if there are errors.  
`UseHooks` with `PreTraffic` and `PostTraffic` runs test functions and sanity checks before the traffic shifting starts and after it completes.

---

## Monitoring and Troubleshooting

Lambda integrates with other AWS services to monitor and troubleshoot Lambda functions.

### Types of monitoring graphs

Lambda automatically tracks the following:  

* Number of requests
* Invocation durration per request
* Number of requests that result in an error

CloudWatch provides built-in metrics to help monitor Lambda functions:  

#### Invocations

The number of timmes function code is run, successfully and unsucessfully. Invocation errors are not counted.  

#### Duration

Time spent processing an event. This is the basis for billing (rounded up to the closest millisecond).  

#### Errors

The number of invocations that result in a function error. This includes exceptions thrown within the function, and errors thrown by the Lambda engine.  

#### Throttles

The number of times Lambda rejects a request because there is no concurrency to run another instance.  

#### IteratorAge

If events are read from a stream, this is the age of the last record in the event, the amount of time the record has exited in the stream.  

#### DeadLetterErrors

For asynch only, the number of times Lambda attempts and fails to send an a dead-letter queue.  

#### ConcurrentExecutions

The number of function instances processing events. This can be further refined to:  

* **UnreservedConcurrentExecutions** - The number of events being processed by functions that don't have reserved concurrency
* **ProvisionedConcurrentExecutions** - The number of function instaces processing events on provisioned concurrency.

### Amazon CloudWatch Lambda Insights

Lambda Insights is a monitoring and troubleshooting solution for serverless applications running on Lambda. It collects, aggrigates, and summarizes system-level metrics, summarizes diagnostic information, and helps isolate issues and resolve them quickly.  

#### Lambda Insights dashboard

The Lmbda Insights dashboard has two vies in the CloudWatch console:

* Multi-function overview - an aggregation of runtime metrics for the account and region.
* Single-function view - runtime metrics for a single function.

These are useful for identifying over and under utilized functions, and to trouble shoot individual requests.  

### Monitoring Lambda functions using AWS X-Ray

X-Ray records how Lambda functions are running. It can be used for:  

* Tuning performance
* Identifying the call flow of Lambda functions and API calls
* Tracing path and timing of an invocation to locate bottlenecks and failures

### Aditional monitoring and troubleshooting tools

#### AWS CloudTrail

Records all the API actions made against the applicatoin. Logs can be edported for use by analysis tools.  

* Control plane (management) events on by default
* Data event logging optional.

#### Dead-letter queues

Captures applicatoin errors that must receive a response. The response is moved to a dead-letter queue and used to identify and fix the problem.  

* Use dead-letter queues to analyze failures for follow-up or code corrections.
* Dead-letter queues are available for asynchronouse and non-stream polling events.
* A dead-letter queue can be an Amazon Simple Notification Service (SNS) topic or an Amazon Simple Queue Service (SQS) queue.

Dead-letter quese can be configured from the Lamnda console.  

---

## Additional Resources

#### Websites:

* [AWS Serverless Land](https://serverlessland.com/)
* [AWS homepage: Serverless on AWS](https://aws.amazon.com/serverless/)
* [AWS Lambda Operator Guide](https://docs.aws.amazon.com/lambda/latest/operatorguide/intro.html)
* [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

#### Whitepapers:

* [AWS Serverless Multi-Tier Architectures Whitepaper](AWS Serverless Multi-Tier Architectures Whitepaper)
* [Security Overview of AWS Lambda Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/security-overview-aws-lambda/security-overview-aws-lambda.pdf)

#### Blogs

* [AWS Compute blog for Lambda](https://aws.amazon.com/blogs/compute/category/compute/aws-lambda/)

#### Online serverless workshops

* [Build On Serverless Season 2](Build On Serverless Season 2)

#### Recored talks

* [Customer Talks](https://aws.amazon.com/lambda/resources/customer-talks/)
* [Tech Talks](https://aws.amazon.com/lambda/resources/webinars-and-talks/)

#### Other courses in the serverless learning path

* [Amazon API Gateway for Serverless Applications (digital training)](https://www.aws.training/Details/eLearning?id=27199)
* [Amazon DynamoDB for Serverless Architectures (digital training)](https://www.aws.training/Details/eLearning?id=27196)
* [Architecting Serverless Solutions (digital training)](https://www.aws.training/Details/eLearning?id=42594)
* [Developing Serverless Solutions on AWS (classroom training)](https://www.aws.training/SessionSearch?pageNumber=1&courseId=53785&languageId=1)

---
