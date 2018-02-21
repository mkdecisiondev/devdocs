# Using SNS and Lambda to Send a Random 6 Digit Number Via Text Message

### By Tim Petrone

AWS SNS is a cloud based web service that allows you to send and recieve SMS messages to individual or multiple devices. You can send text messages to mobile phones or SMS-enabled deivces. (e.g. Amazon Kindle) In this documentation, you will learn how to send a text message to an individual mobile phone with an auto generated verification code as the message.

To start, create a lambda function and require the AWS software development kit at the top like so: `const AWS = require('aws-sdk');`. This allows for the use of Amazon Web Services' various platforms. In this case, we will be using AWS.SNS.

The "event" parameter we will be passing into the exports.handler is a JSON object made with a person's information including: first name, last name, phone number, email, etc.

Inside of the exports.handler function, include the SNS event like so: `const SNS = new AWS.SNS();`. This allows the function to use the SNS platform to send and receive SMS messages.

In order to send a text message, we will need to use a Publish action included within the SNS platform's inherent abilities. For JavaScript, the Publish action must take in at least a message and a phone number. Define params to equal an object that holds these keys as shown below:

```javascript
let params = {
	'Message': smsCode,
	'PhoneNumber': event.phoneNumber,
};
```

A third key that can be added to the params is the MessageAttributes key, which holds additional information for use by the SNS event.
- A sender ID can be added to let the SMS show who the message is from. (This does not work within the U.S. For a list of supported countries and regions, please see [here](https://docs.aws.amazon.com/sns/latest/dg/sms_supported-countries.html))
- A max price can be set so that a message will not send if it would exceed the maximum you are willing to pay for it to succeed. (The price for outbound message now in the U.S. is $0.00645. Prices may vary per provider. To check inbound or other countries and regions prices, please see [here](https://aws.amazon.com/sns/sms-pricing/))
- The SMS type can be set to Promotional or Transactional. Promotional optimizes for cost efficiency, while Transactional optimizes for reliability.

The syntax for the above is shown below.

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

These params can now be passed into our Publish action and be promisified which completes the basic set up of our Publish function.

```javascript
 SNS.publish(params).promise();
 ```

 This is what we will be returning at the end of our lambda function.

 Next, we can set up a function that will generate a verification code to send to our user once they input their information as shown below.

 ```javascript
    //...
    	let smsCode = '';

	//this function will generate a random number with d amount of digits. zeros can be the first digit.
	function generate(d) {

		let max = Math.pow(10, d)*9-1;
		let min = Math.pow(10, d);

		let number = Math.floor( Math.random() * max + min);
		smsCode = ('' + number).substring(1);
	}

	generate(6);
    //...
```

 To do this, first set a variable called smsCode to an empty string inside of our exports.handler function but outside of our new function. This variable will get redefined by our generate function and can be used inside our params down below to be sent to the user.

 We want to generate a code with 6 digits and have them all be numeric characters. The parameter "d" is the amount of digits we want to generate. At the bottom, you can see we are generating a 6 digit code when we run the function.

 The variable "max" is a formula that essentially boils down to the number 8,999,999 when the parameter is set to 6. The variable "min" boils down to 1,000,000. The amount of digits specified will always result in a min and max of that amount of digits plus one. This will help us later on.

After those are set up, we will create a formula to generate a random number shown below:

```javascript
let number = Math.floor( Math.random() * max + min);
```

Here we are multipling Math.random by our max. In this case, that would equal anywhere from 0 to 8,999,999. Then we add on our "min" variable, which will bring up our range to anywhere from 1,000,000 to 9,999,999. This is where our 7 digit number will help us out. As you can see, the last 6 digits of any number in that range is anywhere from 000,000 to 999,999. For this reason, we do not care what number is in the millions place. The 7th digit is only there so our 6 digit number can begin with a zero, therefore giving us a truely random 6 digit number. To finish, we redefine the variable "smsCode" by turning our 7 digit number into a string and then use the substring(1) function to only include the 2nd digit onwards. (e.g. The number 4092134 will return the string '092134') This code is shown below:

```javascript
smsCode = ('' + number).substring(1);
```

When we add all the pieces together for this verification code text message, we get the following code:

```javascript
const AWS = require('aws-sdk');

exports.handler = (event, context, cb) => {
	const SNS = new AWS.SNS();

	let smsCode = '';

	//this function will generate a random number with d amount of digits. zeros can be the first digit.
	function generate(d) {

		let max = Math.pow(10, d)*9-1;
		let min = Math.pow(10, d);

		let number = Math.floor( Math.random() * max + min);
		smsCode = ('' + number).substring(1);
	}

	generate(6);

	let params = {
		'Message': smsCode,
		'PhoneNumber': event.phoneNumber,
		'MessageAttributes': {
		    'AWS.SNS.SMS.SenderID': 'MK Decision'
		    'AWS.SNS.SMS.MaxPrice': 0.00645,
		    'AWS.SNS.SMS.SMSType': 'Transactional'
	    }
	};

	cb(null, smsCode);

	return SNS.publish(params).promise();
};
```
