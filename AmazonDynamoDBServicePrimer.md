---
text: "AWS Skillbuilder"
title: "Amazon DynamoDB Service Primer"
author: "Peter Farrar"
date: 04/16/2025
description: "Learning basics on Amazon DynamoDB"
---

## Technical overview

Physical nodes  

Partition key 
Default primary key  

Sort key
Secondary key  

Primary key
Combination of Partition and sort keys (if sort key exists)  

Two types of secondary indexes: Local, Global

Local secondary index
Partition key + up to 5 secondary index keys

Up to 20 global indexes per table

### Security

Uses IAM to create and manage users and roles  

Authentication and permission required

Table and item level

Enterprice grade E2E encryption

Encryption at rest by default

### Example Flows

Access: Client logs into the website  
Pass-through: Amazon API  
Process: AWS Lambda  
Notification and Data Store: SNS and DynamoDB  

Queue: SQS  
Process: Lambda  
Data store: DynamoDB  
Transform: Amazon EMR  
Analytic data: Amazon S3 data lake  
Query: Amazon Athena  

Lyft uses AWS to move faster as a company using over 100 microservices.  
Lyft uses DynamoDB to track all rides.  

Expedia uses AWS to perform analysis on visitors to their site. DynamoDB stores data for analytics.  

---

## Serice Demonstration

_Stephen Cole_  

### Option 1: Create a DynamoDB database in the management console.  

1. Click **Create table**
2. Add values for `Table name` and `Primary key`
3. Click **Create**

That's it.

From there, add items by clicking on the `Items` tab, then **Create item**

---

### Option 2: Create a DynamoDB database in the CLI.

```bash
$ aws dynamodb create-table \
 --table-name world_facts \
 --attribute-definitions \
   AttributeName=country_code, AttributeType=S \
   AttributeName=country_name, AttributeType=S \
 --key-schema \
   AttributeName=country_code, KeyType=HASH \
   AttributeName=country_name, KeyType=RANGE \
 --billing-mode=PAY_PER_REQUEST \ 
 --region=us-east-2
```

### Option 2, step 2: Add an item to the database in the CLI.

```bash
$ aws dynamodb put-item \
 --table-name world_facts \
 --item '{
    "country_code": {"S": "us"},
    "country_name": {"S": "united states"} }' \
 --region=us-east-2 \
 --returned-consumed-capacity TOTAL
```
```
{
    "ConsumedCapaciy": {
        "CapacityUnits": 1.0,
        "TableName": "world_facts"
    }
}
```
You can add different structures as long as you have the defined key(s):

```bash
$ aws dynamodb put-item \
 --table-name world_facts \
 --item '{
    "country_code": {"S": "mx"},
    "country_name": {"S": "mexico"}, \
    "capitol_city": {"S": "mexico city"}, \
    "primary_language": {"S": "spanish"} }' \
 --region=us-east-2 \
 --returned-consumed-capacity TOTAL
```

To update items:  
```bash
$ aws dynamodb update-item \
 --table-name world_facts \
 --key '{
    "country_code": {"S": "us"},
    "country_name": {"S": "united states"} }' \
 --update-expression "SET primary_language = :newval" \
 --expression-attribute-values '{":newval":{"S":"english"}}' \
 --region=us-east-2 \
 --return-values ALL_NEW
```
```
{
    "Attributes": {
        "country_name": {
            "S": "united states"
        },
        "country_code": {
            "S": "us"
        },
        "primary_language": {
            "S": "english"
        }
    }
}
```

To query:  

```bash
$ aws dynamodb query \
 --table-name world_facts \
 --key-condition-expression "country_code = :code" \
 --expression-attribute-values '{":code":{"S":"us"}}' \
 --region=us-east-2
```
```
{
    "Count": 1,
    "Items": [
        {
            "country_name": {
                "S": "united states"
            },
            "country_code": {
                "S": "us"
            },
            "primary_language": {
                "S": "english"
            }
        }
    ],
    "ScannedCount": 1,
    "ConsumedCapacity": null
}
```

or:  

```bash
$ aws dynamodb query \
 --table-name world_facts \
 --key-condition-expression "country_code = :code" \
 --expression-attribute-values '{":code":{"S":"us"}}' \
 --region=us-east-2 \
 --output=text
```
```
1   1
COUNTRY_CODE    us
COUNTRY_NAME    united states
PRIMARY_LANGUAGE    english
```

Other options include `--output=table`  

---

