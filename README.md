# Monitoring-AWS-Secrets-Manager-Access

## Project Overview
This hands-on project demonstrates how to monitor access to AWS Secrets Manager by combining AWS CloudTrail, CloudWatch, and Amazon SNS. The project implements the principle of least privilege using IAM policies, validates permissions with AWS CLI, and automatically sends email notifications whenever secret access events are detected.

Throughout the project, two IAM users are used to simulate real-world scenarios:

- Developer – Authorized to retrieve secrets.
- Intern – Unauthorized user used to validate access control and monitoring.

The monitoring workflow records API activity through CloudTrail, forwards logs to CloudWatch Logs, evaluates specific events using Metric Filters, triggers CloudWatch Alarms, and delivers notifications via Amazon SNS.

## Architecture Diagram

![Architecture Diagram](image/Diagram.png)

## Prerequisites
Before starting this project, ensure you have:
- An active AWS Account
- Basic understanding of AWS IAM
- AWS CLI installed
- A verified email address for Amazon SNS notifications
- AWS CloudShell or Windows PowerShell
- Basic knowledge of AWS CloudTrail and CloudWatch

## Phase 1 – Create and Manage Secrets
Step 1 – Create the First Secret
![Create Secret Wizard](image/secret-wizard.png)
Create your first secret in AWS Secrets Manager using the Other type of secret option. Store the secret as a key-value pair and assign a meaningful name such as prod/database. This secret will represent a production database credential used later for access validation and monitoring.

Step 2 – Create Multiple Production Secrets
![Secret list](image/secret-list.png)
Using separate secrets for different services follows the principle of least privilege, allowing each application or user to access only the specific secrets they require.

Step 3 – Verify Secret Configuration
![secret detail](image/secret-detail.png)
Review the secret configuration to verify that it has been created successfully. Confirm the secret name, encryption settings, resource ARN, and current version before proceeding to the IAM configuration phase.

## Phase 2 – Configure IAM Access Control
Objective

In this phase, we implement the principle of least privilege by creating IAM users with different permission levels. A custom IAM policy is used to grant only the minimum permissions required to access specific secrets in AWS Secrets Manager.

Step 1 – Create IAM Users
![user list](image/user-list.png)

Create two IAM users to simulate different access scenarios:

- user-developer – Authorized to retrieve secrets.
- user-intern – No permissions assigned.

These users will be used to validate both authorized and unauthorized access throughout the project.

Step 2 – Create a Customer Managed IAM Policy
![permission](image/permission.png)

Create a customer managed IAM policy that allows only the required Secrets Manager actions:

- secretsmanager:GetSecretValue
- secretsmanager:DescribeSecret

Limit the policy to the specific secrets created in Phase 1. This follows the principle of least privilege by granting access only to the required resources and actions.

Step 3 – Attach the Policy to the Developer User
![attach](image/attach.png)

Attach the custom IAM policy only to user-developer. Leave user-intern without any Secrets Manager permissions to simulate an unauthorized user during the testing phase.

Step 4 – Create Access Keys for AWS CLI
![key1](image/key-1.png)

Download the .csv file

![key2](image/key-2.png)

## Phase 3 – Validate Secret Access Using AWS CLI
Objective

In this phase, AWS CLI is used to validate IAM permissions by testing secret access with different IAM users. The tests demonstrate how the principle of least privilege controls access to AWS Secrets Manager.

Step 1 – Install and Configure AWS CLI
![cek cli](image/cek-cli.png)

Download CLI

![current user](image/current-user.png)

Installing

![CLI](image/CLI.png)

Test aws --version

![version](image/version-cli.png)

## Step 2 – Verify Developer Identity
1. type aws configure, and then login with access key that we just created
![configure](image/caller-dev.png)
2. type aws sts get caller identity, make sure which user we login
![caller](image/caller-dev..png)
3. type aws secretsmanager getsecretvalue secret id prod/database
![secret](image/getsecret-dev.png)
4. now, we try to login with user-intern
![configure](image/configure-intern.png)
5. try to getsecret
![intern](image/getsecret-intern.png)
6. and if we trying to list-secret, both user having 'Access Denied', in security world, you dont have to see full list of secret, if you have specific secret to open
![list](image/list-dev.png)
![list](image/list-intern.png)





















