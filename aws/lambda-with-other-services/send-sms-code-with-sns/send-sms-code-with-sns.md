# Using SNS and Lambda to Send a Random 6 Digit Number Via Text Message

Note: Read about [Promises](languages/javascript-promises/javascript-promises.md) if you haven't already before reading this.

AWS SNS is a cloud based web service that allows you to send and recieve SMS messages to individual or multiple devices. You can send text messages to mobile phones or SMS-enabled devices. (e.g. Amazon Kindle) In this documentation, you will learn how to send a text message to an individual mobile phone with an auto generated verification code as the message.

To start, create a lambda function and require the AWS software development kit at the top like so:

```javascript
const AWS = require('aws-sdk');
```

This allows for the use of Amazon Web Services' various platforms. In this case, we will be using AWS SNS.

Next, we can create a function outside the handler that will generate a verification code to send to our user once they input their information as shown below.

```javascript
function generate(numDigits) {
	let max = Math.pow(10, numDigits)*9-1;
	let min = Math.pow(10, numDigits);

	let number = Math.floor( Math.random() * max + min);
	let smsCode = ('' + number).substring(1);
	return smsCode;
}
```

We want to generate a code with 6 digits and have them all be numeric characters. The parameter `numDigits` is the amount of digits we want to generate. The variable `max` is a formula that essentially boils down to the number 8,999,999 when the parameter is set to 6. The variable `min` boils down to 1,000,000. The amount of digits specified will always result in a min and max of that amount of digits plus one. This will help us later on.

After those are set up, we will create a formula to generate a random number as seen above and in the excerpt below:

```javascript
let number = Math.floor( Math.random() * max + min);
```

Here we are multipling Math.random by our `max`. In this case, that would equal anywhere from 0 to 8,999,999. Then we add on our `min` variable, which will bring up our range to anywhere from 1,000,000 to 9,999,999. This is where our 7 digit number will help us out. As you can see, the last 6 digits of any number in that range is anywhere from 000,000 to 999,999. For this reason, we do not care what number is in the millions place. The 7th digit is only there so our 6 digit number can begin with a zero, therefore giving us a truely random 6 digit number. To finish, we define the variable `smsCode` by turning our 7 digit number into a string and then use the substring(1) function to only include the 2nd digit onwards (that is, the number 4092134 will return the string '092134'). We will then return `smsCode`. This code is shown above and in the excerpt below:

```javascript
let smsCode = ('' + number).substring(1);
```
Now that the text message verification code is being generated, we can begin writing the `exports.handler` function. The `event` parameter we will be passing into the `exports.handler` is a JSON object that should at least contain the key `phoneNumber` followed by a phone number as a string.

Inside of the `exports.handler` function, include the SNS event. The `exports.handler` funtion should look like this:

```javascript
exports.handler = function(event, context, callback) {
	const SNS = new AWS.SNS();

	//...
}
```
This allows the function to use the SNS platform to send and receive SMS messages.

Within our `exports.handler` we can call the generate function above to generate our 6 digit verification code.

```javascript
let smsCode = generate(6);
```

In order to send a text message, we will need to use a Publish action included within the SNS platform's inherent abilities. For JavaScript, the Publish action must take in at least a message and a phone number as parameters.

An optional third key that can be added to the params is the MessageAttributes key, which holds additional information for use by the SNS event.
- A **sender ID** can be added to let the SMS show who the message is from. (This does not work within the U.S. For a list of supported countries and regions, please see [here](https://docs.aws.amazon.com/sns/latest/dg/sms_supported-countries.html))
- A **max price** can be set so that a message will not send if it would exceed the maximum you are willing to pay for it to succeed. (The price for outbound message now in the U.S. is $0.00645. Prices may vary per provider. To check other prices, please see [here](https://aws.amazon.com/sns/sms-pricing/))
- The **SMS type** can be set to Promotional or Transactional. Promotional optimizes for cost efficiency, while Transactional optimizes for reliability.

Define params as shown below:

```javascript
let params = {
    'Message': smsCode,
    'PhoneNumber': event.phoneNumber,
    'MessageAttributes': {
        'AWS.SNS.SMS.SenderID': 'MKDecision'
        'AWS.SNS.SMS.MaxPrice': 0.00645,
        'AWS.SNS.SMS.SMSType': 'Transactional'
    }
};
```

These params can now be passed into our `publish()` action which has been promisified to complete the set up. We then add the callback to complete the `exports.handler` function.

```javascript
SNS.publish(params).promise();

callback(null, smsCode);
```

When we add all the pieces together, we get the following code:

```javascript
const AWS = require('aws-sdk');

let smsCode = '';

function generate(numDigits) {
	let max = Math.pow(10, numDigits)*9-1;
	let min = Math.pow(10, numDigits);

	let number = Math.floor( Math.random() * max + min);
	let smsCode = ('' + number).substring(1);
	return smsCode;
}

exports.handler = function(event, context, callback) {
	const SNS = new AWS.SNS();

	let smsCode = generate(6);

	let params = {
		'Message': smsCode,
		'PhoneNumber': event.phoneNumber,
		'MessageAttributes': {
			'AWS.SNS.SMS.SenderID': 'MKDecision'
			'AWS.SNS.SMS.MaxPrice': 0.00345,
			'AWS.SNS.SMS.SMSType': 'Transactional'
		}
	};

	SNS.publish(params).promise();

	callback(null, smsCode);
};
```
