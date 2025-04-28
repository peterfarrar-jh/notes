# AWS Command Line Interface (CLI) Basics

* Unified tool to manage your AWS services
* Interact with multiple services
* Allows automation through scripts
* Works on Windows, Mac or Linux

## AWS CLI Installation

Go to [aws.amazon.com/cli/](https://aws.amazon.com/cli/) to get instructions.  
Either use the windows installer on Windows, or use pip on Mac or Linux.  
```
% pip install awscli
# or
% sudo pip install awscli
```

### Configure AWS CLI

```
% aws configure
AWS Access Key ID [None]: 
AWS Secret Access Key [None]: 
Default region name [None]: 
Default output format [none]: 
```

Sample command:  

```
% aws ec2 describe-instances
```

Alternative output format:  

```
% aws ec2 describe-instances --output text
% aws ec2 describe-instances --output table
% aws ec2 describe-instances --output json
```

Query for info

```
% aws ec2 describe-instances --query 'Reservations[].Instances[].InstanceId'
% aws ec2 describe-instances --query 'Reservations[].Instances[].Placement.AvailabilityZone'
```

## AWS CLI Use Cases

* Automation
* Report generation
* Usual interaction with the AWS account

