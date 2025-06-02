# Automating EC2 Instance Start/Stop using AWS Lambda and EventBridge
This project focuses on using AWS Lambda to automate the starting and stopping of Amazon EC2 instances on a regular schedule. Imagine having a fleet of virtual computers in the cloud, each serving different purposes like testing software or running applications. 

These instances incur costs while running, similar to leaving lights on when not needed. By creating Lambda functions, we can instruct AWS to automatically turn off instances during periods of inactivity, such as nights or weekends, and restart them when needed.

This automation not only streamlines resource management but also helps save costs by optimizing instance usage based on specific time intervals. 

The scheduling aspect is handled through Amazon EventBridge, where we set rules to trigger Lambda functions at designated times, ensuring efficient resource utilization and cost-effectiveness within the AWS environment


# Objectives
Launch a Linux-based EC2 instance.

Create and attach an appropriate IAM Role with required permissions.

Develop AWS Lambda functions to start and stop EC2 instances.

Use Amazon EventBridge to schedule the Lambda invocations.

Verify and validate the automation process.
