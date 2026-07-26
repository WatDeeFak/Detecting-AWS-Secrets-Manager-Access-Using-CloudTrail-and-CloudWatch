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

