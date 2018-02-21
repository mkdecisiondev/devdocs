# How to Send a Verification Code via Text Using AWS SNS

### By Tim Petrone

AWS SNS is a cloud based web service that allows you to send and recieve messages to individual or multiple devices. You can send text messages to mobile phones or SMS-enabled deivces. (e.g. Amazon Kindle) In this documentation, you will learn how to send a text message to an individual mobile phone with an auto generated verification code as the message.







Random 6 digit number generator that can start with zeros.
Got the idea from this stackover flow link: https://stackoverflow.com/questions/21816595/generate-a-random-number-of-fixed-length-using-javascript


```
exports.handler = (event, context, cb) => {

    let smsCode = '';

    function generate(d) {

        let max = Math.pow(10, d)*9-1;
        let min = Math.pow(10, d);

        let number = Math.floor( Math.random() * max + min);
        smsCode = ('' + number).substring(1);

    }

    generate(6);

    cb(null, smsCode);

};
```
