# Mock Testing the AWS SDK

### By Tim Petrone

Testing is an important part of the development of a project. It provides reliability to the end product. Sometimes while testing, your functions will have a few dependencies, usually from an outside source, that can make the unit testing phase a bit tricky. In certain cases, running a unit test with dependencies can be impractical or impossible. For these cases, there is a method we can use to overcome these obstacles. This method is called "mocking".

Mocking simulates complex dependencies for use in testing. This avoids triggering actual live dependencies or having to meet specific criteria in order to execute your function. The mocking libraries are usually defined as variables at the top of the testing file with some exceptions we will go over later. For this example, we will be going over the mocking library for Amazon Web Services software development kit. (i.e. `aws-sdk`)

Below is a barebones S3 upload lambda function that will return a url once the upload is complete. Notice how this function is relying on the AWS SDK on the first line and how this function is creating a new S3 event inside the function.

```javascript
const AWS = require('aws-sdk');

module.exports = function(filename, file, data) {
    const s3 = new AWS.S3();
    let params = {
        Bucket: 'testBucket',
        Key: filename,
        Body: file
    };
    return s3.upload(params).promise()
    .then(function (url) {
        return url.Location;
    });
}
```

To begin to use the AWS mocking library, we need to install it via the command line by typing in `pnpm install --save-dev aws-sdk-mock`. After the library finishes installing, we can start creating our testing file.

At the top of our testing file, we will need to “require” the mocking library and assign it to a const variable:

```javascript
const AWS = require('aws-sdk-mock');
```

This will grant access to the mocking library we have installed. We will then set up the skeleton of the chai testing function, including the describe/it functions and the remaining const variables.

  const AWS = require('aws-sdk-mock');
  const sampleTestData = require('./sampleTestData.js');

  // (Any dummy info you want to pass in goes here)

  const uploadS3 = require('../lib/uploadS3.js');

  //The upload file from above
  const expect = require('chai').expect;
  describe('aws-sdk-mock testing', function() {
      it('should give a successful output of an S3 upload', function() {
          let goodApple = sampleTestData;
          return uploadS3('resume.pdf', buffer, goodApple).then(function (url) {
              expect(url).to.be.a('string');
          });
      });
  }

The problem with this test file is that it needs to call on the AWS SDK’s S3 class’s `upload()` function to complete, but because it’s a test, we don’t actually want to call to call this function, because we aren’t really uploading anything. So how do we go about making that happen? Well, now that we have the AWS SDK mocking library we can use an `AWS.mock()` function within our describe function to mock the actions of a real S3 upload.

Within the `describe()` function, but outside of the `it()` function, we need to make an `AWS.mock()` function that runs every time we want to run an it() function so we can simulate the S3 event. In this example, we are only running one `it()` function, but in the future we may want to run multiple. To run the mocking function every time, we can use a `beforeEach()` function and nest the `AWS.mock()` inside of it. The `beforeEach()` function and its equivalents (`afterEach()`, `before()`, and `after()`) are called "hooks". The `beforeEach()` function will execute a set of commands before each `it()` function is tested. As the names imply, `afterEach()` will run a series of commands after every `it()` function, while `before()` and `after()` will only run commands before and after all of the `it()` functions run, respectively.

Below is a typical framework for hooks:

```javascript
describe('description', function() {
    beforeEach(function () {
      //...
    });

    afterEach(function () {
      //...
    });

    it('blah blah blah', function() {
      //...
    });
});
```

For more information on hooks, please see [here](https://medium.com/@kanyang/hooks-in-mocha-87cb43baa91c).

For this example, one of these commands that these hooks run will be an `AWS.mock()`. This function takes in several parameters including: which AWS platform to mock (e.g. DynamoDB, S3, SNS, etc.), which action to take in that platform (e.g. `upload`, `putItem`, `publish`, etc.), and a function that can define additional details for use by the mock. A typical `AWS.mock()` function designed for an S3 upload will look like this:

```javascript
AWS.mock(‘S3’, ‘upload’, function (params, callback) {
  // additional details here
});
```

Each `AWS.mock()` function can only be run once before needing to be reset. To reset the `AWS.mock()` function, we will use an `afterEach()` function after every `it()` function is executed to restore the mock library before the next `it()` function runs. For this we will use `AWS.restore()`. There are two ways to restore a mock library with this function. We can either target the platform and action we just used like this: `AWS.restore(‘S3’, ‘upload’);` or we can use a restore all option like this: `AWS.restore();`. The restore all option will restore every `AWS.mock()` you have used so far so be careful when using this command.

For more information on setting up and using `aws-sdk-mock`, look [here](https://github.com/dwyl/aws-sdk-mock).

If you put all of this together, it could look like something along these lines:

```javascript
const AWS = require('aws-sdk-mock');
const sampleTestData = require('./sampleTestData.js');
const uploadS3 = require('../lib/uploadS3.js');
const buffer = 'TestBuffer';

describe('aws-sdk mock testing', function() {
    beforeEach(function () {
        AWS.mock('S3', 'upload', function (params, callback) {
            expect(params).to.be.an('Object');
            expect(params).to.have.property('Bucket', 'TestBucket');
            expect(params).to.have.property('Key');
            expect(params).to.have.property('Body', 'TestBuffer');

            callback(null, {
                ETag: 'SomeETag',
                Location: 'PublicWebsiteLink',
                Key: 'RandomKey',
                Bucket: 'TestBucket'
            });
        });
    });

    afterEach(function () {
        AWS.restore('S3', 'upload');
    });

    it('should give a successful output of an S3 upload', function() {
        let goodApple = sampleTestData;
        return uploadS3('resume.pdf', buffer, goodApple).then(function (url) {
            expect(url).to.be.a('string');
        });
    });
});
```

All there is left to do is run our test. For this example, we can use a simple $ mocha test in our command line, but with other project setups, you might need to run `pnpm run test`.

It cannot be said too often that there is a distinction between mock testing and regular unit testing. In regular unit testing, we need to account for everything that can go wrong in a process. However, in mock testing, we should always assume that the input we are receiving is absolutely correct. Mock testing should be reserved to only test the actual SDK’s expected behavior and nothing else. If there are any pitfalls before the actual mock is tested, then they should not be part of the actual testing of the mock. This is because in some cases, wrong information can be passed into a mocking test, yet result in a success. This is something to be aware of and consider with care. You should write any possible vanilla unit tests first to avoid any incorrect data being passed through a mock test.
