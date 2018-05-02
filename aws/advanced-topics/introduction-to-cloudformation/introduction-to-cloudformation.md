# Introduction to CloudFormation

Note: this guide will pick up where the [guide on Webpack](../webpack/webpack.md) left off. It is highly advisable to read and implement the steps covered in that guide before moving on to this one. This guide will also assume that the AWS command line interface (CLI) is installed globally and all necessary credentials are already set up. See [this guide](../../introduction-to-aws/credentials-setup/credentials-setup.md) for more info on AWS credentials.

Before beginning this guide, it is important to tell your console which AWS profile to use. Once you have opened the terminal window you will be using for this project, type `$ export AWS_PROFILE=your-profile-name-here` with the actual name of the AWS profile substituted after the equals sign.

## What Is CloudFormation?

An API implemented on the AWS cloud is not made from just one single service. An API endpoint might be set up with API Gateway. This may trigger a function deployed to Lambda. The Lambda function may use any number of AWS services such as DynamoDB, SES or S3 just to name a few examples. While it is perfectly possible for a developer to set up each of these functions manually using the AWS console in the web browser, this can be time-consuming and very tedious. Development by its nature involves a lot of trial-and-error, and having to manually deploy each service any time you want to make a small change is a poor waste of a developer's time.

This is where AWS CloudFormation comes into play. With CloudFormation, it is possible to have a single template file that describes all the resources needed for a project. The developer can make a change to a resource's settings just by changing this template file. Then, using the AWS CLI, it is possible to deploy all specified resources all at once. While this can take time to set up initially, the time saved in the long-term will more than make up for this as a developer can spend more time writing and testing code, and less time deploying and redeploying the same resources over and over.
