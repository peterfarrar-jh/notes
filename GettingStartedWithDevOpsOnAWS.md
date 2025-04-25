---
text: "AWS Skillbuilder"
title: "Getting Started with DevOps on AWS v01.04.00"
author: "Peter Farrar"
date: 04/17/2025
description: "Basic concepts of AWS DevOps"
---

# Getting Started with DevOps on AWS

## Introduction to DevOps

* Describe challenges associated with traditional software development practices
* List the benefits of implementing DevOps

### What is DevOps?

DevOps is a combination of cultural philosophies, practices, and tools that increase an organization's ability to deliver applications and services at a high velocity.  

* Cultural philosophies for removing barriers and sharing end-to-end responsibility
* Processes developed for speed and quality that streamline the way people work
* Tools that align with processes and automate repeatable tasks, making the release process more efficient and the application  more reliable

### Problems with Traditional Development Practices

**Waterfall development projects** are slow, not iterative, resistant to change, and have long release cycles.

* Requirements are rigig, set at project start, and will likely not change
* Development phases are siloed, each starting after the previous phase has ended. Each phase is supported by highly specialized teams.
* Hand offs from one phase to another are long, often requiring teams to switch tools and spend time clarifyin gincomplete or ambiguouse information
* Testin and security come after implementation, making corrective actions responsive and expensive

**Monolithic applications** are hard to update and deploy.

* Developed and deployed as a unit. Changes require the entire application be redeployed
* Tightly coupling means that for large applications, maintenance becomes difficult. Developers need to understand much or all of the application.
* Use a single development stack, making a change in technology difficult and expensive

**Manual processes** throughout the application lifecycle are slow, inconsistent, and error-prone.

### Why DevOps?

#### Proven success

Teams that adopt DevOps have shorter delivery cycles, decreased change failure rates, and improved performance.  

#### The benefits of DevOps

##### Agility

* Build competitive advantage by anticipating market needs and delivering value quickly
* Monitor application and support development strategies with real data
* Development practices that allow teams to move at high velocity and continuously deliver controlled, small updates as needed

##### Rapid delivery

Core principles of DevOps are Continuous Integration and Continuous Delivery (CI/CD), rapid feedback loops, continuous monitoring, making agile development quicker and more efficient.  

Automation ensures smooth lifecycle development cycle flow, and provides  quick and consistent reviews.  

##### Reliability

* Ensure quality application updates and infrastructure changes
* Use CI/CD to test that each change is functional and safe
* Use monitoring and observing practices to help stay informed of realtime performance

##### Scale

AWS DevOps tools automate tasks and help manage complex environments at scale.  

Simplified provisioning helps engineers move at high-velocity and take advantage of flexible compute resources.

##### Improved collaboration

DevOps cultural model emphasizes values like ownership and accountability. Developers and operation teams share responsibilities and combine workflows, reducing inefficiencies and saving time.  

##### Security

The DevOps model uses fine-grained controls and configuration managment techniques to help move quickly, while retianing and ensuring compliance policies.  

### Why do some teams initially resist adopting DevOps

Risistance to change is natura, as it disrupts the way teams work and interact. Understanding the value of DevOps, and setting realistic expectations will help with adoption.  

---

## DevOps methodology

* Discuss the challenges involved in adopting a DevOps culture and describe possible solutions
* Identify automation opportunities in developing and maintaining applications
* Describe the benefits of decoupling services or components
* Define observability and describe its importance to DevOps
* Explain why security is important in every phase of the pipeline
* Explain how AWS integrates with third-party tools for automated code delivery and deployments

### DevOps Culture

There are seven core principles that help to achieve a DevOps culture:  

#### Create a highly collaborative environment

DevOps breaks down silos. Operations and development align goals and take ownership of the entire lifecycle and optimize the productivity of developers and reliability of operations.  

This increases visibility, enabling continuous improvement, delivering on business goals. It also encourages collabroation that creates a trust culture, and transfers knowledge and best practices across the organization.  

#### Automate when possible

Automating repeatable tasks allows teams to focus on innovation while provideing rapid development, testing, and deployment. Areas of automation include, among other things, code integrations, code reviews, testing, security, deployment, and monitoring.  

#### Focus on customer needs

Using microservices and feedback loops to stay in touch with customers, development can quickly change direction to deliver software that meets customer needs.  

Automation and streamlined processes allow requests to be delivered faster, keeping customer satisfaction high.  

#### Develop small and release often

Small, loosely coupled components allow for frequent small releases.  

#### Include security at evey phase

Security should be iterative, incremental, automated and embedded in every phase of the application lifecycle. This allows identification and resolution of potential vulnerabilities before they reach production.  

#### Continuously experiment and learn

Learning and mentoring are encouraged. With innovation there is going to be failure. Leadership accepts this view failure as a learning opportunity.  

DevOps makes it easy to spin up new environments to try out new ideas. And just as easy to spin them down.  

#### Continuously improve

Monitoring tools can help gather metrics to evaluate processes and tools, and continuously improve their processes and throughput.  

---

### DevOps Practices

DevOps culture leand to practices that are streamlined and constantly improving the devlopment lifecycle, delivering frequent updates and maintaining stability.  

#### Communication and collaboration

Communication and transparency of information allow cross-functional teams to take ownership and collectively consider the project needs. While collaborating towards their common goal, they build empathy, partnership, and trust.  

DevOps tools and automation support conditions required for good communication and collaboration.  

#### Monitoring and observability

An observable system is one that generates data from all resources, applications, and services sufficient to gain insites into application and infrastructure perfomance. Monitoring allows the team to understand these insites, identify opportunites, and make predicitions. Monitoring and observability provide a means of evaluating and improving performance.   

#### Continuous integration (CI)

Continuous integration, the practice of regularly merging code changes into the central depository, helps to find and address bugs more quickly, improves software quality, and reduces the time required to validate and release updates.  

#### Continuous delivery/continuous development (CD)

Continuous delivery is a practice where each code change (see CI above) kicks off an automated process to build, test, and deploy to a non-production environment. The result is a deployment-ready artiface. Manual approval is required before pushing to production.  

#### Microservices architecture

Microservice architecture is a design approach to building applications out of loosely coupled services interacting through well defined APIs. Implementation details of each service can be separate from other services. They allow rapid development and independent deployments.  

#### Infrastructure as code

Infrastructure as code (IaC) is the practice of managing and provisioning infrustructure using code and configuration files. It allows for versioning and continuous integration. Using APIs, developers and admins can programatically provision at scale, update with latest patches, easily duplicate environments, and roll them back to pervious versions.  

_**A CI/CD pipeline**_ is a good example of how DevOps teams use tools to streamline workflows and standardize practices. Pipelines are a serices of stages that move code from source to deployment.  

#### Code

Develop code in the chosen language. Merge code to initiate a peer review.

#### Build

* Compile code (if necessary)
* Check code styles and standards
* Analyze code complexity and maintainability
* Validate dependencies
* Creaete container images
* Run unit tests

#### Test

Common testing practices:

* Functional testing
* Integration testing
* Regression testing
* Acceptance testing
* Load testing
* Security testing

#### Release

Prepare and package a new version of the code

#### Deploy

Deploy the release to targeted environments (test, staging, alpha, beta, production).

#### Monitor

Monitoring the application in production allows for quick detection of bugs and errors.

---

### DevOps Tools

AWS DevOps tools can integrate with third party tools like GitHub and Jenkins.  

General category of tools that might be needed to support DevOps:  

#### Cloud

Cloud platforms and cloud computing resources provide an array of technologies to support application development.  

#### Development

Collaborative development requires tools to help teams develop and deliver faster.  

* IDEs: AWS Cloud9, IntelliJ, Eclipse, VS Code
* SDKs: AWS SDK, iPhone SDK
* Source code repositories: GitHub, AWS CodeCommit

#### CI/CD

CI/CD tools bring seamless automation with compliance checks, testing snd source control.  

* Build tools: Jenkins, Travis CI, AWS CodeBuild
* Source control tools, repositories: Git, AWS CodeCommit
* Deployment tools: AWS CodeDeploy, AWS CloudFormation
* Pipeline automation tools: AWS CodePipeline, Jenkins, GitLab

#### Infrastructure automation

Use templates to deploy services, permission, dependencies, and more.  

* Infrastructure automation tools: AWS CloudFormation, Terraform, AWS Elastic Beanstalk
* Configuration management tools: Chef, Puppet, AWS OpsWorks

#### Containers and serverless

Containers and serverless compute services allow developers to focus on applications, and not implementation details.  

Containers package code, configurations, dependeencies with an operating system and are excellent for running microservices. Containers do require container orchestration for managing interactions.  

Serverless compute services run code, while infrastructure overhead is managed by the cloud provider.  

* Serverless services: AWS Lambda, AWS Fargate
* Container Services:
  * Runtimes: Docker, Containerd
  * Orchestratoin: Amazon Elastic Container Service (Amazon ECS), Kubernetes, Amazon Elastic Kubernetes Service (Amazon EKS)

#### Monitoring and observability

Examples: AWS X-Ray, Amazon CloudWatch, AWS Config, AWS CloudTrail

---

## Amazon's DevOps transformation

* Describe the transition from a monolithic approach to a microservices architecture
* Describe the benefits of smaller, autonomous teams

### Decompose for agility

Amazon changed organizational structure and the monolithic architechure of their application. Implementing SOA (aka micorservices) with backwards compatability allowed them to split into small crossfunctional teams called _Two Pizzas_.  

### Use tools and automate

_Two pizza_ teams began to leverage tools for best practice through automation. They Introduced templates, and metrics for monitoring... Security policies stopped deployment of known vulnerabilities. Testing was integrated and CI/CD was realized.  

### Transform the culture

DevOps transformation is an incremental process over time. Individuals have to change the way they think about their work. Value is placed on innovation, improvement, and business results supported by metrics. Teams at Amazon went from silos to cross-functional. Education and collaboration became the norm.  

Small teams, ownership, talent in-sourcine, bottom-up planning, communication, collaboration, automation, and continuous improvement through innovation and monitoring have become the driving force at Amazon.  

---

## AWS DevOps tools

* List the AWS services available to implement a successful DevOps methodology
* Identify the AWS services used to automate the continuous integration and continuous deliver process

Remember, DevOps solutions might comprise AWS services and third-party solutions. Amazon tools for devops:  

[Developer Tools] AWS Cloud9, Amazon tools and SDKs, AWS Cloud Development Kit (AWS CDK)  
⇩  
[Source Control] AWS CodeCommit  
⇩  
[Packge Creation] AWS CodeBuild  
⇩  
[Deployment Automation] AWS CodeDeploy  
⇩  
[Collect Metrics] AWS X-Ray  
⇩  
[Monitor Metrics] Amazon CloudWatch  
⇩  
[Pipeline] AWS CodePipeline

#### AWS CodePipeline

A continuous delivery service to model, visualize, and automate steps in the software release process.  

* Capture and visualize pipelines, run them, view real-time status, retry failed actoins.
* Automating the release process eliminates human error, speeds up deliver, and improves the quality of releases.
* Establish a consistent release process.
* Incorporate source, build, and deploy tools.
* View pipeline history details.
* Integrate with thrid-party and AWS tools to build, test, and deploy code changes.

##### Monitoring

Pipelines can be monitored in the AWS CodePipeline console, the CLI, using Amazon EventBridge, or AWS CloudTrail.  

##### Security

CodePipeline supports resource-level permissions. For more information see [Security in AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/security.html).  

##### How it works

Break the release process into stages. Each state has a number of actions to perform. Actions are tasks that run either in sequence or parallel. Each action is associated with a service provider that runs the action, or user intervention. Service providers can be AWS services like CodeBuild, Amazon S3, AWS Lambda, AWS CloudFormation, or third party services like Jinkins, and TeamCity.  

Action types:  

* Source (where source is stored)
* Build (how to build the application)
* Test (how to test the application)
* Deploy (how to deploy the application)
* Approval (manual approval and notifications)
* Invoke (Invoke a custom function)

A simple pipeline might consist of three stages:  

1. Source: Retrieve the source code from a repo (GitHub)
2. Build: Compile or transpile the source (CodeBuild)
3. Deploy: Deploy the application (CodeDeploy) 

#### AWS CodeCommit

CodeCommit is a git repository.

##### Why use?

* Eliminate administrative overhead of managing hardware.
* Collaborate with team using git commands.
* Improve your existing workflow by integrating CodeCommit with other AWS services, IDEs, and third-party software.

##### Monitoring

Create notifications and trigger actions based on events in source control.  

##### Security

Security is managed with policies and user accounts. Read more about Security in [AWS CodeCommit](https://docs.aws.amazon.com/codecommit/latest/userguide/security.html).  

##### How it works

It works just like git.  

#### AWS CodeBuild

A fully managed build service. It automatically compiles code, runs tests, and produces software packages.  

##### Why use?

* Eliminates the need to set up, patch, update, and manage your own build server.
* Automatically compiles sousrce code, runs tests, builds artifacts.
* Process multiple builds concurrently.
* Leverage preconfigured build environments (Python, NodeJS, Go, etc.). Or create custom build environments using Docker.
* Pull source code from CodeCommit, Amazon S3, GitHub, GitHub Enterprise, and Bitbucket.
* Integrate with Jenkins.

##### Monitoring

Monitor the build using the CodeBuild console, CloudWatch Logs and other ways.  

##### Security

Build artifacts are encrypted and access is controlled by resource level permissions in AWS IAM policies. Read more in [Security in AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/security.html).  

##### How it works

Uses a build project to create a new build environment in a docker container for each build.  

1. Uses build project to run build. Build projects contain information like source repo location, runtime environment, build command, and where to store output. CodeBuild can be accessed through the CodeBuild console, or by using AWS CLI, AWS SDKs, or CodePipeline.
2. Uses the build project to build an environemnt.
3. Downloads the code and uses the buildspec file to run a build. Buildspec is a collection of build commands that install tools, run tests, packages the code.
4. Outpput is uploaded to an S3 bucket.
5. Build output is streamed to the service console and CloudWatch logs.
6. Monitor the progress through CloudWatch or other services.

#### AWS CodeDeploy

A managed service that automates deployments.  

##### Why use?

* Deploys server, serverless, and container applications.
* Automates deployment.
* Deploys to a variety of copute platforms: AWS Lambda, Amazon ECS, Amazon EC2, and on prem.
* Concurrently deploy one or multiple instances.
* Minimize downtime. CodeDeploy can handle traffic-shifts from version to version.
* Automatically stop and roll back from an unsuccessful deployment.

##### Monitoring

Tools like CloudWatch alarms and CodeDeploy console for monitoring.  

##### Security

Read about Security in AWS [CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/security.html).  

##### How it works

CodeDeploy needs to know which files to copy, what scripts to run, and where to deploy to.  

* Code
  * Identify the correct version of the code
  * Provide an application specification file (AppSpec file) in the project root.
  * The AppSpec file specifies where to copy the code and how to get it started.
* Deployment group
  * Specifies the target environment, specific to the target compute platform.
  * Can have more than one deployment groups.
  * Security needs to be assigned allowing the environmnet to communicate with CodeDeploy.
  * For EC2 and on-prem, a CodeDeploy agent is required.
* Deployment configuration
  * A set of rules and success and failure conditions used durring deployment.

### Additional services you should know about

#### Integrated development environment (IDE) services

* _AWS Cloud9_ is a cloud based IDE.

#### Infrastructure management services

* _AWS CloudFormation_ is an IaC service. that uses templates to describe the resources and dependencies needed, allowing quick, consistent provisioning and management.
* _AWS OpsWorks_ provides managemed instances of Chef and Puppet to help automate server configuration and deployment.

#### Containers and serverless services

* _AWS Lambda_ is a serverless compute service that invokes code when it's needed. It can also help customize the CI/CD pipeline.
* _Amazon Elastic Container service (Amazon ECS)_ is a container management service for Docker containers.

#### Monitoring services

* _AWS X-Ray_ is a distributed tracing system that helps analyze and debug distributed applications.
* _Amazon CloudWatch_ is a monitoring and management service that provides actionable insites and information for infrastructure resources.
* _AWS Config_ continuously monitors and records resource configurations and enables automated evaluation of them.
* _AWS CloudTrail_ logs, monitors, and retains account activity related to actions across the infrastructure. It can be used for compliance, auditing, to detect unusual behavior, and more.

## Demo: Create and Control a CI/CD Pipeline

### Demo high-level overview

Steps completed before Demo:  

* Required infrastructure has been provisioned into two AWS Regions
* An appspec.yml file and supporting scripts have been added to the repo
* A Lambda function that checks text on a webpage has beed created

Durring the demo:  

* Review of provisioned infrustructure with template file
* AWS CodeCommit configuration to hold code, and to start the pipeline with every code change
* AWS CodeDeploy configuration with deployment Region specifics to install the application on the infrastrucure
* AWS CodePipeline is used to create a two stage pipeline to deploy a simple web app to Region 1. Two new stages are added to deploy to Region 2, with a manual approval. Finally a Lambda is used to replace the manual approval with an automated one.


