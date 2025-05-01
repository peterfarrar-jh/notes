# Amazon Connect Development Fundamentals

## Roles and Permissions

* Recognize the IAM permissions for develpers.
* Exploure how to create IAM roles and policies for Amazon Connect

### Lesson Introduction

IAM credentials are needed to perform operations programmatically. The premissions for Amazon Connect are grouped by feature. They are: list, write, read, and tagging. The Skill Builder cource [_Authentication and Authorization with AWS Identity and Access Management_](https://explore.skillbuilder.aws/learn/course/internal/view/elearning/85/authentication-and-authorization-with-aws-identity-and-access-management) has more information on IAM permissions.  

### Roles and policies for Amazon Connect developers

For programmatic access, permissions are required. Permissions are defined in policies and attached to roles. Roles are assigned to users and other resources. A policy definition is stored in as JSON in a policy document.  

Example Document Policy:  

```json
{
        "Version": "2012-10-17",
        "Statement": [
                {
                        "Sid": "ListPromptAllRegionsAndInstances",
                         "Effect": "Allow",
                        "Action": "connect:ListPrompts",
                        "Resource": "arn:aws:connect:*:123456789012:instance/*"
                },
                {
                        "Sid": "SearchProfilesAllRegionsAllDomains",
                        "Effect": "Allow",
                        "Action": [
                                 "profile:SearchProfiles"
                          ],
                         "Resource": [
                                 "arn:aws:profile:*:123456789012:domains/*"
                          ]
                 },
                 {
                         "Sid": "MultipleConnectActionsOnGranularResources",
                         "Effect": "Allow",
                          "Action": [
                                    "connect:DescribeQueue",
                                    "connect:DeleteContactFlow"
                          ],
                          "Resource": [
                                      "arn:aws:connect:ap-southeast-2:123456789012:instance/11111111-1111-1111-1111-111111111111/queue/12345678-1234-1234-1234-123456789012",
                                       "arn:aws:connect:ap-southeast-2:123456789012:instance/11111111-1111-1111-1111-111111111111/contact-flow/*"
                           ]
                 }
           ]
}
```

When defining policies and roles for AWS resources, [the principle of least privileges](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) is recomended.  

To understand the above example, it is necesary to understand the following statements:  

* ListPromptAllRegionsAndInstances
* SearchProfilesAllRegionsAllDomains
* MultipleConnectActionsOnGranularResources

#### Statement details

Every statement has a Security Identifier (Sid). This is an arbitrary name that identifies the policy.  

This section allows Amazon Connect to run the ListPrompts operation from all instances in all Regions of a specific AWS account:  

```json
{
        "Sid": "ListPromptAllRegionsAndInstances",
        "Effect": "Allow",
        "Action": "connect:ListPrompts",
        "Resource": "arn:aws:connect:*:123456789012:instance/*"
}
```

This sample allows SearchProfiles to be run on Amazon Connect Customer Profile in all domains of a specific account:  

```json
{
        "Sid": "SearchProfilesAllRegionsAllDomains",
        "Effect": "Allow",
        "Action": [
                "profile:SearchProfiles"
        ],
        "Resource": [
                "arn:aws:profile:*:123456789012:domains/*"
        ]
}
```

And This example allows running the DescribeQueue and the DeleteContactFlow operations on a specific queue in a specific Amazon Connect instance and on all flows:  

```json
{
        "Sid": "MultipleConnectActionsOnGranularResources",
        "Effect": "Allow",
        "Action": [
                "connect:DescribeQueue",
                "connect:DeleteContactFlow"
        ],
        "Resource": [
                "arn:aws:connect:ap-southeast-2:123456789012:instance/11111111-1111-1111-1111-111111111111/queue/12345678-1234-1234-1234-123456789012",
                "arn:aws:connect:ap-southeast-2:123456789012:instance/11111111-1111-1111-1111-111111111111/contact-flow/*"
        ]
}
```

## AWS CLI for Amazon Connect

* Recognize the key concepts and terminology of the AWS CLI.
* Identify the benefits of using the AWS CLI.
* Explore installing and configuring the AWS CLI.
* Explore the use of AWS CLI commands for Amazon Connect.

### Lesson Introduction

The AWS CLI is a streamlined method for developers to interact with AWS.  

### Introduction to AWS CLI

The AWS CLI allows one to controle multple AWS services from the command line and through automation scripts. Amazon Connect is fully supported. Scripts using the CLI can do the following:  

* Limit manual operations to avoid human errors.
* Automate repetitive tasks like promotion flows from dev to prod.
* Perform bulk operations like creating users or associating profiles.
* Run actions otherwise prevented in the Amazon Connect UI, like deleting flows, flow modulres, or queues.

### Access

Using the AWS CLI requires a user and an access key ID and secret key.  

### Concepts and terminology

* CLI - A text based user interface for interacting with computer systems. It is an alternative to a GUI.
* Shell - A program that provides a command line to interpret text based commands.
* Service - In this context, an AWS service.
* Commands - A specific instruction users type into the command line. This can be a shell command, or a seperate program like the AWS CLI.
* Parameters - Additional information provided to a command that modifies its behavior.
* Options - Special arguments that modify the behavior of a command. Basicly, parameters.
* Environment variables - System level settings that can be accessed and modified from the command line.
* JSON - _**J**ava**S**cript **O**bject **N**otation_ is open-standard format for data that uses human readable text to store and transmit attribute/value pairs and arrays.

### Benefits and considerations

The AWS CLI can perform the following operations for Amazon Connect features:  

* Amazon Connect resource management
* Amazon Connect Contact Lens
* Amazon Connect outbound campaigns
* Amazon Connect Cases
* Amazon Connect Customer Profiles
* Amazon Connect Participant Service
* Amazon Q in Connect

Detailed information can be found in the [AWS CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html).  

The two main benefits of the AWS CLI are:  

#### Efficiency and speed

Typing commands is faster than navigating the GUI. Scripting commands is useful for repetitive or complex tasks and improves productivity. For example, the `aws describe-contact-flow` command retrieves the definition of a contact flow. This can then be used to deploy a duplicate flow to another Amazon Connect instance.  

#### Improved level of control and customization

The AWS CLI provides more control and customization than the GUI. It allows access to advanced features that are not redily available throught the console. For example, the `aws connect list-queues` command can retrieve a list of deactivated queues from an instance that can be used to delete the queues with the `aws connect delete-queue` command.  

### Installation and configuration

The AWS CLI runs on Linux, MacOS, and Windows. Each OS has its own installation process. For detailed instructions see the [Install or Update to the Latest Version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).  

Confirm installation by running:  

```sh
% aws --version
```

FYI: AWS CLI is already installed in the AWS CloudShell.  

To configure the CLI:  

```sh
% aws configure
```

Configuring prompts for:  

* An AWS access key ID
* An AWS secret access key
* The name of a default Region to use
* The default output format

### Manage user profiles

AWS CLI can be configured to use multiple profiles. To configure a new profile:  

```sh
% aws configure --profile profile_name
```

Profiles are stored in `~/.aws/config` (on Mac and Linux).  

Profiles can be specified on the command line:  

```sh
% aws --profile profile_name connect-dev connect list-instance
```

## Amazon Connect REST APIs

* Explore benefits and considerations when using the Amazon Connect REST API.
* Explore how to set up an API client.
* Recognize the endpoint options for the Amazon Connect REST APIs.

### Lesson introduction

You can interact with Amazon Connect using the Amazon Connect RESTful APIs.  

### Introduction to the Amazon Connect REST APIs

REST APIs can be accessed by any system or language that can handle HTTP requests.  

### Concepts and terminology

* Endpoint - A specific location within an API that accepts requests and returns responses.
* Resource - A funamental concept in RESTful APIs, representing a data entity or object that can be accessed through the API.
* URI - _Uniform Resource Identifier_: a unique address or path used to identify a specific resource.
* HTTP methods - GET, POST, PUT, DELETE, sometimes PATCH, tohers.
* Request - A message sent by client to server. IncludesHTTP method, URI, headers, and optional body
* Response - The message sent from server to client. Contains status code, headers, nad optional body.
* Authentication and authorization - Mechanisms for securing APIs. Examples: API keys, OAuth, JSON Web Tokens (JWT), other.
* Throttling or rate limiting - Techniques used to control the number of requests a client can make to the API.

### Benefits of using the Amazon Connect REST APIs

REST APIs offers capabilities for managing and extending the functionality of Amazon Connect contact centers.  

#### Automation

APIs allow automation and streamlining call center operations. Manage users, queues, routing profiles, and contact flows. Improve efficiency, reduce manual effort, allow faster deployments and updates.  

#### Integration

REST APIs allow integration with other systems and applications. Custom apps can retrieve real-time metrics, use information to update other systems, even initiate outbound calls.  

Things to consider:  

#### Authentication

Amazon Connect APIs requires requests are signed using AWS Signature Version 4 (SigV4). SigV4 uses a secret access keys to create a signing key, afterwhich the secret keys are no longer needed to interact with the APIs. A seperate key is required for each date, service, and Region. Learn more in the [AWS Signature Version 4 for API Requests](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-signing.html) section of the _AWS Identity and Access Management User Guide_.  

#### Throttling

REST APIs have throttling quotas, so applications using these should have logic to handle this. See [API Throttling Quotas](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-service-limits.html#api-throttling-quotas) in the Amazon Connect Administrator Guide.  

### Setting up an API client

* Start with a secret key and secret access key. Insure access to perform Amazon  Connect operations are in place.  
* Create a collection of requests.  
* Configure the auth for all requests.  
* To configure authorization for an Amazon Connect API endpoint, read this: [Create a signed AWS API request](https://docs.aws.amazon.com/IAM/latest/UserGuide/create-signed-request.html).

Parameters to configure:  

* Access key and secret access key - This is a long term credential obtained through IAM. It will sign programatic requests to the AWS CLI or AWS APIs.  
An access key consists of an access key ID and a secret access key. Both are required to authenticate requests.  
* AWS Region - Endpoints are typically Region specific.
* Service name - The name of the service. For Amazon connect, the service is _connect_, or for customer profiles it is _profile_.
* Session token - A temporary security credential used with programmatic requests.

### Endpoints

See the [Amazon Connect endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/connect_region.html)) section of _the AWS General Reference guide_. 

### Paths, methods, and the request and response models

The URI is the path to the specific service being called. They are typically hiarchial and include the following:  


* Resource type
* Amazon Connect instance ID
* Resource ID

HTTP methods include:  

* GET - Used to retrieve the representation of a resource or collection of resources.
* POST - Used to Create or update resources in Amazon Connect.
* DELETE - Used to remove a resource from Amazon Connect.
* PUT - Used to Create or update resources in Amazon Connect.

POST and PUT requests require a body.  

## AWS SDK for Amazon Connect

* Recognize the purpose and key components of the AWS SDK.
* Explore the core concepts and terminology of the AWS SDK for Amazon Connect.
* Identify the benefits of using the AWS SDK for Amazon Connect.
* Explore the use of Amazon Connect SDK.

### Lesson Introduction

The AWS SDK for Amazon Connect is a collection of software tools designed to simplify development of new functionality for Amazon Connect.  

### Introduction to the AWS SDK for Amazon Connect

The AWS SDK for Amazon Connect includes support for various programming languages:  

* Java
* .NET
* Python (Boto3)
* JavaScript
* Go
* Many others...

### Concepts and terminology

#### AWS service clients

Service-specific clients used to interact with individual services. As well as a client for interacting with Amazon Connect, there are feature specific clients for interacting with features like _Customer Profiles_ or _Cases_.  

#### AWS credentials

The SDK requires valied AWS credentials to authenticate and authorize access to AWS resources. These could be stored as environment variables, configuration files, IAM roles.  

#### Exceptions and error handling

The AWS SDK for Amazon Connect has specific exceptions that provide detailed information on errors.  

#### Asynchronous programming

Many AWS SDKs support non-blocking, concurrent code.  

#### Throttling or rate limiting

Techniques that control the number of requests a client can make, often refered to as _transactions per second (TPS)_.  

### Benefits of using the AWS SDK for Amazon Connect

* Simplified access to Amazon Connect functionality
* Consistent and reliable
* Seamless authentication and authorization
* Language specific integration
* Support for asynchronous programming
* Ongoing maintenance and updates

When building applications consider:  

* Maintenance and updates
* Managing AWS credentials
* Error handling and exception management
* Performace and optimization
* SDK documentation

### Using the AWS SDK for Amazon Connect

Add the SDK as a project dependency. Instanciate and initialize the client. This varies depending on language.  

### AWS SDK for Amazon Connect documentation

For information about how the languages are defined, see [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/), under the language-specific documentation.  

### Using the AWS SDK for Amazon Connect in Lambda

A version of the AWS SDK is included with lambda functions. No additional installation is required. If a newer version than provided is required, creat a layer with that version. For more information on layers, read the [AWS Lambda Developers Guide](https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html).  

Advantages of using Lambdas include:  

* Serverless architecture - Allows running code directly from a contact flow, or based on an emitted event.
* Credentials - Lambdas use special IAM roles for authorization.
* Logging and monitoring - Lambda automatically sends logs from lambda functions to associated log groups in CloudWatch.

### Handling errors and retries with the Amazon Connect SDK

#### Throttling and TPS limits with Amazon Connect

Most APIs have a TPS limit of two transactions per second.  

#### Retry behavior and exponential back-off

AWS Clients can be configured to implement retry behavior. There are two important parameters:  

* Max attempts - The max number of retry attempts.
* Retry mode - The algrithm used: legacy, standard, and adaptive.

_Legacy mode_ varies by language. It has a mex retry of 3.  
_Standard mode_ defaluts to three retrys, but can be configured with a different value.  
_Adaptive mode_ - Experimental. Utilizes throttling on the application side. Behavior may change between versions.  


