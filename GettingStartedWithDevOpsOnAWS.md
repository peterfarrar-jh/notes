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

#### AWS CodeCommit

#### AWS CodeBuild

#### AWS CodeDeploy





