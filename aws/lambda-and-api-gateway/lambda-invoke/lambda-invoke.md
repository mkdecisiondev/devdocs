# Using a Lambda Function to Invoke Another Lambda Function

This tutorial will demonstrate how to write a Lambda function that calls a second Lambda function. To do this, we will make use of Lambda's `invoke()` operation, the AWS Documentation for which can be found [here](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Lambda.html#invoke-property).

As always, if you are responsible for creating your function's role in AWS IAM, be sure that it has the necessary permissions to use `invoke()` on the Lambda function it will be invoking. More information about using IAM can be found [here](../../introduction-to-aws/iam/iam.md).

We'll need two Lambda functions: the one that calls the invoke function, and the one that is invoked. For this example they are respectively called `LambdaInvokeTrigger` and `LambdaInvokeEvent`.

## Invoking a Lambda Function as an Event

The first example we will look at is how to make our function "fire and forget," meaning that our first function will not be expecting a response from the second one. This will involve invoking our function as an event.

 We'll keep `LambdaInvokeEvent` as simple as possible to demonstrate `invoke()`: if the function's event param object contains a `message` property it logs that property's value and calls back a string to let us know it's finished. Otherwise it calls back an error.

```javascript
exports.handler = function(event, context, callback) {
	try {
		if (event.message) {
			console.log(event.message);
			callback(null, 'Finished');
		} else {
			throw new Error('Invalid params');
	} catch(err) {
		callback(err, null);
	}
}
```

For `LambdaInvokeTrigger`, we need to first require the AWS SDK, and then create a Lambda instance to give the function access to `invoke()`.

```javascript
const AWS = require('aws-sdk');

exports.handler = function(event, context, callback) {
    const lambda = new AWS.Lambda();
};
```

`lambda.invoke()` takes an object of parameters. The way we configure these parameters will depend on the manner in which we want to call the function.

We need to define a set of params to pass into the `invoke()` function.

```javascript
const params = {
    FunctionName: 'LambdaInvokeEvent',
    InvocationType: 'Event',
    Payload: Buffer.from(JSON.stringify({message: 'Hello World'}))
};
```

* `FunctionName` is naturally the name of the function that will be invoked.
* Setting `InvocationType` to `Event` means that our Lambda function will not be expecting a response from the one it invokes.
* `Payload` is what the invoked function will use as its `event` parameter. This is an object consisting of any information we want to make available to the second function. The object needs to be made from stringified JSON into a buffer before it can be passed into another Lambda function to be used as an event object.

There are other parameters that can be passed into the `invoke()` function if desired. More information about these parameters can be found in the AWS SDK documentation.

Next we use our Lambda instance to call `invoke()`, pass in our params object, and finally callback a string to let us know the function is terminating.

```javascript
lambda.invoke(params);
callback(null, 'Finished');
```

Here is the `LambdaInvokeTrigger` function so far.

```javascript
const AWS = require('aws-sdk');

exports.handler = function(event, context, callback) {
    const lambda = new AWS.Lambda();
    const params = {
        FunctionName: 'LambdaInvokeEvent',
        InvocationType: 'Event',
	    Payload: Buffer.from(JSON.stringify({message: 'Hello World'}))
    };
    lambda.invoke(params);
    callback(null, 'Finished');
};
```

Lastly, let's make `lambda.invoke()` into a promise so we can callback our "Finished" string once `invoke()` has wrapped up or callback an error in a `.catch()` block if it fails.

```javascript
const AWS = require('aws-sdk');

exports.handler = function(event, context, callback) {
    const lambda = new AWS.Lambda();
	const params = {
		FunctionName: 'LambdaInvokeEvent',
		InvocationType: 'Event',
		Payload: Buffer.from(JSON.stringify({message: 'Hello World'}))
	};
    lambda.invoke(params).promise().then(function() {
		callback(null, 'Finished');
	}).catch(function(err) {
		callback(err, null);
	});
};
```

(`lambda.invoke()` can be make into a promise by simply adding `.promise()` to the end when it is called. We know this syntax is valid because in the AWS SDK documentation for `.invoke()`, it is shown to return an AWS request. See [here](../../languages/javascript-promises/javascript-promises.md) for more information about using promises in general as well as with AWS SDK functions in particular).

Let's test out the function. Since `LambdaInvokeTrigger` as it's currently implemented doesn't make use of its own event object, it doesn't matter what we pass in. The default test will do just fine.

![alt text](images/1.png)

When we test the function, we get the return we specified for after `lambda.invoke()` has wrapped up. However, to test whether `LambdaInvokeEvent` has run properly after being invoked, we need to check its logs in AWS CloudWatch.

![alt text](images/2.png)

We can see that `LambdaInvokeEvent` has successfully logged the contents of `invoke()`'s `Payload` parameter from `LambdaInvokeTrigger`.

## Invoking a Lambda Function and Requesting a Response

The next example will demonstrate how to use `invoke()` to call a Lambda function and have that second function return information to the first one.

We're going to alter `LambdaInvokeEvent` so that it modifies the information it receives in its event message and then calls it back so it returned to `LambdaInvokeTrigger`.

```javascript
exports.handler = function(event, context, callback) {
    try {
        if (event.message) {
            const reversedMessage = event.message.split(' ').reverse().join(' ');
            callback(null, reversedMessage);
        } else {
            throw new Error('Invalid params');
        }
    } catch(err) {
        callback(err);
    }
};
```

Now, unless there's an error caused by invalid parameters, the function will reverse the word order of its `event.message` parameter and callback the result.

In `LambdaInvokeTrigger`, we need to change the parameters we pass into `lambda.invoke()` so the `InvocationType` is `'RequestResponse'`. This signifies that when we call `lambda.invoke()`, it is expecting some sort of return from the invoked function.

```javascript
    const params = {
            FunctionName: 'LambdaInvokeEvent',
            InvocationType: 'RequestResponse',
    	    Payload: Buffer.from(JSON.stringify({message: 'Hello World'}))
    };
```

`lambda.invoke()` should now be returning whatever is called back from `LambdaInvokeEvent`. Let's see what it looks like when we log that response.

```javascript
lambda.invoke(params).promise().then(function(response) {
        console.log(response);
    }).catch(function(err) {
        callback(err, null);
    });
```

![alt text](images/3.png)

We are logging an object containing a `Payload` property, the value of which is the reversed string we are expecting. Now all we need to do is parse this value and call it back in our `then()` block.

```javascript
callback(null, JSON.parse(response.Payload));
```

Here's the whole of `LambdaInvokeTrigger` with our final changes:

```javascript
const AWS = require('aws-sdk');

exports.handler = function(event, context, callback) {
    const lambda = new AWS.Lambda();
    const params = {
            FunctionName: 'LambdaInvokeEvent',
            InvocationType: 'RequestResponse',
    	    Payload: Buffer.from(JSON.stringify({message: 'Hello World'}))
    };
    lambda.invoke(params).promise().then(function(response) {
        callback(null, JSON.parse(response.Payload));
    }).catch(function(err) {
        callback(err, null);
    });
};
```

Since the response we are looking for is now in the function we are testing, we can verify we're getting the correct result right in the Lambda console after running the test. Here is the result when running `LambdaInvokeTrigger`:

![alt text](images/4.png)
