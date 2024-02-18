# Create-API-and-lambda-events-using-SAM
Create API and lambda events using SAM

We continuous with our last demo (S3-TRIGGER-LAMBDA-USING-SAM)

in this demo We're going to create API Gateway with Get and Post methods and lambda events using SAM.

We are going to learn how to put lambda as endpoint of API

We add additional resources from event souce types  (github page)

In the template.yaml file, We are going to add additional resources from event souce types (github page) to obtain lambda-events-API.yml file

Here template.yaml file

```json
Description: Test Pipeline Lambda
Resources:
  samfunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: samfunction
      Description: Sample SAM lambda deployment
    Metadata:
      SamResourceId: samfunction
```


Here is the final template for lambda-events-API.yml file

```json
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Description: Test Pipeline Lambda
Resources:
  hellofunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: ./lambda-sam/hello_country.py
      Description: Sample SAM Lambda Deployment
      Events:
        S3Event:
          Type: Api
          Properties:
            Path: /photos
            Method: get
```

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/4793a851-9770-4529-8be0-5480c2be021c)



# Create lambda template with SAM

Let's run this package lambda-events-s3.yml:

$ sam package --template-file lambda-events-API.yml --s3-bucket demotest-101 --output-template-file  lambda-events-API-packaged.yml

The pacckage is downloaded in SAM folder of Cloud9

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/7219b79a-e997-4665-889c-6c5cb5fe8359)

It take the code from local directory and put it in s3 bucket.

Let's check s3 bucket

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/6338f502-f995-48cb-8617-3e459dca00e4)


# Deploying lambda package with SAM

To deploy the package rune the below command

$ sam deploy --template-file lambda-events-s3-packaged.yml --stack-name SAM-S3-events --capabilities CAPABILITY_IAM

The package is running and changeset created in cloudformation

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/e5a2aa26-b720-4816-ae0e-2f05b2ab1150)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/7fd7f55c-50a1-44a3-974a-4b5ef0ff7820)

Let's check in lambda console

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/9aab492e-ec0f-4e20-8bde-13187aba1a02)

Lambda deployment succeed

There is no trigger here but we can check it in S3 bucket

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/1922c5d3-6ac1-48ac-b5f9-c66a533e2f17)


![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/ba3bcd0b-7d67-4724-9d58-c538f264b601)


Let's check S3 bucket

Properties

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/a08fab95-b99e-4381-a549-ac3bee5c731b)

scrowl down to "Event notifications"

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/97332493-5c39-4496-933d-8d6c669ee076)
