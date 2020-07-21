# Amazon EventBridge - Producer/Consumer example

This example application creates two AWS Lambda functions - a producer and a consumer. The SAM template deploys these functions, together with an EventBridge rule that determines which events are routed to the consumer.

The example shows how an ATM application at a bank could generate events, and the rule only passes 'approved' transactions to an event consuming application.

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

```bash
.
├── README.MD                   <-- This instructions file
├── atmProducer                 <-- Source code for a lambda function
│   └── handler.js              <-- Main Lambda handler
│   └── events.js               <-- Events
│   └── localTest.js            <-- Wrapper for local testing
│   └── package.json            <-- NodeJS dependencies and scripts
├── atmConsumer                 <-- Source code for a lambda function
│   └── handler.js              <-- Main Lambda handler
├── template.yaml               <-- SAM template
```

## Requirements

* AWS CLI already configured with Administrator permission
* [NodeJS 12.x installed](https://nodejs.org/en/download/)

## Installation Instructions

1. [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and login.

1. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [install the AWS Serverless Application Model CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) on your local machine.

1. Create a new directory, navigate to that directory in a terminal and enter ```git clone https://github.com/jbesw/aws-serverless-eventbridge-consumers```.

1. From the command line, run:
```
sam deploy --guided
```
Choose a stack name, select the desired AWS Region, and allow SAM to create roles with the required permissions. Once you have run guided mode once, you can use `sam deploy` in future to use these defaults.

## How it works

* Use the AWS CLI or AWS Lambda Console to invoke the Producer function. This places the events in `events.js` onto the default event bus in EventBridge.
* The EventBridge rule specified in `template.yaml` filters the events based upon the criteria in the `EventPattern` section.
* When the rule validates an event, it is routed to the Consumer function. This logs out the event, which you can see in CloudWatch Logs.

==============================================

Copyright 2020 Amazon.com, Inc. or its affiliates. All Rights Reserved.

SPDX-License-Identifier: MIT-0