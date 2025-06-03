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

## Key Concepts
### AWS Lambda
AWS Lambda is a serverless computing service provided by Amazon Web Services (AWS).

It allows you to run code without provisioning or managing servers, enabling you to focus on writing and deploying code without dealing with infrastructure management. With Lambda, you upload your code and AWS Lambda takes care of automatically scaling and managing the compute resources required to run your code in response to incoming requests or events.

Lambda supports multiple programming languages such as Node.js, Python, Java, Ruby, and others, making it versatile for various application development needs.

Lambda functions can be triggered by various AWS services, APIs, HTTP requests, or scheduled events, providing flexibility in designing serverless architectures.

### Amazon EventBridge
EventBridge is a serverless service that uses events to connect application components, making it easier for you to build scalable event-driven applications.

Event-driven architecture is a style of building loosely coupled software systems that work together by emitting and responding to events.

Event-driven architecture can help you boost agility and build reliable, scalable applications.

Use EventBridge to route events from sources such as home-grown applications, AWS services, and third-party software to consumer applications across your organization.

EventBridge provides simple and consistent ways to ingest, filter, transform, and deliver events so you can build applications quickly.

### AWS IAM Role
An IAM role is an IAM identity that is used to created in your account that has specific permissions.

An IAM role is similar to an IAM user, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS.

However, instead of being uniquely associated with one person, a role is intended to be assumed by anyone who needs it.

Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.

### AWS IAM Policy
An AWS Identity and Access Management (IAM) policy is a set of permissions that define what actions users, groups, and roles can perform on AWS resources.These policies are written in JSON format and are attached to IAM entities to control access to services and resources within an AWS account.

## SETUP 
### 1. Launch Linux Based server
 Go to EC2 Dashboard
- Launch a Linux-based instance
- Note the **Instance ID**
- ![Screenshot (79)](https://github.com/user-attachments/assets/2d1af87a-8204-4ba4-b9e9-d08776cbd7de) ![Screenshot (80)](https://github.com/user-attachments/assets/f638d5bc-34c5-47e9-906d-ec1bfd1297bf)

### 2. Create AWS IAM Role
 #### create policy
Attach the following policy:
    {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "ec2:DescribeInstances"
      ],
      "Resource": "*"
    }
  ]
}
![Screenshot (82)](https://github.com/user-attachments/assets/5e272f84-4a73-4b7e-b07e-854de9b09bb3)

  #### Create Role and Attach created policy
  ![Screenshot (83)](https://github.com/user-attachments/assets/2b74fda9-6100-4eb6-83b2-7fc37cf853f6)![Screenshot (84)](https://github.com/user-attachments/assets/8ed470a0-6e75-48d9-994e-4748a71ac299)![Screenshot (85)](https://github.com/user-attachments/assets/f57b45c4-c555-4b8d-a38f-490593a6a8f2)![Screenshot (87)](https://github.com/user-attachments/assets/48a54a8b-d481-4358-866a-d73da3eb3dd5)

## Configure the Lambda Function & EventBridge
An AWS Lambda function is a serverless computing service provided by Amazon Web Services that allows you to run code without provisioning or managing servers. With Lambda, you can upload your code in the form of a function and AWS takes care of the infrastructure needed to run that function. Lambda functions can be triggered by various AWS services, such as API Gateway, S3 events, DynamoDB streams, and more, as well as by custom events through services like Amazon EventBridge.

  ### Create the Lambda Function
  ---- Select the Runtime as Python 3.9.
       ![Screenshot (90)](https://github.com/user-attachments/assets/f63f627d-abb6-4e16-b38a-bc859b1e9c02)
 ---- Under Permissions, select the Use an existing role and select the IAM Role (LambdaRole) which we have created in the earlier steps. Then click on Create Function.
      ![Screenshot (89)](https://github.com/user-attachments/assets/0eaa7513-fd18-402e-be8f-c9101807e4ae)
 ---- In the code editor, paste the refined start code and deploy
 ![Screenshot (93)](https://github.com/user-attachments/assets/57d8a071-6f53-4a12-bb53-66ffac8c8170)
 ---- In the code editor, paste the refined stop code and deploy
      ![Screenshot (94)](https://github.com/user-attachments/assets/a738f044-484b-451c-98f6-b29068819739)![Screenshot (95)](https://github.com/user-attachments/assets/50e55d26-bf3f-483d-a49e-d552a5cd8107)

### Configure the EventBridge
----  Create EventBridge Rule for Start
    On the Lambda Console, Click on Add Trigger.
    ![Screenshot (97)](https://github.com/user-attachments/assets/6b764d6e-bbbc-4439-8c0e-0f7e73985233)
    Select the Rule type as the Schedule expression.we will write the Expression as cron(0 8 * * ? *) utc. starting instance 8am everyday
    ![Screenshot (99)](https://github.com/user-attachments/assets/46cbdf33-3822-4abf-b5ff-8186078933d8)

----  Create EventBridge Rule to Stop
      On the Lambda Console, Click on Add Trigger.
      ![Screenshot (100)](https://github.com/user-attachments/assets/16d92add-fcfd-4c17-9be9-63cc683e7bb8)
      Select the Rule type as the Schedule expression.we will write the Expression as cron(25 0 * * ? *) utc. stopping instance 12:25am everyday
      ![Screenshot (103)](https://github.com/user-attachments/assets/4663c2aa-b41e-4f2f-b6f1-7ac17ddb1284)

  ## Benefits
1. Cost Optimization: Avoid charges for idle EC2 instances.

2. Automation: Eliminate manual instance management.

3. Scheduling Flexibility: Easily configure based on your workflow.



      

      
