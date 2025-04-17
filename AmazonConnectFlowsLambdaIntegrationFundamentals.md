---
text: "AWS Skillbuilder"
title: "Amazon Connect Flows Lambda Integration Fundamentals"
author: "Peter Farrar"
date: 04/03/2025
description: "Learning basics on Amazon Connect Flows integration with Lambda"
---

# Amazon Connect Flows Lambda Integrations Fundamentals

## Introduction to Amazon Connect Flows and Lambda Integration

* Recognize the benefits of Amazon Connect flows and AWS Lambda Integration.
* Identify common use cases

### Lesson introduction

Lambda functions help Amazon Connect flows interact with other AWS services to customize the customer journey experience.  

### Benefits

Invoking lambda functions in a Connect flow lets organizations:

* _Reduce customer effort:_ Retrieve contact information from external sources to help predict intent.
* _Improve customer experience:_ Retrieve contact information from external sources to personalize the user experience.
* _Extend contact access:_ Introduce self-service capabilities, allowing customers to resolve issues outside of call center hours.
* _Improve security:_ Generate and use one-time passwords (OTP) to mitigate the risk of unauthorized access to sensitive data.
* _Streamlined operations:_ Lambdas can help with modularization, and allow changes in logic without modifying the Amazon Connect flow directly.
* _Seamless omnichannel transition:_ Lambdas can facilitate seamless transitions between different communication channels.
* _Increased revenue:_ Lambdas can help personalize sales opportunities within the call.

### High-level integration architecture

Through the _Invoke AWS Lambda function block_, flows can pass parameters to, and recive resulting data from, Lambda functions.  

#### Use case one

Customers with open cases still have to start with tier one CSRs. This uses time and resources, and creates a bad customer experience.  
Using Lambdas to access CRM based on incomming phone number, logic in the flow can identify if a customer has an open case, prompt the customer using their name, and route them to the correct agent team.  

#### Use case two

A business analyst notes that 20% of calls are repeat callers that want to pay a bill.  
A Lex bot is added to the flow to allow self-service. The Lex bot uses a Lambda call to process payment and return details, which are stored in contact attributes.  

#### Use case three

French speaking customers are regularly routed to English speaking agents, who then have to transfer them to the correct queue. This increases average hold time, and lowers customer satisfaction scores.  
A Lambda is used to retrieve the callers information, specifically their membership status and preferred language. This information is used to automatically route the customer to the correct queue for their preferred language.  

## Invoking Lambda Functions from Flows

* Explore a use case for demonstrating the input and response syntax of a Lambda function invocation
* Identify a test event format for a Lambda function invoked by flows

### Lesson introduction

Amazon Connect flows use a specific format to send input to a Lambda function and expect results in a specific format.  

### Invoking a Lambda function

A flow can use the _Invoke AWS Lambda function block_ to pass information to a Lambda function. The input data is JSON, as is the repsonse. The function is invoked syncronously, and a timeout is set to limit the length of time the flow will wait for a response. This timeout can be configured for up to eight seconds.  

#### Use case

The most common use case when invoking Lambda functions is to retrieve data from an external source (like a CRM). The response can be used for routing and personalization.  

#### Architecture

The flow implements the _Invoke AWS Lambda function block_ and passes it the caller's phone number. The Lambda function connects to the CRM and queries using the phone number. Any customer data returned is formatted in JSON and returned to the flow.  

### Exploring the data exchange between flows and the Lambda function

The _Invoke AWS Lambda function block_ returns with "prescriptive flow response format syntax." If there is an error, or the response format is incorrect, the flow continues using the **Error** branch. Otherwise, the flow continues using the **Success** branch.  

#### Understanding the Lambda function input parameters

Additional information can be passed using the _Function input parameters_ section of the _Invoke AWS Lambda function block_.  

The event object looks like this:  
```json
{
    "Name": "ContactFlowEvent",
    "Details": {
        "ContactData": {},
        "Parameters": {
            "customer-phone-number": "+14165550011"
        }
    }
}
```

The `ContactFlowEvent` may contain additional contact interaction details, like custom attributes, the communication channel or contact phone number.  

#### Use case one

The _Invoke AWS Lambda function block_ is configured to call the `AccountFunction` Lambda. _Function Input parameters_ set the `Destination key` to "operation" and "Set manually" to the value "checkBalance".  

Here is some nonsensical javascript pretending to demonstrate Lambda code:  

```javascript
exports.handler = function(event, context, callback) {
  let parameters = event['Details']['Parameters'];
  let channel = event['Details']['ContactData']['Channel'];

  switch(parameters.operation) {
    case "checkBalance":
      checkBalance(channel);
      break;
    case "lockCard":
      lockCard(channel);
      break;
    case "fundsTransfer":
     fundsTransfer(channel);
     break;
    default:
  }

  const response = {
    "Result" : "Success",
    "Savings" : balance
  }

  callback(null,response);
};
```

#### Understanding the Lambda function repsonse

The _Response validation_ of the _Invoke AWS Lambda function block_ can be configured to expect either a JSON response or a STRING_MAP response (which is a shallow JSON set of key value pairs where the value is a string). The response in the example code above is an example of a STRING_MAP.  

A JSON response might look like this:  

```json
{
 "Result" : "Success",
    "Balance" : {
        "Savings": "$3018.19",
        "Checking": "$577.42"
    }
}
```

### Testing your Lambda function

The Lambda console provides test functionality, including a connect-contact-flow-event JSON template for creating input.  

## Best Practicews and Key Considerations

* Recognize the benefits of environment variables.
* Recognize the benefits of using a Lambda alias in flows.

### Lesson introduction

Designing functions that are strightforward to deploy and maintain reduces the risk of negatively affecting production environments.  

### Using environment variables

Loosely couple Lambdas with resources like DynamoDB and CRMs by storing their identifiers as environment variables. This also allows reuse across environments. 

Here is an example of using environemnt variables in a Lambda:  

```python
import boto3

s3 = boto3.client("s3")
connect = boto3.client("connect")
instance_id = os.environ['INSTANCE_ID']
bucket = os.environ['BUCKET_NAME']
num_retries = int(os.environ['NUM_RETRIES'])
```

### Using Lambda versions and aliases

By default, Amazon Connect uses the most current version of a Lambda. But by using the _Set manually_ option in the _Function ARN_ settings of the _Invoke AWS Lambda function block_, and using the ARN of a specific Lambda version (a Lambda pointer), a specific version of a Lambda can be used instead. Lambda development and testing can move forward without interupting the flow. And the pointer can be updated when the Lambda is ready to be released.  
Using weighted aliases, traffic can slowly be routed from the old alias to the new.  

Amazon Connect instances need explicit permission to invoke Lambda aliases. Permission can be granted by administrators like this:  

```bash
aws lambda add-permission --function-name <LAMBDA_ARN>:<ALIAS> --statement-id <UNIQUE_CODE> --action lambda:InvokeFunction --principal connect.amazonaws.com --source-account <ACCOUNT_ID> --source-arn <CONNECT_INSTANCE_ARN>
```

### AWS Region selection

Organizations may choose to host their Lambdas in a different region than the Amazon Connect instance.  

#### Permission access configuration

When the Lambdas and the Amazon Connect instance are in the same region, admins can grant Amazon Connect permission to access the Lambda using the AWS Management Console.  

When the Lambda and the Amazon Connect instnace are in different regions, admins can grant Amazon Connect permission to access the Lambda by doing the following:  

* Associate the lambda function with the Amazon Connect instance by using the AssociateLambdaFunction API. More information is available [here](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociateLambdaFunction.html).
* Attach a resource-based AWS IAM policy to the Lambda. The policy must contain a resource permission tag specifying **connect.amazonaws.com** as the principal and the ARN of the Amazon Connect instance.  

Sample IAM policy for the above:  

```json
{
  "Version": "2012-10-17",
  "Id": "default",
  "Statement": [
    {
      "Sid": "connect-lambda-allow-listing",
      "Effect": "Allow",
      "Principal": {
        "Service": "connect.amazonaws.com"
      },
      "Action": "lambda:InvokeFunction",
      "Resource": "arn:aws:lambda:us-east-1:111122223333:function:FuncName",
      "Condition": {
        "ArnLike": {
          "AWS:SourceArn": "arn:aws:connect:us-east-1:111122223333:instan..."
        }
      }
    }
  ]
}
```

More information on resource-based IAM policies can be found [here](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html),  

