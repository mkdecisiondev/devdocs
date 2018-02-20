# The AWS Cloud

### By Eric Hendrickson

## Overview

Unlike other set ups, like the MEAN, Ruby on Rails, or Django stacks, MK uses the Amazon Web Services (AWS) cloud. The AWS cloud is a set of services curated by Amazon, which when used together can store files, write to databases, create API endpoints, and more. At MK, we use the AWS cloud to host our web pages as well as orchestrate and host our back end.

AWS is very powerful and is utilized by myriad tech companies, so whether or not you use our implementation in the future it is nothing short of essential to learn if you want to have any career in software development. That being said, it is _incredibly_ complex and eccentric, so as a result it is intimidating at first. Do not let this phase you though. While the learning curve may initially be steep, it will not be long at all before you become reasonably comfortable with it. What follows is a brief tour of the services we use for the MK Decision backend.

## IAM, Lambda, and API Gateway

The three bare minimum technologies that you need to know in order to create a serverless backend API on AWS are IAM, Lambda, and API Gateway.

IAM stands for "Identity and Access Management," and it is one of the ways in which we check who or what is authorized to do or see what. It does this by assigning "roles" to both users as well as processes (such as a Lambda function). "Policies," or permissions, are then added to the roles to authorize the roles to do a specific action and/or access data. Thus, policies authorize users and processes via authorizing roles. If this is confusing to you at this point, relax, because we will go over IAM in more detail, but for now recognize that you must use IAM if you are going to create an API.

Lambda functions are basically just normal functions of code, triggered by themselves. That's it. When learning about Lambda, you will hear buzz words like "serverless" and "stateless," and these are important to understand because an API that utilizes Lambda functions calls those functions differently than an API that is run on your own server. However, explaining that is the purpose of [a different chapter](../introduction-to-lambda/introduction-to-lambda.md). Lambda functions can be run using Java, Python, C#, or even Go, so you can use a number of languages based on their strengths. At MK, however, we will almost exclusively be using Node.js 6.10.

Whereas in most Node-based stacks Express is used to set up API endpoints, in a serverless AWS environment you use API Gateway. API Gateway is a service separate from Lambda. When you make a request to an API Gateway endpoint, it then triggers, or calls, a Lambda function. This means that at MK we generally will not be using Express in our Lambda functions because that is a function of API Gateway.

## Other Services Utilized on the Back End

IAM is necessary to do anything on AWS, while API Gateway and Lambda are sufficient for setting up an API. However, depending on your needs, other AWS services may be necessary. The following is a list of services that we use with our back end at MK:

* **CloudFormation**: Used to deploy a stack and automatically link all your services together. The details of CloudFormation are better suited to advanced AWS developers, but for now just think of it as the way to conveniently link everything together and deploy your code.
* **CloudWatch**: A logging service. This will be your best friend when doing software development at MK.
* **DynamoDB**: A NoSQL database designed to work seamlessly with AWS services. It is probably most similar to MongoDB, but implementing it in a Node-based application is simpler provided you're utilizing the AWS cloud.
* **S3**: A storage service. You can use it to store images or other files that are too big to be stored in DynamoDB and store their references in your database, a feature so convenient and useful that even apps that are not hosted on AWS often use it.
* **SES**: Stands for "Simple Email Service". You can use this to easily send emails through AWS Lambda.
* **SNS**: Stands for "Simple Notification Service". We often use this to notify our developers of any errors when we deploy our code in a production environment. Alternatively, SNS can be used to send text messages to mobile devices.

The way to link these services to your API will be discussed further in later chapters, but for now I hope that these descriptions just paint a picture of how an AWS API can and is organized without using the MEAN, Ruby on Rails, or Django stack.

To see this in action, I recommend setting up your own AWS account and begin watching [this series of videos by Savjee on YouTube](https://www.youtube.com/watch?v=fSUEk6iMW88&list=PLzvRQMJ9HDiSQMe68cti8cupI0mzLk1Gc). We will not be doing things quite this way, but this is a great way to get your feet wet, and the further you get the easier your transition to MK's system will be.
