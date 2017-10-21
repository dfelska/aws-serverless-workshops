# Module: Build a Multi-Region Serverless Application for Resilience and High Availability

In this module you will use AWS Lambda to build a Customer Ticketing application so we can provide a great experience to Wild Rydes users.

The Wild Rydes team wants this application to meet the following requirements:
1. Users must be able to submit and view support tickets
2. Users must be able to log in with their Facebook credentials
3. The application should use an entirely serverless architecture (we don't have an ops team to manage our infrastructure!)
4. The application must be able to failover to another region in the case of a disaster. The [RTO][] and [RPO][] must both be less than 15 minutes.

[RTO]: Recovery time objective – the targeted duration of time and a service level within which a business process must be restored after a disaster.
[RPO]: Recovery point objective –  the maximum targeted period in which data might be lost from a service due to a major incident.

## Architecture Overview

The application will utilize three layers:

1. A UI layer built using HTML, Javascript and CSS and hosted directly from AWS S3
2. An API layer built using Node.js running on AWS Lambda and exposed via Amazon API Gateway.
3. A data layer storing customer tickets in DynamoDB.

***[TODO FULL ARCH DIAGRAM]***

Each of these layers will be replicated in a second region so that we can failover in the event of a disaster. In addition, all data in DynamoDB will be replicated from the primary region to the secondary region ensuring that our application data will be available when we failover.

A few additional components will be utilized to assist us including AWS Cognito to allow the application to authenticate users and authorize access to the API layer. AWS Route53 will be used for DNS and will allow us to perform healthchecks on each region and automatically failover if an unhealthy region is detected.

## Prerequisites

### AWS Account

In order to complete this workshop you'll need an AWS Account with access to create AWS IAM, S3, DynamoDB, Lambda and API Gateway. The code and instructions in this workshop assume only one student is using a given AWS account at a time. If you try sharing an account with another student, you'll run into naming conflicts for certain resources. You can work around these by appending a unique suffix to the resources that fail to create due to conflicts, but the instructions do not provide details on the changes required to make this work.

### Facebook Developer Account and App ID

We will be using Facebook federated identity to allow our users to login with their regular Facebook account. In order to set this up you will need a Facebook Developer account. You can sign up for this by [following this guide](https://developers.facebook.com/docs/apps/register/). Note that you will create the App ID later on in this guide using the URL you set up.

### AWS Command Line Interface

To complete parts of this workshop you'll need the AWS Command Line Interface (CLI) installed on your local machine. You'll use the CLI to copy objects into your S3 website bucket.

Follow the [AWS CLI Getting Started guide](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) to install and configure the CLI on your machine.

### A local environment with Git, Node.js, NPM and Angular2

***[TODO: instructions on doing this or setting up in EC2 - maybe cfn'd with custom AMI]***

### Browser

We recommend you use the latest version of Chrome or Firefox when testing the web application UI.

### Text Editor

You will need a local text editor for making minor updates to configuration files or


## Implementation Instructions

This workshop is broken up into multiple modules. In each, we will walk through a high level overview of how to implement or test a part of this architecture. Some guidance is given regarding commands but if you need more detailed step-by-step instructions at any time, you can expand sections for more detail. You must complete each module before proceeding to the next.

### Region Selection

We will be using the following two regions for this workshop. Please remember these and check before creating resources to ensure you are in the correct region:
* Primary: `eu-west-1` (Ireland)
* Secondary: `ap-southeast-1` (Singapore)

### Modules

1. [Build an API layer](1_API/README.md)
2. [Build a UI layer](2_UI/README.md)
3. [Replicate to a second region](3_Replication/README.md)
4. [Test failover](4_Testing/README.md)