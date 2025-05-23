# Deploying Serverless Applications

## Understanding Serverless Deployments

Serverless applications should be:

* Decoupled
* Stateless
* Use minimal code

### Introduction to serverless deployments

Deployment could be as simple as an API call.  
To insure code is successfully deployed:  

* The ability to audit changes. Cloudtrail can record events. Automated actions can alert to failed deployments.
* Ability to roll back or halt bad deployments.
* Deploying changes through a planned and automated process can increase successful deployments.

A successful deployment is a deplyment your customers don't notice.  

### Serverfull or serverless development

#### Serverfull

Deploy code changes to multiple servers.  

#### Serverless

* AWS CloudFormation
* AWS Cloud Development Kit (AWS CDK)
* Terraform
* Serverless Framework

API calls can create or update function code.  

### Journey of a serverless developer

* Build and test code locally
* Need to deploy into a sandbox

AWS SAM is an extention of AWS Confirmation. SAM transforms shorthand syntax into CloudFormation syntax.  

#### SAM templates

Infrustructure as code: Define infrastructure in JSON or YAML templates. CloudFormation will interpret these and create resources accordingly. AWS Confirmation Service will roll back changes if any errors occur.  

In a SAM template, `Transform` and `Type: AWS::Serverless::Function` define commands that allow transformation of the template file into CloudFormation instructions.  

#### SAM CLI

* Tests code locally.
* Emulate Lambda environment.

Perform unit tests, debug, troubleshoot issues locally.  

Develop SAM template  

Use SAM CLI:

* SAM `package` command - creats a deployment package
* SAM `deploy` command - deploys template into a CloudFormation stack

## AWS SAM

An open source framework for building serverless appliactions.  

* APIs
* Databases
* Event source mappings
* Lambda functions

Uses shorthand syntax, then transforms this into CloudFormation syntax durring deployment.  

### SAM templates

* Creates CloudFormation templates using shorthand syntax
* Uses linfrastructure as code to define resources
* Will rollback if any errors are detected

### Example of a SAM template

```yaml
AWSTemplateFormationVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Resources:
  SAMDemoFunction:
    Type: AWS::Serverless::Function
      CodeUri: sam-demo/
      Handler: app.lambdaHandler
      Runtime: nodejs14.x
      Architectures:
        - x86_64
```

Types supported:  

* `AWS::Serverless::Api`
* `AWS::Serverless::Application`
* `AWS::Serverless::Function`
* `AWS::Serverless::LayerVersion`
* `AWS::Serverless::SimpleTable`

### Deploying SAM templates with the SAM CLI

1. Write code
2. Define resources in template file
3. Use SAM to emulate Lambda environment and perform local tests
4. Use SAM to create deployment package
5. Use SAM to deploy package

### Serverless Patterns Collection

The [Serverless Patterns Collection](https://serverlessland.com/patterns) is a repository of serverless examples integrating two or more AWS services using SAM or CDK. These can be used to simplify creation and configuration of AWS serverless applications.  

### Additional resources: documentation

* [AWS Well-Architected Framework – How Do You Implement Change?](https://wa.aws.amazon.com/wat.question.REL_8.en.html)
* [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
* [Monitoring and Troubleshooting Lambda Applications](https://docs.aws.amazon.com/lambda/latest/dg/troubleshooting.html)
* [AWS SAM and SAM CLI GiHub Reference Guide](https://github.com/awslabs/serverless-application-model)
* [AWS SAM Gradual Code Deployment](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/automating-updates-to-serverless-apps.html)
* [Working with Deployment Configurations in AWS CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-configurations.html)

### Additional resources: blog posts

* [Implementing Safe Lambda Deployments with CodeDeploy](https://aws.amazon.com/blogs/compute/implementing-safe-aws-lambda-deployments-with-aws-codedeploy/)

## Sharing Configuration Data

### Managing configuration data

* Connection strings
* Logging settings
* Output

#### Sharing configuration data in a serverless environment

Handling secrets is a big issue  

* Hard code in deployment package - Generally a bad idea.
* Store in environment variabes - Key/value pairs. Can be encrypted. Specific to a single Lambda.
* Load at runtime - Centralized location available to all Lambdas. Parameter store is hierarchical. Fine grained permissions through IAM. Adds cold start latency.

Best practice:  

Pull configuration data from Parameter Store and store it in a global variable. Use function code to check if you need to pull or update the parameter.  

Places to store configuration data:  

* AWS Systems Manager Parameter Store
* AWS Secrets Manager
* AWS AppConfig

### AWS Systems Manager Parameter Store

The AWS Systems Manager has a Parmeter Store that stores configuration data and secrets hierarchically.  

* Free, fully managed, centralized storeate system for configuration data and secret management.
* Data can be stored in plain text or encrypted with AWS KMS.
* Parameter Store tracks all parameter changes through versioning, making it easy to roll back to an earlier version.

### Additional resources: documentation

* [AWS Lambda Environment Variables](https://docs.aws.amazon.com/lambda/latest/dg/env_variables.html)
* [AWS Systems Manager FAQs](https://aws.amazon.com/systems-manager/faq/)
* [What Is AWS Secrets Manager?](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)

### Additional resources: blog posts

* [Sharing Secrets with Lambda Using Systems Manager Parameter Store](https://aws.amazon.com/blogs/compute/sharing-secrets-with-aws-lambda-using-aws-systems-manager-parameter-store/)

Additional resources: tutorials and samples

* [Parameter Store Walkthroughs](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-walk.html)

---

## Automating the Deployment Pipeline

### Safe and gradual deployments

When deploying code, it should not require a human to approve or test each piece. It also shouldn't immediately release it into production.  

### Deployment strategies

* _All-at-once deployment:_ Shift 100% of traffic to the new version.  
* _Canary deployment:_ Use traffic shifting to send a small percentage of traffic to the new version. When the new version is validated, shift all traffic to it.  
* _Linear deployment:_ Use traffic shicting to sene a small percentage of traffic to the new version. Over time, incrementally increase traffic untill 100% is going to the new version.  

Traffic shifting: Points alias to two different versions, sending a small portion to the new version. When it is clear that the new version is working properly, more or all traffic can be directed to it.  

* Pre-traffic hooks - Started before the alias can accept traffic
* Post-traffic hooks - Started after traffic shift
* Alarms - Helpful to trigger the rollback process
* Deployment preferences - Where you choose whether you want a canary, linear, or all-at-once deployment
* Hooks - Sanity checks to test and perform actions against your code

AWS SAM is the best way to build serverless applications. Configure CodeDeploy to manage deployment strategies.  

#### Lambda versions

The current version is called `$LATEST`. Each deploy creates a new immutable version so that it can be rolled back.  

#### Lambda aliases

An alias is a pointer to a specific version of a function. Default behavior is for an alias to point at one version.  

### Deployment preferences with AWS SAM

<div class="container">
  <style>
    table {
      margin: 0 auto;
      width: 80%
    }
    tr {
      color: #333;
    }
    tr:nth-child(even) {
      background-color: #ccc;
    }
    tr:nth-child(odd) {
      background-color: #eee;
    }
    td, th {
      padding: 1rem;
    }
  </style>
  <div class="table-wrapper">
    <table>
          <thead>
            <tr>
              <th>Deployment Preference Type</th>
              <th>Description</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Canary10Percent30Minutes</td>
              <td>Shifts 10 percent of traffic in the first increment. The remaining 90 percent is deployed 30 minutes later.</td>
            </tr>
            <tr>
              <td>Canary10Percent5Minutes</td>
              <td>Shifts 10 percent of traffic in the first increment. The remaining 90 percent is deployed 5 minutes later.</td>
            </tr>
            <tr>
              <td>Canary10Percent10Minutes</td>
              <td>Shifts 10 percent of traffic in the first increment. The remaining 90 percent is deployed 10 minutes later.</td>
            </tr>
            <tr>
              <td>Canary10Percent15Minutes</td>
              <td>Shifts 10 percent of traffic in the first increment. The remaining 90 percent is deployed 15 minutes later.</td>
            </tr>
            <tr>
              <td>Linear10PercentEvery10Minutes</td>
              <td>Shifts 10 percent of traffic every 10 minutes until all traffic is shifted.</td>
            </tr>
            <tr>
              <td>Linear10PercentEvery1Minute</td>
              <td>Shifts 10 percent of traffic every minute until all traffic is shifted.</td>
            </tr>
            <tr>
              <td>Linear10PercentEvery2Minutes</td>
              <td>Shifts 10 percent of traffic every 2 minutes until all traffic is shifted.</td>
            </tr>
            <tr>
              <td>Linear10PercentEvery3Minutes</td>
              <td>Shifts 10 percent of traffic every 3 minutes until all traffic is shifted.</td>
            </tr>
            <tr>
              <td>AllAtOnce</td>
              <td>Shifts all traffic to the updated Lambda functions at one time.</td>
            </tr>
          </tbody>
    </table>
  </div>
</div>

### Creating a deployment pipeline

A CI/CD pipeline helps automate steps and standardize quality checks when deploying software. AWS tools for pipelines:  

* AWS CodeCommit for Source
* AWS CodeBuild for Build and Test
* AWS CodeDeploy for Production
* AWS CodePipeline for fully managed continuous delivery

For more information see the [CI/CD on AWS](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/cicd-on-aws.html) whitepaper.  

### Automating your deployment pipeline

#### Source

* Check-in source code
* Peer review

#### Build

* Compile code
* Unit testing
* Style checker
* Create container images and deployment packages

#### Test

* Integration testing (with other systems)
* Load testing
* UI testing
* Security testing

#### Production

* Deployment to production environments
* Monitor code in production

Each stage should have its own AWS account  

### AWS SAM Pipelines

AWS SAM Pipelines provide templates for AWS CodePipeline, Jenkins, GitHub Actions, Bitbucket Pipelines, and GitLab CI/CD.  

AWS SAM Pipelines is composed of two commands:  

1. `sam pipeline bootstrap` - Designed for operators, this command creates the AWS resources and permissions required to deploy application artifacts from your code repository into your AWS environments. 
2. `sam pipeline init` - Designed for developers, this command generates a pipeline configuration file that your CI/CD system can use to deploy serverless applications using AWS SAM. 

`sam pipeline init --bootstrap` combines the two commands above.  

SAM produces a configuration file for the pipeline of choice.  

### Creating pipeline deployment resources

`sam pipeline init --bootstrap` is a guided process that creates a template file with the AWS resources needed to deploy code from a repository into an AWS environment.  

`sam deploy` will deploy the pipeline using the template file.  

[comment]: # (Review the video and follow up language. It lays out everything you need to know to get started building pipelines. Add summary steps below)  
