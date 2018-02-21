# IAM Explained

### By Eric Hendrickson

## Overview

Identity and Access Management, or IAM, is the way that AWS regulates the scope of an entity's abilities. By "entity," I mean users and services, like Lambda functions. IAM can also configure multi factor authentication for users signing into the AWS console. IAM is also directly involved in the creation of keys so a user in a remote development environment can deploy a project on AWS.

## Permissions

In order to understand permissions, you must understand the entities I mentioned above. These are users and services.

* **Users:** As you can probably guess, users are, well, just users signed into AWS. Users can be given permissions directly or assigned to **groups** in order to receive permissions.
* **Services:** Services are AWS processes, such as Lambda functions. Services are assigned **roles** in order to receive permissions.

Unless a user or a service is explicitly given a permission, it cannot do anything in AWS. Thus, in order to have permissions, users need to have permissions added to them or to be assigned to groups with permissions. Services need to be assigned roles that have permissions attached to them. Permissions are given to users, groups, and roles in the form of policies.

### What Is a Policy?

A policy is a JSON object that contains a permission. Take this policy for example:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "logs:*"
            ],
            "Resource": "*"
        }
    ]
}
```

This policy, when added to a role, will allow whatever service that role is assigned to to write logs for anything. Its official name is CloudWatchLogsFullAccess. Let's break it down further:

* **Version:** The policy version. Don't change this value.
* **Statement:** This field is an array of objects that give permissions. The fields within the object in this example are:
  * **Effect:** Determines whether a policy allows or denies access. Usually you're going to see "Allow" in this field, simply because as stated before, permissions are denied by default.
  * **Action:** An array of actions. They are formatted as "service:function". In this case, `logs` refers to the CloudWatch service, and `*` refers to every single function in CloudWatch.
  * **Resource:** The specific arn, or id, that you want to access. This could refer to a specific DynamoDB table, S3 bucket, or whatever. In this particular case, `*` refers to every resource.

When you add policies to a user, group, or role, you can either choose from a group of preset policies (such as the one mentioned above) or create your own. If you create your own policies, make sure you research the documentation for the AWS service you're trying to effect. You want to give your entity enough permissions to accomplish the task you want it to do, but you also need to make sure it doesn't have more permissions than it needs.

For more information on policies, check out the [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html).

### Managing Permissions

In general, it is smart to follow these guidelines:

1. Add policies to groups and then assign users to groups, instead of granting individual permissions to individual users.
2. In the final product, make certain that there is only one role per service and that that role only has policies absolutely essential to its task, and nothing more.

In a development environment it is okay to be lax on the second point, because you are just figuring out how to do a certain thing. This is also why we created the role "tfe-lambda-role" in the TFE Workspace. However, even during the development process, you should make an effort to understand what specific permissions are necessary for your task.

## What Comes Next

At MK Decision, we require our developers to have multi factor authentication set up on their AWS accounts. You will also need to configure your AWS CLI keys. The next two articles will discuss how to do these things.
