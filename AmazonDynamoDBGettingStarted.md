---
text: "AWS Skillbuilder"
title: "Amazon DynamoDB Getting Started"
author: "Peter Farrar"
date: 04/17/2025
description: "Learning basics on Amazon DynamoDB"
---

# Amazon DynamoDB Getting Started

## Introduction to Amazon DynamoDB

* Identify the purpose of DynamoDB
* Reconize problems DynamoDB can solve
* Identify the benefits of DynamoDB
* Recognize key characteristics about DynamoDB pricing

### What does DynamoDB do?

DynamoDB is a serverless NoSQL database that uses the best qualities of both a document store and a key/value pair. It is highly performant with single-digit millisecond response speed.  

### What problems does DynamoDB solve?

Performant for large-scale distributed systems requiring high availablity and consistant performance. Able to handle millions of users, process vast volumes of data, and still maintain responsiveness.  

### What are the benefits of DynamoDB?

#### Automatic scaling

DynamoDB automatically scales to handle workload demands without manual intervention. It provdes consistant, fast response times, even when handling millions of request. Applications stay responsive durring peak traffic periods.  

#### Fully managed service

Eliminates operational DB management tasks. No hardware provisioning, software configuration, patching or cluster scaling.  

#### Built-in high availability

Replicates across multiple AWS regions, maintaing a 99.999 % availability rate.  

#### Flexable data model

Supports a flexable schema for both key/value and document storage. Requires a primary key, but allows for different attributes. No schema migrations required.  

#### Comprehensive security

DynamoDB provides comprehensive security features like encryption at rest, in transit, and fine-grained access control. AWS IAM used for auth, supporting IAM policies, resource-based policies, attribute-based access control (ABAC), and access restrictions down to specific items and attributes in a table.  

#### Automatic backups

Includes automatic backup and point-in-time recover for 35 days.  

#### AWS service integration

Integrates with AWS Lambda, Amazon API Gateway, and AWS Step Functions, for building modern, serverless, event-driven architectures.  
Offers zero-ETL integration with Amazon Redshift and Amazon OpenSerch Service.  

#### Event driven capabilities

Applications can automatically respond to data changes to trigger workflows and maintain data consistancy across systems.  

#### Transaction support

Supports atomic, consistent, isolated, and durable (ACID) transactions across multiple items and tables.  

### How much does DynamoDB cost?

* **On-demand capacity mode:** Pay for the read and write requests made. Works well for workloads with unpredictable or intermittent traffic patterns.
* **Provisioned capacity mode:** Reserve a specific amount of read and write capacity in advance. Works well for workloads with predictable and consistent traffic patterns.

Costs are based on several factors:  

* Read and write requests processed
* Data storage used in tables, with Standard and Standard-Infrequent Access table classes
* Data transfer out of DynamoDB
* Additional features like global tables for multi-Region deployment
* Backup and recovery options
* Data streaming and export capabilities
* Data import and export with Amazon Simple Storage Service (Amazon S3)
* Warm capacity for infrequent workloads

There are other factors not listed above. More information is available [here](https://aws.amazon.com/dynamodb/pricing/). Also, there is a [Pricing Calculator](https://calculator.aws/#/) to help estimage costs.  

---

## Architecture and Use Cases

* Recognize the relationship between DynamoDB and other components of the AWS Cloud
* Recognize the meaning of DynamoDB technical concepts
* Identify typical use cases for DynamoDB

### How is Dynamo DB used to architect a cloud solution?

DynamoDB integrates with other AWS services to create distributed global cloud applications.  

### What AWS services integrate with DynamoDB?

#### Lambda

Lambda connects with DynamoDB to process table data and respond to data changes. This integration supports applications that take action based on updates to your database.  

#### API Gateway

APO Gateway works with DynamoDB to create web interfaces for your data. This integration provides secure access to your database for web and mobile applications.  

#### IAM

IAM controls access to DynamoDB resources. This integration manages who can read or change data in your database tables.  

#### CloudWatch

Amazon CloudWatch tracks DynamoDB performance and activity. This integration monitors your database usage and alerts you to potential issues affecting your applications.  

#### AWS AppSync

AWS AppSync seamlessly integrates with DynamoDB tables to extend GraphQL APIs for your application data. This integration helps keep data consistent across mobile and web applications, even when devices are offline.

#### Amazon S3

Amazon S3 works with DynamoDB to manage large files. This integration stores file information in your database while keeping the actual files in cost-effective storage.  

### What are the basic technical concepts of DynamoDB

#### Tables and items

DynamoDB organizes data into tables of items (like a row) with attributes (like columns). Tables require a primary key, but are otherwise  schemaless.  

#### Primary key structure

Each table requires a unique primary key. This can be just the partition key, or it can be composed of the partition key and one or more sort keys.   

#### Data distribution

Using partition keys allows DynamoDB to scale horizontally across storage partitions while maintaining consistent performace as data grows.  

#### Secondary indexes

Global and Local Secondary Indexes (GLIs and LSIs) provide additional query patterns. GSIs can have different partition and sort keys, LSIs must share the same partition key as the base table.  

#### Data operations

DynamoDB provides multiple ways to work with data, including queries, scans, and transactions.  

#### Capacity modes

* On-demand mode automatically handles traffic changes
* Provisioned mode optimizes for a specified expected workload capacity.  

#### Global tables

Global tables automatically replicate data across AWS Regions and have conflict detection and resolution built-in. This provides consistent performance for globally distributed applications.  

#### Backup and recovery

On-demand backups and point-in-time recovery allows restoration to any point within the last 35 days.  

#### Warm throughput capacity

Warm throughput capacity mode provides cost-effective performance for tables with infrequent or unpredictable workloads. Tables are ready for traffic, while minimizing costs when idle. This is good for dev, test, and prod tables that don't require full provisioned capacity at all times.  

#### Security and protection

DynamoDB provides fine grained access controls using IAM, and encrypts all data at rest and in transit.  

### What are typical use cases for DynamoDB

#### Gaming applications

Store player profiles, leaderboards, and game state data.  

#### Session management

Handles application session data efficiently, automatic scaling, and millions of concurrent users.  

#### Digital commerce

Store shopping cart data, product catalogs, and user preferences. High availability and durability provides seemless shopping experiences.  

#### Real-time analytics

Process and store high-velocity data from IoT devices, user activity tracking, and real-time bidding platforms.  

#### Media metadata

Store and retrieve metadata for videos, images, articles, and other digital content, with flexible schema support for varied content.  

#### Mobile backend

Power mobile applications with a scalable backend. Handles user profiles, app settings, and synchronized data across multiple devices seamlessly.  

### What else should I keep in mind about DynamoDB?

#### Security measures

Protect data by implementing these security measures:  

* Configure access policies to control user access and permissions for tables
* Enable encryption at rest using AWS KMS keys to secure stored data
* Use encryption in transit to protect data as it moves between services and applications
* Set up VPC endpoints to enhance network security and data privacy

#### Monitoring capabilities

Track and optimize performance in the following ways:  

* Set up CloudWatch metrics and alarms to monitor key performance indicators like:
  * capacity
  * throttled requests
  * latency
* Use built-in CloudWatch integration to detect bottlenecks and optimize applications
* Create custom dashboards to visualize important metrics in a centrallized view
* Configure automated notifications and alerts for potential performance issues 

#### Backup strategies

Protect and store data long-term using these features:

* Set up backup a strategy using point-in-time recovery and on-demand backup options
* Configure TTL settings to automatically remove expired items from tables
* Export historical data to Amazon S3 for cost-effective storage
* Create data retention policies to match business needs

---

## How to Use Amazon DynamoDB

* Recognize how to use DynamoDB

### Demonstration list

* Creating a Table and a Global Secondary Index
* Querying and Scanning Operations on Your Table and Index
* Enable Point-in-Time Recovery
* Cleaning Up Resources

### Creating a Table and a Global Secondary Index

1. On the DynamoDB dashboard, select `Tables` (left side menu).
2. On the Tables page, choose `Create table`
3. On the Create Table page, in the `Table detail` sectoin, enter a name for the table, a name and data type for the partition key, and optionally a sort key.
4. In the `Table settings` section, choose `Default settings`.
5. Review the configuration and click on **Create table**.
6. Choose the new table from the table list.
7. From the `Actions` menu (top right corner), select `Create index`.
8. On the `Create global secondary index` page, in the `Index details` section, enter a name and data type for the partition key, and the optional sort key, and name the indedin the `Index name` field.
9. Leave the rest of the settings at their default value.
10. select `Create Index` (bottom right corner).

The global secondary index allows querying on a second set of criteria, the game name and top score.  

### Querying and Scanning Operations on Your Table and Index

#### Add items using the Create item form:

1. On the DynamoDB dashboard, select `Explore Items` (left side menu).
2. From the `Tables` list, choose the table you want to create items in.
3. Choose `Create item` (far right)
4. Enter values for the partition and (if there is one) the sort key.
5. From the `Add new attribute` (top right), choose the data type for new information to add to the item.
6. Add the name and value for the new attribute.
7. Continue adding new attributes as needed

#### Add items using the Create item JSON view:

1. Choose `Create item` (far right)
2. From the Create item page, select `JSON view` (top right).
3. Enter a JSON object into the editor. The structure should resemble the sample that follows.
4. Choose `Create item` (bottom right).

```json
{

  "UserId": {

      "S": "201"

  },

  "GameTitle": {

      "S": "Comet Quest"

  },

  "TopScore": {

      "N": "200"

  },

  "Wins": {

      "N": "3"

  },

  "Losses": {

      "N": "1"

  }

}
```

#### Run a query operation:

This requires, at a minimum, the partition key's value.  

1. In the `Scan or query items` choose `Query`.
2. Enter a value in the `Partition key` field.
3. Choose `Run`.

#### Run a scan operation:

Unlike the query operation, scan operations do not require a partition key.  

1. In the `Scan or query items` choose `Query`.
2. To scan for specific items with matching attribute values, choose `Add filter`.
3. Select the attribute names and values for the filter.
4. Choose `Run`.
5. Without a filter, the scan operation returns all the items in the table.

#### Edit an item

1. In the `Items returned` section, select the checkbox next to the item to edit.
2. From the `Actions` dropdown, choose `Edit item`.
3. Use the `Edit item` page's `Attributes` form to edit the values of the item.
4. Select `Save and close` (bottomright).

#### PartiQL

1. On the DynamoDB dashboard, select `PartiQL editor` (left side menu).
2. Select the table you want to query.
3. From the three dots dropdown choose `Query table`.
4. In the PartiQL editor, enter a SQL query on the data in the table and choose `Run`.
5. The results are displayed below.
6. Now run a SQL query against an index. See below for an example of how to query using an index.

```sql
SELECT "GameTitle", "TopScore", "UserId"
FROM "GameScores"."TopScores-GSI"
WHERE "GameTitle" = 'Comet Quest'
ORDER BY "TopScore" DESC
```

### Enableing Point-in-Time Recovery (PITR)

1. On the DynamoDB dashboard, select `Tables` (left side menu).
2. Choose the table you want to enable backups on.
3. Choose the `Backups` tab. This contains all the backup options.
4. Choose `Edit`.
5. On the `Edit point-in-time recovery` pageselect the checkbox in the Point-in-time (PITR) section for `Turn on point-in-time recovery`.
6. Choose `Save changes`.
7. Verify that Point-in-time recovery now shows a status of `On`.

### Cleaning Up Your Resources

How to remove a table and it's associated resources

1. On the DynamoDB dashboard, select `Tables` (left side menu).
2. Choose the table you want to enable backups on.
3. From the `Actions` dropdown, choose `Delete table`.
4. Enter `confirm` in the confirmation dialog box and click `Delete`.

This removes the table and all related resources.  

---

## Resources

* [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
* [Amazon DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
* [DynamoDB Blog Posts](https://aws.amazon.com/blogs/database/category/database/amazon-dynamodb/)
* [AWS re:Post](https://repost.aws/)

---


