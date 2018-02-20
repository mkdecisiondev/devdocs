Random 6 digit number generator that can start with zeros.

```
exports.handler = (event, context, cb) => {

    let smsCode = '';

    function generate(d) {

        let max = Math.pow(10, d)*9-1;
        let min = Math.pow(10, d);

        let number = Math.floor( Math.random() * max + min);
        smsCode = ('' + number).substring(1);

    }

    generate(event);

    cb(null, smsCode);

};
```
