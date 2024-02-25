# Create-API-and-lambda-events-using-SAM
Create API and lambda events using SAM

We continuous with our last demo (S3-TRIGGER-LAMBDA-USING-SAM)

in this demo We're going to create API Gateway with Get and Post methods and lambda events using SAM.

We are going to learn how to put lambda as endpoint of API

We add additional resources from event souce types  (github page)

In the template.yaml file, We are going to add additional resources from event souce types (github page) to obtain lambda-events-API.yml file

Here template.yaml file

```yml
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

```yml
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

Let's run this package lambda-events-API.yml:

$ sam package --template-file lambda-events-API.yml --s3-bucket demotest-101 --output-template-file  lambda-events-API-packaged.yml

The pacckage is downloaded in SAM folder of Cloud9

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/bf2f5918-b4dc-4680-ad7b-670fcd11f2fc)

It take the code from local directory and put it in s3 bucket.

Let's check s3 bucket

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/6338f502-f995-48cb-8617-3e459dca00e4)


# Deploying lambda package with SAM

To deploy the package run the below command

$ sam deploy --template-file lambda-events-API-packaged.yml --stack-name SAM-API-events --capabilities CAPABILITY_IAM

The package is done and changeset created in cloudformation

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/0a4fe34d-42d8-43c6-9af9-8d9b0fe8fb49)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/9ef12141-ebe8-4ab5-b09c-46833dcfea8d)

Let's check out API Gateway first

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/c527288b-1a5e-45ee-a0df-3134dbda7132)

It' triggered lambda function

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/7660c0e7-8b43-4b4c-8482-bb5e9e925237)

Let's check in lambda console

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/9aab492e-ec0f-4e20-8bde-13187aba1a02)

Lambda deployment succeed

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/aed47683-6cdb-4492-8378-cd65c2398f7a)


![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/c95932de-77f6-45ca-aa8b-ff598e79a24e)


