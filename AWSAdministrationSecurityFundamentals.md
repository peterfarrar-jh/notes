---
text: "LinkedIn Learning"
title: "AWS Administration: Security Fundamentals"
author: "Peter Farrar"
date: 03/31/2025
description: "Fundamentals of AWS security"
---

# AWS Administration: Security Fundamentals

## Introduction

### Fundamentals of AWS security

This course will cover:
* Compute
* Networking
* Storage

As well as
* IAM Users
* Groups
* Roles

### What you should know

What you should have:
* Interest in AWS cloud security
* Basic knowledge of the public cloud would be helpful

## 1. The AWS Account

### Understanding your AWS account

* Your AWS account proides you access to AWS could services hosted in AWS regions around the world
* Your AWS account is a container
* Colud services from any AWS region can be hosted in the AWS account container
* Within your AWS account, you create admin users and groups of administrator types (admin, dev)
* IAM users and groups are contained within each individual AWS account
* IAM stands for Identity and Access Management

#### Root Account

* Each AWS account has a root administrator account
* It has no restrictions and cannot be controlled
* Protect by MFA and "forgetting" password

#### Root Account Tasks
* Set up account billing

* Submit a reverse DNS request
* Transfer domain registration
* Changing root account details
* Changing AWS support plan
* Create a CloudFront key pair
* Close AWS account

If your current AWS login is an email address, you are using the root account.  

#### AWS Account Design

Multiple locations, multiple accounts, single accounts, different environments (dev, test, prod)  

To determine how to create accounts, consider _Locations_ and _Requirements_  

#### management through Governance

Specific accounts for different resources?  

#### AWS Organizations

* Consolidate multiple AWS accounts
* All accounts are centrally managed
* Group accounts into organizational units (OUs)
* Granular control over all accounts using service control policies

How many accounts do I need? Do I want central management of my accounts? Is it a good idea?  

Start with a Management Account.  
Then create organizational units, like dev, test, prod.  
Then align specific developer and administrator accounts that work on specific projects.  
Then consider accounts for each resource you'll use (especially for larger organizations).  
Specific policies are also created for each OU.  

#### AWS Control Tower

* Manage and govern AWS Organizations
* Automate AWS account deployment and configuration
* Maintain compliance and governance across AWS Organizations
* Landing zone - enterprise container
* Controls - governance using guardrails

#### Landing Zone

Management account manages all the accounts in the tree  
Logging of all activity  
suggested sandbox OU for development

#### Considerations

* An AWS account is self-contained
* AWS accounts can be managed in a tree - AWS Organizations
* AWS Control Tower allows you to centrally control and govern AWS Organizations accounts
* Remember the root user

### AWS regions and edge locations

#### Global Infrastructure Design

* AWS infrastructure follows the AWS Well-Architected Framework best practices
  * Security
  * Reliability
  * Performance efficiency
* AWS infrastructure is deployed worldwide in regions
* Regions are divided into availability zones (AZs)
* Edge services sit outside of AWS regions

#### AWS Regions

Regions are independent and separate from eachother.  
Regions contain availability zones for highly available cloud services.  

#### Choosing an AWS Region

Data Security  
Data is always stored in multiple locations

Data Residency  
Data may have to be stored in a give location by law  

Compliance  
Industry rules and regulations  

#### Availability Zones

* Each availability zone contains at least one data center for customer workloads
* Each availability zone has inexpensive low-latency nework connectivity to the other availability zones in the same region
* EC2 instances are deployed in multiple subnets in multiple availability zones (web, app, database)

#### Core AWS Services

Compute  
Networking  
Storage  

A region deploys EC2 instance and a DB instance  
Can be placed in one availibility zone or two or three zones  
Pay for reliability/failover/security  

#### Failover Possibilities with AZs

Two availability Zones with an Elastic Load Balancer "fronting" the application.  

#### Regional Services Design

Generic services are available in any region:  
* RDS
* DynamoDB
* Elastic File System
* Elastic Load Balancing
* S3
* S3 Glacier

#### Services at the Edge

Services outside of the regions.  
_CloudFront (CDN)_ - Caches static and dynamic data records  
_Route 53 (DNS)_ - Delvers user to the closest edge location  
_WAF (Firewall)_ - Filters incoming public traffic at the edge  

#### Edge Locations

Hundreds of locations around the world.  

* Amazon CloudFront is a content devivery network (CDN)
* Speeds up distribution of static and dynamic content to users
* CloudFront caches content using edge locations
* Requested content is routed to the edge location that provides the best possible performance

#### CloudFront (CDN)

Without cloudfront, everyone would need to connect to the same S3 bucket. With cloudfront users only go to the edge location, where the edge location has pulled the data for all users in that proximity.  

#### Considerations

* AWS regions contain regional cloud services
* Each AWS region has at lease three AZs
* AZs provide high availability and failover possibilities for applications
* Edge locations cache data closer to the end user

Performance, security, reliability  

## 2. AWS Cloud Services and Security

### IAM accont security overview

#### Security Service for Securing Access

* IAM controls AWS account security
* Identification before access to AWS cloud services
* Each AWS account has separate IAM users and IAM groups
* AWS root accounts are not controlled by IAM

#### Identity and Access Magagement

* Use IAM user accounts for enterprise administrators
* Use multifactor authentication(MFA) to secure all user account logins
* Limit the use of the root user account
* Use IAM role for daily admin tasks

#### IAM Security Tools

* Security credentials - manage credentials, MFA, and access keys
* Access Analyzer - review access by external identities
* Account settings - password policy
* Access advisor - service permissions and access times
* Credential report - AWS account users and status of their credentials

#### Managing Access

Use IAM to grant permissions.  
Control who can create,configure, and delete.  
IAM activity is logged in AWS CloudTrail.  

#### Auditing IAM Users

* AWS CloudTrail logging services trackcredentials and access
* Enable AWS Config and set acceptable levels of compliance using managed and custom rules

#### Monitoring IAM Users

* AWS CouldTrail tracks all authentication
* Integrate AWS CloudTrail activity with AWS CouldWatch alarms
  * CloudWatch alarms for authentication issues
  * CloudWatch alarms when root user logs in

#### Considerations

* IAMmanages access to AWS could services
* MFA should be enabled on all IAM accounts
* AWS CloudTrail tracks all authentications
* AWS CloudWatch is the build-in monitoring utility

### EC2 instance security overview

#### Three-Tier Workload

Private Subnets to host application servers.  
Hosted in a VPC, which spans the chosen AZs.  
Access from the Internet goes through the Loadbalancer.  
No direct access to the servers.  
At least two copies of data.  
Internet gateway provides access to the VPC.  
VGW provides access to the application stack.  
NAT Gateway service provides indirect access to the internet for services that need it (for updates, etc.).  

#### Security Group

* Security groups are described as "virtual firewalls" protecting EC2 instances
* Security groups contain "allout rules" that control inbound and outbound traffic
* Separate allow rules can be defined for both inbound and outbound traffic

#### Security Group Design

Example rules:  
Bastion Host login might be on port 22, and only allows access to Web servers.  
Application access users via the end user is to the load balancer, and only accepts traffic on port 443, and are delivered to the webserver (8080) and the web server can only access the SQL server.  

#### Monitoring Workloads

* Monitor system and instance status checks
* Amazon CloudWatch metrics and alarms

CloudWatch can monitor EC2 instances for metrics. CPU load, Disk I/O, and network I/O are collected every five minutes.  

Or enable detaile dmonitoring  

Alarms and automated responses can be triggered based on these metrics.  

#### Launch Templates

Because there are so many options, it's a good idea to use a template, filling in details.  

#### AMI Components

The image has permissions, boot volumes, additional volumes, network adaptters, custom tags and region specifics  

EC2 Image Builder:  

* Automate the creation, maintenance, and deploymnet of Linux/Windows/Docker images  
* Images can be updated on an automated schedule  
* Define security settings to harden images  
* Run AWS-provided and custom tests before finalization  

#### EC2 Instance Protection Goals

* Define the level of access required (web, application, database)
* Ensure EC2 instances are protected against unauthroized access
* Scan for malware using GuardDuty on-demand scans

#### EC2 Administrative Tools

* Automate deployments using CloudFormation or third-party utilites such as Terraform
* Automate patch management using AS Systems Manager
* Amazon Inspector - identify vulnerabilities in operating systmes and installed applications  

#### Considerations

* Security group design for access control
* Monitor workload with CloudWwatch metrics
* Launch templates help manage EC2 instance deployment
* Manage AMI updates using the EC2 Image Builder

### Demo: EC2 instance security overview

Start with the VPC  
VPC > Your VPCs  
VPC and more  

What region do we want to operate in?  

How many AZs? At least two.  

Public subnets - load balancer

Private subnets - Web, application, DB servers  

> He chose 2 public subnets and 4 private subnets  

Nat gateways  

> originally chose '1 per AZ' but changed it to 'None' to save on costs  

VPC endpoint  

> None  

On the right side is a view of what will be build based on the choices on the left side.  

Click 'Create my VPC'  

For a web server, head to EC2 console.  
Creating a virtual server.  

To launch an instance, give it a name, pick an image (AMI) and size, a key pair for authentication, and choose the VPC and (private) subnet.  
Security group was added automatically.  

Click 'Launch instance'  

Note 'Launch Templates' option  

### Data security overview

#### Privacy FAQ

* Access - customers retain complete control of data stored on AWS
* Storage - customers choose the AWS region where content is stored
* Security - customers (mostly) choose how content is stored and encrypted
* Amazon S3 and Glacier automatically encrypt objects at rest

#### Access toData

* Infrastructure and storage services are supplied by AWS
* Customer managees data access
* Customer manages data protection

#### Data Management

* Redundancy and Durability  
* Data Encryption 
* Monitoring  

#### Redundancy and Durability

* Data records are stored in multiple availability zones
  * S3 Buckets
  * EBS volumes and snapshots
  * Shared storage (FSx for Windows File Server, EFS, RDS synchronous replication)

#### Data Encryption

* S3 buckets and S3 Glacier vaults are automatically encrypted
* RDS databaseshave encryption choices
* EBS volumes can be encrypted
* Shared storage (EFS and FSx) supports AWS 256-bit encryption

#### Data Protection Options

* Monitor S3 buckets with Amazon Macie
* Amazon S3 Glacier Vault Lock and Amazon S3 Object Lock provide mandatory access control
* Amazon RDS with AWS Backup provides point-in-time recovery (PITR)
* Automate EBS snapshots with Amazon Data Lifecycle Manager

#### Data Protection Controls

* Default EC2 encryption
* IAM policies per AWS account
* Resource tags for security control
* SCPs per AWS Organizations
* Encryption at rest
* Key Management Service (KMS) or CloudHSM for encryption policies
* Separate AWS accounts per sensitivity of data records
* AWS Config rules for control and remediation

#### Monitoring

* CouldTrail API calls can be monitored by AWS CloudWatch
* Use Amazon S3 Inventory to audit replication and encryption status
* Amazon Macie - compliance through detection
* Amazon GuardDuty to automatically detect suspicious Amazon S3 read activity
* Configure S3 and RDS access logs

#### Considerations

* Data storage on AWS is replicated data storage
* All data services can be encrypted

### Demo: AWS data security overview

Elastic Block Store > Volumes  
Select a volume for details  
Is it encrypted? Do you want that?  
EC2 Dashboard > Data protection and security (right hand side)  
There is an option for EBS encryption (currently dissabled). Can change settings using the Manage button.  

Can back up volue using snapshot 'create a snapshot' button.  
How many snapshots you take depends on what kind of updates are occuring.  

Lifecycle manager automates creation, retention, copy and deletion of snapshots and AIMs. It lets you copy snapshots to other regions in AWS.  

View all services  
Scroll down to storage

EFS > Customize  

RDS > Create database > Postgres
Multi AZ DB CLuster  

EC2 console: Service health  lists AZs in the region  

S3 buckets  
Create bucket  
Need unique name  
See naming rules  
Security options show bucket is automatically encrypted.  

### Network security overview

#### Host-Level Protection

* VPC hosts AWScompute resources (app, web, database)
* Private subnets don't have direct internet access
* Security groups control what traffic is allowed to reach and leave resources

#### Internet Gateway (IGW) Access

* Internet gateway provides internet access to resources hosted on pyblic subnets
  
#### Indirect Internet Access

* A NAT gateway allows EC2 instances in a private subnet to indirectly connect to internet services

#### VPN Gateway Access

* A virtual private gateway allows private VPN connections to a VPC

#### Two-Tier Application

VPC spans two AZs and provides public and private subnets  
The NAT Gateway provides access to the internet through the internet gateway for public subnets  
THe load balancer has access to public queries because it is hosted in the public subnet and via the IGW  
The private subnets host the application and DB servers are hosted  
All these services are provided by the Virtual Private Cloud (VPC)  

#### Subnet Access

* Network access control list (ACLs) allow or deny specific inbound or outbound traffic at the subnet level (optional)

#### Network Protection

* AWS Network Firewall protects subnets in a VPC from threats
* Amazon Route 53 Resolver DNS Firewall protects outbound requests from a VPC

#### VPC Private Connections

* VPC endpoints allow connections from private subnets to supported AWS services
* Peering allows private networking between VPCs
* AWS Transit Gateway connects VPCs and on-premises networks together privately

#### Considerations

* Use a diagramming tool (draw.io) to visualize network design
* AWS has icons for all AWS cloud services

### Demo: Network security options

Select a VPC and view subnets and AZs  
Where are you going to place your resources?  
Then consider the firewalls for the resources.  
Security groups are firewalls for EC2 instances  

> Inbound rules  
outbound rules  

Other Firewalls:  
Network ACL has a default, but can customize, add custom  
DNS Firewall (Route 53)  
Network Firewall (might replace Network ACLs)    

### AWS compliance frameworks

#### ISO 27001

* Security management standard
* Specifies best practices and comprehensive security controls
* Evaluate information security risks

#### SOC 2: Security and Availablity

* SOC means **S**ystem and **O**rganization **C**ontrols
* External audit meets AICPA standards
* Nondisclousure agreement (NDA) is required for SOC 1 and SOC 2 reports

#### PCI DSS Level 1

* Payment Card Industry Data Security Standard
* Applies to entities that store, process, or transmit cardholder data
* Sensitieve authentication data

**Your industry will have specific rules and regulations to consider when operating in the AWS cloud.**

#### Logging Requirements
Payment Card Industry (PCI) DSS Level 1  
5.2: Ensure that all anti-virus mechanisms are current, actively running, and generating audit logs.  

System and Organization Controls 2 (SOC 2)  
3.13: Procedures exist to identify, report, and act upon system confidentiality and security breaches and other incidents.  

Federal Risk and Authorization Management Program (FedRAMP)  
AU-3: The information system produces audit records that contain sufficient information to establish what type of event occurred.  

#### Log Protection

* Encrypted Using SSE
* IAM and Bucket Policies
* Glacier Vault Lock Policy

#### Rules and Regulations

* Internal Rules
* Corporate Rules
* Government Rules

#### Compliance Standards

* Legal regulations may dictate that log files must be stored for a long period of time
* "Logs must be stored for one year"
* Relates to PCI DSS 6.2 and 10, SOC 2, ISO 27001

#### Choosing an AWS Region

* Data Security 
* Data Residency
* Compliance

### Challenge: Review compliance reports with AWS Artifact

#### Step 1: Sign Up for AWS Free Tier

1. Go to [https://www.wellarchitecteedlabs.com](https://www.wellarchitecteedlabs.com).
2. Scroll down and select Amazon Free Tier.
3. After setup, log in to your new AWS account.

#### Step 2: AWS Artifact

1. Log in to AWS Managenent Console.
2. Search and select AWS Artifact.
3. Select View Reports. 
4. Search for "PCI DSS".
5. Select "PCI DSS Attestation of Compliance (AOC) and Responsibility Summary - Current".
6. Select Download Report.

### Solution: Review compliance reports with AWS Artifact

[AWS compliance page](https://aws.amazon.com/compliance/programs/)  

### The AWS shared responsibility model

#### Security of the Cloud: AWS

* Security and compliance are shared responsibilities between AWS and each customer
  * Hardware, software, networking, and physical facilities that host AWS cloud services
  * Adhere to specific compliance standards and security controls

#### Security in the Could: Customer

* Management and configuration of selected cloud services, including IT controls
* Adhere to specific compliance standards and security controls

#### AWS Shared Responsibility Model

<div class="outer-wrapper">
  <style>
    .outer-wrapper {
      width: 80%;
      background-color: white;
    }
    .left-trap {
      font-weight: 700;
      width: 20%;
      padding: 3.5rem 1.5rem 4.5rem 0rem;
      -webkit-clip-path: polygon(0 0, 0 100%, 75% 100%, 100% 50%, 75% 0);
      min-width: 12rem;
    }
    .bg-gray {
      background-color: gray;
    }
    .bg-cyan {
      background-color: cyan;
    }
    .bg-blue {
      background-color: #3492eb;
    }
    .bg-orange {
      background-color: orange;
    }
    .bg-plum {
      background-color: #2C23A1;
    }
    .header {
      font-size: 1.5rem;
    }
    .row {
      display: flex;
      flex-direction: row;
    }
    .column {
      display: flex;
      flex-direction: column;
    }
    .inner-wrapper {
      padding: 1rem;
      max-width: 45rem;
      margin: auto;
      background-color: white;
      justify-content: space-between;
      color: white;
      font-weight: 700;
      text-align: center;
    }
    .boxes {
      justify-content: space-between;
      padding: 0.5rem 0.5rem 0 0;
      width: 100%;
    }
    .boxes > div:not(.sm) {
      padding: 0.75rem 1rem;
      white-space: nowrap;
    }
    .bar {
      padding: 0.75rem 2rem;
    }
    .boxes.thirds > div {
      width: 33.3%;
    }
    .boxes.quarters > div {
      width: 25%;
    }
    .first {
      margin: 0 0.25rem 0 0;
    }
    .last {
      margin: 0 0 0 0.25rem;
    }
    .box:not(.first, .last) {
      margin: 0 0.25rem;
    }
    .bar.bottom {
      margin-top: 0.25rem;
    }
    .bar.below-box {
      margin-top: 0.5rem;
    }
    .bar.top {
      margin-bottom: 0.25rem;
    }
    .bar:not(.top, .bottom, .below-box) {
      margin: 0.25rem 0 0.25rem 0;
    }
    .sm {
      font-size: 0.65rem;
      padding: 0.25rem 0.15rem;
    }
  </style>
  <div class="inner-wrapper row">
    <div class="left-trap bg-gray">
      <span class="header">AWS</span><br />Responsibility for<br />Security <i>of</i> The Cloud
    </div>
    <div class="column">
      <div class="bar bg-blue top">Software</div>
      <div class="boxes quarters row">
        <div class="box bg-orange first">Compute</div>
        <div class="box bg-orange">Storage</div>
        <div class="box bg-orange">Database</div>
        <div class="box bg-orange last">Networking</div>
      </div>
      <div class="bar bg-blue below-box">Hardware/AWS Global Infrastructure</div>
      <div class="boxes thirds row">
        <div class="box bg-orange first">Regions</div>
        <div class="box bg-orange">Availability Zones</div>
        <div class="box bg-orange last">Edge Locations</div>
      </div>
    </div>
  </div>
</div>

#### Customer Shared Responsibility Model

<div class="outer-wrapper">
  <style>
  </style>
  <div class="inner-wrapper row">
    <div class="left-trap bg-cyan">
      <span class="header">Customer</span><br />Responsibility for<br />Security <i>in</i> The Cloud
    </div>
    <div class="column">
      <div class="bar bg-plum top">Customer Data</div>
      <div class="bar bg-plum">Platform, Applications, Identity and Access Management</div>
      <div class="bar bg-plum bottom">Operating System, Network and Fierwall Configuration</div>
      <div class="boxes thirds row">
        <div class="box sm bg-gray first">
          Client-Side Data<br />
          Encryption and Data<br />
          Integrity Authentication  
        </div>
        <div class="box sm bg-gray">
          Server-side Encryption<br />
          (File System and/or Data)
        </div>
        <div class="box sm bg-gray last">
          Networking Traffic Protection<br />
          (Encryption, Integrity, Identity)
        </div>
      </div>
    </div>
  </div>
</div>

#### AWS Responsibilities

* AWS Patches its infrastructure
* AWS maintains the configuration of its infrastructure

#### Customer Responsibilities

* Customers patch their servers and containers
* Customers are responsible for configuring and managing deployed cloud services

#### Customer Responsibilities

* Customers perform all necessary security configuration and management tasks
  * Network Connectivity
  * Network Security
  * Logging and Monitoring
  * Patching
  * Encryption and Key Management
  * Identity Management and Access Control
* Management of the guest operating system (including updates and security patches)
* Management of application software or utilities installed
* Subnet placement and route table management
* Backing up/snapshots

## 3. Identity and Access Management Security

### Identity and access management

#### IAM Controls Access to API Calls

#### IAM Features

* Bundled in the price - IAM can be deeployed with no additional AWS charges
* Controls access to AWS account resources
* Granular permission control
* Identity federation support for externally authenticated users

#### Aecure Access to AWS Resources

* IAM user
* IAM groups
* IAM roles
* Externally authenticated users
* Other AWS accounts

### IAM user and group accounts

#### IAM User

* Are administrators of AWS resources
* Can be given access to the Management Console
* Can also be given access to perform automated tasks
* Have a username, password, and optionally MFA
* Can also be members of IAM groups

#### Access to Resources

| Administrative | Administrative | Programmer |
|---|---|---|
| AWS Management Console | Command-Line Interface (CLI) | APIs via HTTPS |

First IAM needs to _identify_ the user, then IAM grants the user _permissions_.  

* Users
* Groups
* Roles
* External Credentials

Permissions are provided by Policy Documents  

#### IAM Groups

* Groups contain IAM users  
* Permissions apply to all group members
* IAM groups can't be nested
* There are no default IAM groups
* IAM users can belong to multiple groups

Service quotas limit the number of groups and users that can be created  

Groups may be divided like 'Developers' or 'Testers'  

#### Considerations

What administrative tasks would IAM groups be useful for in your organization?  

### AWS credentials

#### Authentication and Authorization

* Initially, all request are implicitly denied
* Nex, all policies are evaluated; the request is denied if there is an explicit denial
* The request is allowed if an explicit allow is found
* If no explicit allow or deny permission is found, then the default implicit deny is maintained

#### IAM User Authentication

* Username and password combination
  * Access key (access key ID + secret access key)
  * Access key + session token
* AWS only authorizes requests allowed by the attached permission policies
* API calls to AWS services must include the access key and session token

#### IAM Authorization

* Controlling authorization to AWS resources with security policies
* Security policies define the level of access to the service
  * Allow/Deny
  * Conditions (define limits)
  * Service (ARN)

#### Managing Credentials

* Identity and Access Management
* IAM Identity Center
* AWS Organizations
* Third-party solution (Okta, F5 BIG-IP Access Policy Manager)

#### Considerations

* Every authenticated IAM user has an access key and session token
* Every AWS resource is assigned an ARN

### IAM policies

#### IAM Policy Rules

* IAM policy permissions allow or deny
* IAM policy logic - explicitly deny or explicity allow

#### Policy Statement Logic

JSON based. You do not have to write them.  

#### IAM Policies

* Managed
* Custom
* Resource*

#### Managed Policy

* Managed policies are created and maintained by AWS
* Are read-only but can be copied
* Attached to multiple IAM users, AIM groups, and IAM roles

#### Inline Policy (discouraged)

* Linked to IAM user, IAM group, or IAM role
* Inline policy is revoked if the user/group/role is deleted

#### Resource Policies

* Are attched directly to the resource
* S3 bucket and S3 Glacier vaults support resource policies
* Sharable across AWS accounts

#### Policy Types

**IAM Based**  
What does a specific entity have access to?  

| DevGroup1 | Read | Write | List |
|---|---|---|---|
| Resource S3 | ✔ | ✔ | ✔ |
| Resource SQS | | | ✔ |
| | | | |

Attached to the IAM user or group  

**Resource Based**  
Who can access the resource?  

| S3 Bucket | Read | List | Write |
|--|--|--|--|
| John | ✔ | ✔ | ✔ |
| Sue | ✔ | | |
| | | | |

Attached to the resource  

Identity based policies are attached to an identity, and so don't have to specify the identity to which they applies.  
Resource based policies are applied to specific resources, and so must specify the identity to which they apply.  

#### Permission Boundaries

AKA Guardrails  

Permission boundaries define what resources an account can access. This could be useful to large organizations that want to create seperate accounts for seperate resources like DBs, S3 buckets, web applications, etc.  

Permission Boundaries over-ride permissions on an identity policy.  

#### Policy Evaluation Logic

* Identity-Based Policies
* Identity-Based Policies + Resource-Based Policies
* IAM Permission Boundary
* AWS Organizations Service Control Policies (SCPs)

### Demo: Creating an IAM group and IAM user

IAM > User groups > Create user group  
Add a name 'admin'  
Select policy "AdministratorAccess' (top of list)  
Click "Create user group" (bottom of page)  

IAM > Users > Create user  
Add a name 'mark'  
Grant access to the AWS Management Console  
Custom password  
User must create a new user at next sign in  

Add mark to the user group  

### Challenge: Create an IAM user group

#### Challenge: Create an IAM User 

#### Step 1: Sign up for an AWS Free Tier

* [https://www.wellarchitecteedlabs.com](https://www.wellarchitecteedlabs.com).
* Scroll down and selecvt Amazon Free Tier
* After setup, log in to your new AWS account

#### Step 2: Create an IAM User Group

1. Log in to AWS Management Console
2. Search and select IAM
3. Select User Groups
4. Click "Create Groups"
5. Name user group "Admin"
6. Attach permissions policy "AdministratorAccess"
7. Click "Create group"

### Solution: Create an IAM user group

### Understanding IAM roles

#### IAM Roles

* Permissions can be defined using an IAM role
* A role is a permission policy
* When a role is assumed, temporary security credentials are provided for access to requested AWS resources
* Attached to externally authenticated user
* Attached to IAM users in the same AWS account
* Attached to IAM users for cross-account access
* Roles are authenticated and approved by the AWS Security Token Service (STS)

#### When to create Roles
* When an application needs access to AWS resources
* When local administrators are already authenticated and need access to AWS resources without signing in again
* When assigning tasks to IAM users
* When a mobile app requires acess to an AWS service

#### IAM Roles

* Roles are used to provide temporary delegatoin of permissions
* Role delegation allows the identity to perform the approved actions listed in the permissions policy
* The user/application is assigned a trust policy with the permission to run the assumed role command
* The assume role request is performed by the Security Token Service (STS)

### STS Operation

* AWS Security Token Service is a global service
* All AWS STS requests go to a single endpoint at [https://sts.amazonaws.com](https://sts.amazonaws.com)
* Regional AWS STS endpoints can also be chosen for faster access speeds
* Security token lifetime can be set from 1 to 36 hours

#### IAM Roles with EC2 Instances

* Simplify management and deployment of access keys to applicatoins running on EC2 instnaces
* Associate an IAM role with the EC2 instance
* The application accesses the AWS service defined by the attached IAM role

#### Cross-Account Access

* Define permissions in one AWS account using assigned IAM role
* Users in AWS account can assume role to access resources in the linked AWS account
* Conditions can also be applied to roles

#### Creating an IAM Role

1. Define the resources you want to allow access to
2. Define the trust policy: What actions and resources is the principal allowed access to?
3. What can assume the role?
4. AWS account, AWS service, SAML provider, or identity provider
5. Associate the permission policy

#### Considerations

* IAM roles provide temporary access to resources when required
* Best practice is to use IAM roles for access rather than an IAM user

### Demo: Creating a role

Adding an IAM role for a webserver needing access to an AWS service.  

IAM > Roles > Create role  
Select trusted entity type "AWS service"  
Use case: "EC2"  
Click "Next"  
Choose permission policy "AmazonS3ReadOnlyAccess"  
Click "Next"  
Give the role name: "s3_access"  
Review policy  
Click "Create role"  

EC2 > Select running webserver (I don't have a running webserver)  
Actions > Security > Modify IAM role  
Choose the role "s2_access"  
Click "Update IAM role"  

Creating a role is the first step.  
Attaching it to where it is actually going to be used is the next step.  
A role doesn't do anything until it is attached to a resource.  

## 4. AWS Security Services

### AWS Shield

#### AWS Shield

* No charge for distributed denial-of-service (DDoS) protection
* DDoS protection for AWS services
* Inline attack mitigation against ifrastrucutre attacks, UDP floods, and SYN floods

### AWS Shield Advanced

If you have an attack that you can't solve yourself  

* Protection against attacks targeting EC2-hosted applications
* Elastic Load Balancing (ELB)
* Amazon CloudFront
* AWS Global Accelerator
* Amazon Route 53 resources

#### Considerations

* AWS Shield protects all AWS customers
* Web Applicatoin Firewall (WAF) filters power AWS Shield

### AWS web application firewall

#### AWS WAF

Managed rules and custom rules  

* Rules protect public-facing AWS resources
* Common attack vectors and threats
* Regular or rate-based rules
* Actions to take (block, allou, count)

#### WAF Integration

* Amazon API Gateway
* Application Load Balancer
* Amazon CloudFront

#### WAF Design

Create a number of rules to protect:  

* Application Load Balancer
* API Gateway
* CloudFront Distributions

#### WAF Rules

* Custom Rule
  * Write rules for your specific situation
* Managed Rule
  * Written by Amazon

#### WAF Traffic Filtering

* Traffic allowed except for specific requests.  
* Traffic denied except for specific requests.  
* Count incoming requests and decide.  

#### Conditions

* IP Address
* Country
* Request Header Values
* Malicious SQL Code
* Malicious Scripts

#### Considerations

* Do you have public-facing applicatoins?
* Consdier creating a free AWS account
* AWS Well-Architected security Workshop - CloudFront with WAF Protection

### Demo: WAF

AWS WAF and Shield:  
Shield is what AWS provides for free.  
WAF is what customers of AWS can use to create rules.  

AWS WAF > Web ACLs > Create web ACL  
name/description  
metric name  
Click "Next"  

Add rules > Managed rule groups  
AWS managed rule groups dropdown  
Browse rules. Select rule with Add to web ACL (bot)  
Click "Edit" to set up configuration  
Choose an inspection level (Common)  
Select appropriate option
Needs some technical background  

CloudFront (CDN) > Distributions > Create  
Choose origin domain: Select application from dropdown list  
Scroll down to Web Application Firewall (WAF)  
"Enable security protections" allows Amazon to provide an ACL that protects the application from common web threats and security vulnerabilities  

### AWS Key Management Services

#### AWS KMS

* Manages the encryiption and decryption of AWS data services
* Unique data keys are used for each encryption request
* KMS stores multiple copies of encrypted keys with 99.999999999% durability
* AWS KMS also supports multi-regioin keys for encryption data in one AWS region and decryption in another region

#### Data Keys

* Data keys are encrypted by using your AWS KMS key (formerly customer master key, or CMK)
* Data keys are not reused
* When an AWS service needs to decrypt your data, KMS decrypts the data key using your KMS key
* All requests to use your KMS key are logged in CloudTrail

#### CloudTrail Logging of KMS Activity

* When were keys used?
* What data was accessed?
* Who used the key?
* Where did the request originate from?

#### Encrypt with Data Key

Data key generated for customer.  
Application uses it to encrypt.  
Application uses it to decrypt.  

#### KMS Administrative Tasks

* Control access to IAM users and roles
* Automatically rotate keys
* Re-enable disabled keys
* Audit use of keys
* Temporarily disable keys
* Create keys with unique aliases

#### Considerations

* Checking off a dialog box starts the encryption process
* KMS is a shared service
* CloudHSM manages encryption keys per customer with non-shared lockboxes

### Demo: Enabling encryption

KMS > Customer managed keys  
Keys the customer creates deliberately  

KMS > AWS managed keys  
Keys created when a service is created, like Lex.  

Example:  
EC2 > Volumes > Create volume  
Click on the "Encrypt this volume" box  
From the drop down select "Default"
This creates a key for the volume managed by Amazon  
Key information is displayed.  
Click "Create Volume"  
Check the properties to see the key info  

KMS > Customer managed keys  
Click "Create key"  
Symmetric or Asymmetric  
click "Next"  
Name the Alias
click "Next"  
Define administrators
click "Next"  
Click "Finish"  
This key will show up in the custom list. It is also available in the Create volume/Encryption?KMS key dropdown  

KMS > AWS managed keys  
See the new key for the new volume  

KMS > CloudHMS key stores
provides seperate hardware for your accounts KMS keys  

### AWS CloudTrail

#### AWS CloudTrail

* AWS CloudTrail monitors and records account activity across your AWS infrastructure
* All API calls and authentications are tracked
* AWS CoudTrail integrates with AWS Organizations (centralize all account activity)

#### AWS CloudTrail Operation

* All API activity is recorded as a CloudTrail event
* CloudTrail events are viewed through event history
* Search, view, and download the last 90 days of activity (free)

#### Create a Custom Trail

For more than 90 days, create a custom trail  

Requires a place to store logs  

* Select a S3 bucket
* Select a CloudWatch log
* Use KMS keys for encryption
* Enable SNS notifications

#### Considerations

* CloudTrail tracks all activity across all active regions
* AWS CloudTrail documentation details the creation of custom trails

### Demo: CloudTrail details

Audits everything that happens in an AWS account.  

CloudTrail > Event history  

Everything is tracked for the last 90 days  

To keep things longer, create custom trail  

CloudTrail > Trails > Create trail  
Name trail  
Store in new S3 bucket (good for third party tools)  
Could encrypt  
Validatoin enabled  
Could store in CloudWatch (allows monitoring)  
click "Next"  
Choose log event
By default, each task is captured  
Data events  
Insight events  
Scroll to Data events
Here you can choose the events you want to log (there is a charge for this)  
Scroll to Insights events  
API call rate and API error rate options (there is a charge for this)  

Pick just management events (no charge) and click "Next"  

### AWS Config

#### AWS Config

* Assesses, audits, and evaluates AWS infrastructure
* Detailed view of the confituration of AWS services in your AWS account
* Automate and maintain compliance with internal policies and regulatroy standards

#### AWS Config in Action

* Continuous monitoring of AWS account resource configurations
* Automate evaluation of recorded configurations against desired configurations
* AWS Config rules can perform automated compliance checking

#### AWS Config Rules

* Automatically check the configuration of AWS resources against compliance rules
* Check if Amazon S3 buckets have a specific feature enabled
* Check if EBS volumes are encrypted as directed

#### Automateed Response

* Automated response to configuration changes
* When resource configurations change, AWS Config can trigger remediation
* Remediation can notify an adminsitrator or make changes to the noncompliant resource

#### Notifications with Amazon SNS

* AWS Config can send notifications whenever resources are created or modified
* Notification sare sent by Amazon Simple Notification Service

#### Considerations

* CloudTrail focuses on who made the specific change, when, and from where
* AWS Config reports on resource changes
* What compliance standards could be maintained with AWS Config?

### Demo: AWS Config

AWS Config > Set up AWS Config  
Select recording strategy (default)  
Select IAM role for AWS Config (Create AWS Config service-linked role)  
Select Delivery method/Amazon S3 bucket (Create a Bucket)  
Optionally, stream configuration changes and notifications to an Amazon SNS topic (this can be used to trigger automation and notifation based on changes)  
click "Next"  
Amazon provides a number of pre-configured rules to choose from  
click "Next"  
Review and "Confirm"  

AWS Config > Dashboard > Conformance Packs  

### AWS GuardDuty

#### Detection Categories

* Reconnaissance activity suggesting attacks
* EC2 instance compromise patterns
* AWS account compromise via API calls
* S3 bucket compromise

#### Intelligent Treat Detection


* CloudTrail Audit of AWS Account
* API Call MOnitorin
* VPC Flow Logs
* Route 53 Query Logs
* S3 Bucket Access
* Lambda Protection
* Amazon RDS Data Protection
* Amazon Elastic Kubernetes Runtime Monitoring
* EC2 Instance Malware Protection

#### GuardDuty Integration

Monitors your logs for you and runs analysis to detect suspicious activities  

#### Considerations

* 30-day free trial
* Sample data for analysis

Can be expensive because it runs all the time. Compare to third party tool cost.  

### Demo Guard Duty protection options

GuardDuty > Summary  
GuardDuty > Settings  
Sample findings are enabled
GuardDuty > Findings  
Lists sample security issues
GuardDuty > Summary  
Graphical views of potential problems
Protections or the right hand side:  
GuardDuty > S3 Protection  
GuardDuty > S3 Protection  
GuardDuty > EKS Protection  
GuardDuty > Malware Protection  
GuardDuty > RDS Protections  
GuardDuty > Lambda Protection  

Accounts  
Supports AWS Organizations

### Amazon Macie

#### Amazon Macie

* Automated security classification of data access patterns
* Monitors data usage for anomalies (over time)
* Proactive data loss prevention through data visibility
* Custom report and alert management

#### Data Classification Types

<div>
  <style>
    .three-table-wrapper {
      display: flex;
      width: 80%;
      margin: 0 auto;
      padding: 1rem 5rem;
      justify-content: space-between;
      border: solid 2px #DDD;
      font-size: 0.75rem;
    }
    .table-wrapper.plumb  td {
      background-color: rgb(105, 20, 139);
      padding: 3.08rem 1rem;;
    }
    .table-wrapper.blue  td {
      background-color: rgb(20, 105, 139);
      padding: 2.68rem 1rem;
    }
    .table-wrapper.orange  td {
      background-color: rgb(139, 91, 20);
      padding: 2rem;
    }
    .table-wrapper td {
      padding: 2px;
      height: 100%;
      text-align: center;
      margin: 0.5rem;
      border: 1px solid #DDD;
    }
  </style>
  <div class="three-table-wrapper">
    <div class="table-wrapper blue">
      <table>
        <tbody>
          <tr>
            <td>CVE</td>
            <td>Router<br />Config</td>
            <td>DSA<br />Private<br />Key</td>
          </tr>
          <tr>
            <td colspan="2">Encrypted RSA<br />Private Key</td>
            <td>Swift Codes</td>
          </tr>
          <tr>
            <td colspan="3">AWS_SECRET_KEY</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="table-wrapper orange">
      <table>
        <tbody>
          <tr>
            <td>Mailing Address</td>
          </tr>
          <tr>
            <td>Full Name</td>
          </tr>
          <tr>
            <td>Credit Card<br />Numbers</td>
          </tr>
          <tr>
            <td>Dirvers<br />License IDs</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="table-wrapper plumb">
      <table>
        <tbody>
          <tr>
            <td>Application Logs</td>
            <td>Encryption Keys</td>
          </tr>
          <tr>
            <td>Email</td>
            <td>Source<br />Code</td>
          </tr>
          <tr>
            <td>JSON</td>
            <td>Financial</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

#### Alerts

* Generated automatically by Amazon Macie security checks
* Custom alerts for exact conditions can be generated

#### Considerations

* Macie does more than GuardDuty
* 30-day free trial
* Sample data for analysis

### Demo: Amazon Macie

Amazon Macie > Summary  
Settings:  
Enable sample findings  

Amazon Macie > Summary  
Data security provides some information  
Findings:  
Sample findings:
Severities of findings  

Jobs:  
Create job  
Pick a buckets  
Click "Next"  
manage data identifier options  
Click "Next"  
Click "Next"  
Allow lists?  
name job  

Macie's primary job is to look at the content, analyzing it, and alerting if it's suspicious, and who is trying to access that data.  

### AWS Security Hub

#### AWS Security Hub

* Comprehensive view of high-priority security alerts and compliance status
* Insights into the configuration and behavior of your AWS resources and accounts
* Automated compliance checks across integrated AWS service

#### Consolidated View

* AWS Security Hub consolidates findings
* Amazon GuardDuty
* Amazon Inspector
* Amazon Macie

#### Considerations

* AWS Security Hub provides a centralized view for managing and analyzing security alerts
* GuardDuty is focused on detecting threats related to malicious activities within AWS resources
* 30-day free trial
* Integrates with AWS Organizations

## Conclusion
### Learning more about AWS security

#### What You've Learned

* AWS security services
* Identity and Access Management

#### Additional Resource

AWS Well-Architected Labs  

#### LinkedIn Learning Course
For a follow up course, recommends:  
_Cloud Security Concepts: Services and Compliance_  
