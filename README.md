# Monitoring-AWS-Secrets-Manager-Access

## Project Overview
This hands-on project demonstrates how to monitor access to AWS Secrets Manager by combining AWS CloudTrail, CloudWatch, and Amazon SNS. The project implements the principle of least privilege using IAM policies, validates permissions with AWS CLI, and automatically sends email notifications whenever secret access events are detected.

Throughout the project, two IAM users are used to simulate real-world scenarios:

- Developer – Authorized to retrieve secrets.
- Intern – Unauthorized user used to validate access control and monitoring.

The monitoring workflow records API activity through CloudTrail, forwards logs to CloudWatch Logs, evaluates specific events using Metric Filters, triggers CloudWatch Alarms, and delivers notifications via Amazon SNS.

# Architecture Diagram

