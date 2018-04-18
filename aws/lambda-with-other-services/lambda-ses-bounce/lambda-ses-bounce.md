# Using an SNS Topic to Trigger a Lambda Function on SES Email Bounce


## Overview

Using AWS Simple Email Service (SES) is a convenient way to automate the sending of emails. As with any other programming concept, a developer must always be cognizant of how errors are handled when a program is run, and this can be as simple as an email not making it to its intended destination.

This tutorial will demonstrate how to set up a Lambda function that is triggered by an AWS Simple Notification Services (SNS) topic, which listens for SES email bounces. For our example we will write the information of the email bounce to a DynamoDB table, though the Lambda function can be set up to do just about anything.
