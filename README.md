# Automated Cost Control for University Research using AWS Organizations

##  Problem

Universities often run multiple research teams (e.g., AI, Data Science, Search), each using cloud resources such as EC2 for experiments. A common issue is that researchers forget to stop compute instances after experiments, leading to uncontrolled cloud costs, lack of visibility per team, and no enforcement of budget limits.

##  Solution

I designed a multi-account AWS architecture using AWS Organizations to isolate research teams and implemented an automated cost control system. When a budget threshold is exceeded, EC2 instances are automatically stopped using an event-driven architecture powered by AWS Budgets, SNS, and Lambda.


## Services Used

AWS Organizations for account structure and governance, Amazon EC2 for research compute workloads, AWS Lambda for automation logic, Amazon SNS for event triggering, AWS Budgets for cost monitoring, IAM for permissions and roles, CloudWatch Logs for observability, and AWS CloudTrail (in the security account) for centralized logging and audit.

##  How It Works

A budget threshold is defined for research workloads. When the threshold is reached, AWS Budgets sends a notification to an SNS topic. This triggers a Lambda function, which automatically identifies and stops running EC2 instances, ensuring that cloud costs are immediately controlled without requiring manual intervention.

##  Key Design Decisions

The system uses a multi-account structure to isolate research teams and improve cost visibility. A serverless approach with Lambda was chosen to avoid additional infrastructure costs. An event-driven architecture ensures real-time response to budget events, and centralised control from the management account simplifies governance across multiple teams.

##  Security Account

A dedicated security account is included to centralise logging and monitoring. It is designed to aggregate CloudTrail logs from all accounts, provide audit visibility, and support future integration with security services such as GuardDuty and Security Hub. This ensures separation of duties and prevents tampering with audit data.

##  Benefits

This solution prevents unnecessary cloud spend, removes reliance on manual intervention, scales across multiple research teams, and improves governance, visibility, and accountability.


##  Summary

This project demonstrates how a university can control cloud costs across research teams using a scalable, event-driven, multi-account AWS architecture, allowing researchers to innovate freely while maintaining strong financial governance and operational control.
