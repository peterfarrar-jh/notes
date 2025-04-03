# Amazon Connect Flows Intermediate

Find the course [here](https://explore.skillbuilder.aws/learn/courses/19869/amazon-connect-flows-intermediate)

## Introduction to Amazon Connect Contact Attributes

* Recognize contact attribute types.
* Recall common use cases for contact attributes

### Introduction

An interaction with a customer is called a **contact**. Data associated with that contact is stored in _Amazon Connect contact records_, and is accessable as _contact attributes_. For example:  

* Name of the customer
* Name of the agent who handled the interaction
* Channel type

### Contact attributes

This is a key-value pair storing customer data associated with a contact. This data can be used to influence the customer journey, provide information to agents, generate reports.  

### Contact attribute types

The list of available contact attributes in Amazon Connect can be found [here](https://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html)  
The five most common type of attributes:

* _System attributes:_ Information about the Amazon Connect instance and contact identifiers (channel used, contact's phone number)
* _Agent and queue attributes:_ Information about the contact center agent and queue.
* _Amazon Lex attributes:_ Information to and from Lex chatbots.
* _External attributes:_ Information returned from external sources, like Lambdas, SalesForce.
* _User defined attributes:_ Information stored in attributes created by the designer, typically for business logic.

### Data sources

Attributes like _Dialed Number_ and _Customer Number_ are set automatically when a customer call connects to the flow. Others are updated from external sources like lambdas and Lexbots.  

### Data persistence

Some attributes are available for the duration of the contact, including:  

* System
* Media stream
* Amazon Lex
* User defined

External attirbutes populated by Lambdas are overwritten each time the function is called. Agent attributes persist only within the scope of specific flows, like _Transfer to queue_ or _Transfer to agent_. Designers can choose to store external data in user-defined attributes to persist throughout the contact.  

After the contact ends, user-defined attributes are stored in an Amazon Connect contact record.  

### Flow attributes

These attributes only persist within the flow in which they are defined. They are useful for sensitive data that should be forgotten when no longer needed.  

### Common use cases

Contact attributes can be used to personalize interactions. Common use cases are:  

* _Queued callback:_ Use the phone number to schedule a call back.
* _Post call survey:_ Associate a post call survey with agents that interacted with the customer.  
* _Dynamic routing:_ Identify if the caller should be routed to a different queue.
* _VIP treatment:_ Route VIP customers to specific queues and agents
* _Use external data:_ Use data from a customer interaction with a bot.

## Using Contact Attributes

* Recall how to access and store data in contact attributes using flow blocks.
* Explore how to store sensitive data using contact attributes.

### Lesson introduction

Personalized experiences help make customers feel valued. Using attributes, designers can store information that can help agents greet a customer by name and anticipate their intent.  

### Checking and setting contact attirbutes

#### Set contact attributes flow block

This flow block can assign values to user-defined variables for later use.  

#### Check attributes block

This flow block implements conditional logic used to direct the flow based on attribute values. It supports the following comparisons:  

* Equals
* Is Greater Than
* Is Less Than
* Starts With
* Contains

### Access contact attirbutes values using JSONPath

A list of available contact attributes and their JSONPath reference is available [here](https://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html)  

Some blocks can access attributes using JSONPath syntax. For example:  

```code
$.Agent.FirstName
```

#### Play Prompt flow block

This prompt speask or dispalys a prompt to the customer. JSONPath can be integrated into the play prompt flow block message:  

```code
You are being transfered to $.Agent.FirstName who can help you further.
```

To avoid prompting with empty values, use the _Check contact attribute_ flow.  

### Encrpyt sensitive customer input

Some information should be encrypted, to comply with regulatory bodies like the Payment Card Industry (PCI). The _Store Customer Input_ flowblock can use public key cryptography to encrypt data. The public key is configured within the Amazon Connect instance. The Store Customer Input block uses an X.509 certificate signed by the private key to prove it has the right to use the public key.  

### Secure IVR

Secure IVR uses multi-factor authentication to verify a callers identity, and allow encryption of customer data. This allows IVR to service the customer without the use of an agent.  

## External Data Sources

* Exploure using data from Amazon Lex and Amazon Connect Customer Profiles as contact attributes.
* Explore using contact attributes for integrations through Lambda functions.

### Lesson introduction

Data from external sources can help customize the customer journey to meet contact expectations and business needs.  

### Get customer input block

This block prompts the customer to enter a number on a touch-tone phone corresponding to the numbers listed in the prompt. This input is used to branch appropriatly.  

* Supports voice, chat, task channels. Integratoin with Amazon Lex. One chatbot works for voice and messaging.
* Configure timeout settings for length of wait.
* Stores custom input keys.

#### Get customer input block with Amazon Lex

The _Get customer input_ block can collect customer input using Amazon Lex. Customers can go through an exchange with Lex and then return to the flow with contact attributes from the Lex exchange.  

#### Data available from Amazon Lex

Amazon Lex returns information including:

* _Intent name:_ This is the user intent
* _Intent confidence score:_ This is the score Lex uses to establish its confidence in the customer's intent
* _Sentimental label and score:_ This is the value Lex assesses the customers sentiment to be. Values are POSITIVE, NEGATIVE, MIXED, and NEUTRAL
* _Session attributes:_ These attributes are passed to and from the Lex bot
* _Slots:_ Lex slots capture user data from their conversation.

### Customer Profiles block

The Customer Profiles block can create, retrieve, and update customer profile data. It identifies profiles using identifiers like phone numbers, emails, account IDs. Once retrieved, profile data can be mapped to contact attributes.  

#### Customer Profile data:

* _Profile metadata:_ basic demographic information (name, address, phone number, etc.)
* _Attributes:_ Custom fields. Can include _calculated attributes_ like paterns of behavior, customer value, past behaviors
* _Asset:_ items related to the profile, like products and their related information
* _Order:_ Order data like status, ID, cost
* _Case:_ Case ID, short description, date created, status, etc.

### Invoke AWS Lambda function block

This block allows flows to exchange data with external systems using AWS Lambdas. This could retrieve customer data, reset passwords, trigger emails. The lambda returns values as contact attributes. JSONPath can be used to access nested data.

More information about invoking Lambda functions from flows is located [here](https://docs.aws.amazon.com/connect/latest/adminguide/connect-lambda-functions.html#function-contact-flow)  

## Flow Design Best Practices

* Recognize best practices for implementing flows.
* Identify optimal ways to implement error handling in flows.

### Lesson introduction

More about the AWS Well-Architected Framework can be found [here](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc)  

This is a collection of recomended best practices aligned with the six pillars of the AWS Well-Architected Framework. They are:  

* Operational excellence
* Security
* Reliability
* Performance efficiency
* Cost optimization
* Sustainability

### Best practices

#### Modularized flows

Break functionality into logical sections. Combine sections to create modular flows. Logical sections improve flow managability.  

#### Taxonomy

Use standard naming conventions for all AWS services and attribute names. Do not name anything using spaces or special characters.  

#### Error handling

Ensure all errors route to a block that effectivley handes them or ends the contact in a manor that maintains customer trust.  

#### Permissions

Make sure Amazon Connect has appropriate permissions for all integration points.  

#### Data security

Only store data you need.  

#### Monitoring

Disable logging for segments where sensitive information is collected, to avoid storing this in CloudWatch logs. Otherwise, ensure logging in activated.  

#### Hours of operation and staffing

Ensure that the _Check hours of operation block_ and _Check staffing block_ are used to verify there are agents available to handle a call before routing a customer to a queue.  

Additional architectural guidance can be found [here](https://docs.aws.amazon.com/connect/latest/adminguide/architecture-guidance.html)  

### Error handling

Common errors:  

* Invalid user input
* Using dynamic contact attribute values that are not set
* Error from running Lambda functions

#### Handling errors best practices

Recomended patterns for catching and handling errors:  

_Continue past the error:_  

If the error is not serious, it may not be necessary to exit the current flow, or the error could change the route within the flow. In this pattern, the customer should be unaware of the error.  

_Gracefully inform the customer and continue:_  

Change to a flow branch that informs the customer of the error and continues the contact. Perhaps route the customer to a priority queue if there intent can not be addressed automatically due to the error.  

_Gracefully disconnect the customer:_  

For critical errors, it may make sense to end the flow and disconnect the customer. For example, if a queue is full the customer could hear a message like "We're sorry, all agents are busy at this time. Please try back later."  

