# Introduction to CloudFormation

Note: this guide will pick up where the [guide on Webpack](../webpack/webpack.md) left off. It is highly advisable to read and implement the steps covered in that guide before moving on to this one. This guide will also assume that the AWS command line interface (CLI) is installed globally and all necessary credentials are already set up. See [this guide](../../introduction-to-aws/credentials-setup/credentials-setup.md) for more info on AWS credentials.

Before beginning this guide, it is important to tell your console which AWS profile to use. Once you have opened the terminal window you will be using for this project, run `$ export AWS_PROFILE=your-profile-name-here` with the actual name of the AWS profile substituted after the equals sign.

## What Is CloudFormation?

An API implemented on the AWS cloud is not made from just one single service. An API endpoint might be set up with API Gateway. This may trigger a function deployed to Lambda. The Lambda function may use any number of AWS services such as DynamoDB, SES or S3 just to name a few examples. While it is perfectly possible for a developer to set up each of these resources manually using the AWS console in the web browser, this can be time-consuming and very tedious. Development by its nature involves a lot of trial-and-error, and having to manually deploy each service any time you want to make a small change is a poor use of a developer's time.

This is where AWS CloudFormation comes into play. With CloudFormation, it is possible to have a single template file that describes all the resources needed for a project. The developer can make a change to a resource's settings just by changing this template file. Then, using the AWS CLI, it is possible to deploy all specified resources all at once. While this can take time to set up initially, the time saved in the long-term will more than make up for this as a developer can spend more time writing and testing code, and less time deploying and redeploying the same resources the hard way over and over.

## The Serverless Application Model

There are multiple ways to set up a project and have the various AWS resources interact with each other. The API created in this demonstration will follow the Serverless Application Model (SAM). The deploy template created here will be following this model. Information for SAM provided by the AWS team can be found [here](https://github.com/awslabs/serverless-application-model), as well as the official SDK documentation located [here](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) While this repository has little in the way of descriptive documentation, the readme does link to examples of projects built around this model with an accompanying deploy template for each one. This can be a very useful resource for developers creating their own templates from scratch.

If you intend to use a model other than SAM, it is important to research that model thoroughly to make sure the format of the template is correct. Information about templates for other models can be found in the official AWS SDK documentation located [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html).

## The Deploy Template

In your project directory, create a file called `deploy.yml`. This will be our template where we specify all the resources we want to create when we deploy.

Recall that in the project we set up in the Webpack documentation, we've created a handler called `contact`. We are going to write our template to automatically deploy this function to Lambda whenever we enter the relevant script in the terminal.

To keep this tutorial focused on CloudFormation, let us assume that the IAM role intended for the AWS function has already been created. For more information about using IAM to create roles and add permissions, please see our [documentation on IAM](../../introduction-to-aws/iam/iam.md).

Here is the code we will use for our `deploy.yml` template.

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Resources:
  Contact:
    Type: AWS::Serverless::Function
    Properties:
      Handler: contact.handler
      Runtime: nodejs8.10
      CodeUri: ./build/contact.js
      Timeout: 3
      MemorySize: 128
      Role: role-ARN-goes-here
      Events:
        RootPost:
          Type: Api
          Properties:
            Path: /contact
            Method: post
```

Let's break down these properties:

* `AWSTemplateFormatVersion: '2010-09-09'`: According to the [SDK documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/format-version-structure.html) as of May 2018, this must be set to 2010-09-09.

* `Transform: AWS::Serverless-2016-10-31`: This is where we declare that we are using the SAM model. Setting this will simplify the configuration we have to do to the Lambda function itself. AWS SDK documentation for this property is [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-aws-serverless.html).

* `Resources`: This takes up most of the template. All resources we want to be deployed will be described here.

* In this example, `Contact` is the name we want to give to the function when it is deployed to Lambda. All settings related to this handler will go inside this property.

* `Type: AWS::Serverless::Function`: The type must be set to this for Lambda functions when using the Serverless Application Model.

* `Handler: contact.handler`: `handler` is the name that we have given the function being exported from the contact file.

* `Runtime: nodejs8.10`: This is the version of Node.js we are telling Lambda to use. Recall that when we created the configuration for Babel in the Webpack guide, we set Node 8 as the version to transpile our code to.

* `CodeUri: ./build/contact.js`: This is the directory that our build of this function is written to when we run our Webpack script. This is where we want CloudFormation to pull our code from to be deployed.

* `Timeout: 3`: When the function has been deployed and is being run, this is the maximum amount of time (in seconds) that it will be allowed to run before it is terminated. 3 seconds should be more than enough time for simple functions. This can be raised if desired, but this can be more expensive as resources used for longer periods of time will cause AWS to bill for a higher amount. In general, it shouldn't be set for a much higher duration than the actual function is expected to take to run.

* `MemorySize: 128`: Similarly to timeout, raising this number will allow more memory to be allocated to running the function, but using more memory is more costly than using less.

* `Role`: The value of this property should be the ARN of the role that will be assigned to the function.

* `Events`: in the SAM model, this is where we specify the API endpoint that will be triggering this function. The `RootPost` property and the `post` value for the `Method` property are being used because the API will be set to trigger this function on post requests. `/contact` is the name of the API resource to which the post method will be assigned.

For now, the Lambda function is the only resource we will be creating. However, if we wanted to set up other resources such as an S3 Bucket or DynamoDB table, we would place each one under the `Resources` properly. For example, the SDK documentation for SAM also shows how to create a simple DynamoDB table on deployment [here](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html#simpletable).

## Scripts
