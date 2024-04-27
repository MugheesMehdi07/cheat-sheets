# AWS Cheat Sheet

## Core AWS Services

### 1. Amazon EC2 (Elastic Compute Cloud)
- **Launch Instance**: `aws ec2 run-instances --image-id ami-xxxxxxx --count 1 --instance-type t2.micro --key-name MyKeyPair`
- **Stop Instance**: `aws ec2 stop-instances --instance-ids i-xxxxxxx`
- **Terminate Instance**: `aws ec2 terminate-instances --instance-ids i-xxxxxxx`

### 2. Amazon S3 (Simple Storage Service)
- **Create Bucket**: `aws s3 mb s3://my-bucket`
- **List Buckets**: `aws s3 ls`
- **Upload File**: `aws s3 cp my-file.txt s3://my-bucket`
- **Download File**: `aws s3 cp s3://my-bucket/my-file.txt my-file.txt`
- **Delete File**: `aws s3 rm s3://my-bucket/my-file.txt`

### 3. Amazon RDS (Relational Database Service)
- **Create Database**: `aws rds create-db-instance --db-instance-identifier mydb --db-instance-class db.m4.large --engine mysql`
- **List Databases**: `aws rds describe-db-instances`
- **Delete Database**: `aws rds delete-db-instance --db-instance-identifier mydb --skip-final-snapshot`

### 4. Amazon VPC (Virtual Private Cloud)
- **Create VPC**: `aws ec2 create-vpc --cidr-block 10.0.0.0/16`
- **List VPCs**: `aws ec2 describe-vpcs`
- **Delete VPC**: `aws ec2 delete-vpc --vpc-id vpc-xxxxxxx`

### 5. AWS Lambda
- **Create Function**: `aws lambda create-function --function-name my-function --runtime nodejs12.x --role arn:aws:iam::123456789012:role/lambda-ex --handler index.handler --zip-file fileb://function.zip`
- **Invoke Function**: `aws lambda invoke --function-name my-function output.txt`
- **List Functions**: `aws lambda list-functions`

### 6. Amazon DynamoDB
- **Create Table**: `aws dynamodb create-table --table-name my-table --attribute-definitions AttributeName=ID,AttributeType=S --key-schema AttributeName=ID,KeyType=HASH --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1`
- **List Tables**: `aws dynamodb list-tables`
- **Delete Table**: `aws dynamodb delete-table --table-name my-table`

## Key AWS Concepts

- **IAM (Identity and Access Management)**: Manage users, groups, roles, and permissions.
- **Elastic Load Balancing (ELB)**: Automatically distribute incoming traffic across multiple targets.
- **Auto Scaling**: Automatically adjust capacity to maintain steady, predictable performance.
- **AWS CloudFormation**: Write templates to create and manage AWS resources.
- **AWS CloudWatch**: Monitor resources and applications.

## AWS CLI Basics

- **Configure AWS CLI**: `aws configure`
- **List AWS CLI Commands**: `aws help`
- **Command Help**: `aws [command] help`

## Security and Identity

- **Create IAM User**: `aws iam create-user --user-name my-user`
- **List IAM Users**: `aws iam list-users`
- **Attach User Policy**: `aws iam attach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --user-name my-user`

## Networking

- **Create Security Group**: `aws ec2 create-security-group --group-name my-sg --description "My security group" --vpc-id vpc-xxxxxxx`
- **List Security Groups**: `aws ec2 describe-security-groups`
- **Delete Security Group**: `aws ec2 delete-security-group --group-id sg-xxxxxxx`

