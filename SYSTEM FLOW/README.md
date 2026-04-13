## System Flow

1. The university separates cloud environments using AWS Organizations, with a management account for central control, a workload account for the research team, and a security account reserved for central logging and monitoring.

2. The research team launches EC2 instances to run experiments and compute-heavy workloads such as search analysis, data processing, or temporary research environments.

3. AWS Budgets is configured in the management account to monitor spending against a defined budget threshold for research activity.

4. When the defined budget threshold is reached, AWS Budgets sends an alert notification to an Amazon SNS topic.

5. The SNS topic immediately triggers the Lambda function named `budget-enforcer`.

6. The Lambda function checks for running EC2 instances and calls the EC2 stop action to shut them down automatically.

7. CloudWatch Logs records the Lambda execution, providing evidence that the automation was triggered and showing which instance was stopped.

8. As a result, unnecessary compute spend is controlled automatically without relying on researchers to manually stop resources.

9. The security account is included in the architecture to support future centralised logging and monitoring, for example by aggregating CloudTrail logs across accounts for audit and governance purposes.
