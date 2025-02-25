+++
title = "Deploying the backend"
weight = 15
+++

[![See Serverlesspresso](/images/se-setup-overview4.png)](https://youtu.be/M6lPZCRCsyA)
The backend is a set of serverless microservices. In this section, you will deploy the following:

* The *Counting* microservice - Uses an [Amazon DynamoDB](https://aws.amazon.com/dynamodb) table for incrementing order numbers sequentially.
* The *OrderManager* microservice - Provides an API to send/update/cancel a coffee order. Consists of a DynamoDB table containing the state of each customer order.
* The *Config* microservice - Uses a DynamoDB table containing information about menu items and shop status, along with an [Amazon API Gateway](https://aws.amazon.com/apigateway) resource to provide authenticated access.
* The *Publisher* microservice - Routes events to different IoT core topics. IoT Core publishes event messages to front end applications.
* The *QR Validator* microservice - Provides QR codes to front end display application, Codes are sorted in a DynamoDB table and used to validate each order.

## Cloning the GitHub repository ##

### Step-by-step instructions ###

Clone the repo which will download a local copy of the instructions and code you will use to build the backend portion of the workshop.

1. Run these commands in the Cloud9 terminal window:

```console
cd ~/environment/
git clone https://github.com/aws-samples/serverless-coffee-workshop ./serverlesspresso
```

![Module 0 Cloud9 clone](../images/setup6.png)

2. Within the Cloud9 file browser on the left hand side you can see the backend files have been downloaded.

![Module 0 Cloud9 backend files](../images/setup7.png)

## Deploy the backend infrastructure

This is a good time to introduce the [AWS Serverless Application Model](https://aws.amazon.com/serverless/sam/), or AWS SAM. SAM is an open-source framework that makes it easier to deploy serverless infrastructure.

This allows you to specify your application requirements in code and SAM transforms and expands the SAM syntax into AWS CloudFormation to deploy your application. You will see and use SAM templates throughout this workshop.

*More information on this services used in this section:*
* [AWS Serverless Application Model](https://aws.amazon.com/serverless/sam/)

### Step-by-step instructions

In this section, you will complete a SAM deployment which will build much of the backend infrastructure which we will add to throughout the rest of the workshop.

1. Go back to your browser tab with Cloud9 running. If you need to re-launch Cloud9, from the AWS Management Console, select **Services** then select [**Cloud9**](https://console.aws.amazon.com/cloud9) under *Developer Tools*. **Make sure your region is correct.**

2. Change directory:
```
cd ~/environment/serverlesspresso/setup
```
3. Use the SAM CLI to build any code dependencies by running the following command:
```
sam build
```

4. Use the SAM CLI to deploy the infrastructure by running the following command:
```
sam deploy --stack-name serverlesspresso-backend --resolve-s3 --capabilities CAPABILITY_IAM
```

5. Once the deployment is complete, you'll see a list of output in the terminal under `CloudFormation outputs from deployed stack`.

![SAM setup](../images/setup9.png)

{{% notice tip %}}
Copy these outputs from the stack to a scratch file, notepad or text editor for later use. These are all the resource names you'll need in subsequent modules.
{{% /notice %}}

6. SAM has now used CloudFormation to deploy a stack of backend resources which will be used for the rest of the workshop.

* Multiple Lambda functions
* An S3 bucket
* A DynamoDB table
* A Cognito UserPool
* An AWS IoT thing
* Step Functions workflows
* EventBridge custom event bus
* Several IAM roles and policies

### Recap

* You cloned a GitHub Repo containing an infrastructure template with resources used by the application.
* You deployed the core SAM template to your AWS account.

### Next steps

In the next module, you'll learn about workflows and state machines, and build the main workflow that powers the application.

{{% notice tip %}}
Now you are ready to start building 👷
{{% notice note %}}