# Deploying a Python Application on AWS Lambda

This README provides detailed instructions for setting up and deploying a Python application on AWS Lambda using AWS SAM (Serverless Application Model), including how to integrate with AWS API Gateway.

## 1. Introduction to AWS Lambda

AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes.

## 2. Setting Up AWS SAM

AWS SAM is an open-source framework that you can use to build serverless applications on AWS.

### Installation

Install the AWS SAM CLI:

```bash
pip install aws-sam-cli
```

Configure your AWS credentials:

```bash
aws configure
```

## 3. Creating a Lambda Function

### Sample Python Function

Create a new file `app.py`:

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

### SAM Template

Define your AWS Lambda function in `template.yaml`:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function 
    Properties:
      CodeUri: .
      Handler: app.lambda_handler
      Runtime: python3.8
      Events:
        HelloWorldApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

## 4. Deploying with AWS SAM

Build your application:

```bash
sam build
```

Deploy your application:

```bash
sam deploy --guided
```

## 5. Integrating with AWS API Gateway

The SAM template defines an API event that triggers your Lambda function via HTTP GET requests. After deploying, AWS SAM automatically creates an API Gateway endpoint.

## Conclusion

By following these steps, you have created a Python Lambda function, defined it with AWS SAM, and deployed it with an associated API Gateway endpoint. This setup enables you to run Python code in response to HTTP requests without managing servers.
