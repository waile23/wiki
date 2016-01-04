#在MEAN应用中使用JWT进行token认证

##环境
- nodejs
- express
- angularjs

####node中使用的组件

- jwt
- passport
- passport-local
- express-jwt

####anularjs中使用的插件
- angular-jwt

##原理

####server
使用jsonwebtoken生成jwt和验证jwt来实现对token处理。

``` javascript

'use strict'

// sign with default (HMAC SHA256)
var jwt = require('jsonwebtoken');
//失效时间为1分钟
var token = jwt.sign({ username: 'waile23' }, 'mysecret', { expiresInMinutes: 1 });
//output 'token is: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6IndhaWxlMjMiLCJpYXQiOjE0NTE5MTkzOTYsImV4cCI6MTQ1MTkxOTQ1Nn0.2fGK2bhyZixpGwscO14EmRCqfbVmJnBsI-mGtpCLoUY'
console.log('token is: ' + token);


// verify a token symmetric - synchronous
var decoded = jwt.verify(token, 'mysecret');
//output 'decoded is: {"username":"waile23","iat":1451919396,"exp":1451919456}'
console.log('decoded is: ' + JSON.stringify(decoded));


//测试失效token
//输入var token = jwt.sign({ username: 'waile23' }, 'mysecret', { expiresInMinutes: 1 });生成的token值，替换token60mins中的值
var token1min =  'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6IndhaWxlMjMiLCJpYXQiOjE0NTE5MTkzOTYsImV4cCI6MTQ1MTkxOTQ1Nn0.2fGK2bhyZixpGwscO14EmRCqfbVmJnBsI-mGtpCLoUY';
// verify a token symmetric - synchronous  
// execute one minute later throw TokenExpiredError: jwt expired
var decoded1min = jwt.verify(token1min, 'mysecret');
console.log('decoded1min is: ' + JSON.stringify(decoded1min));



//测试失效token
//输入var token = jwt.sign({ username: 'waile23' }, 'mysecret', { expiresInMinutes: 60 });生成的token值，替换token60mins中的值
var token60mins =  'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6IndhaWxlMjMiLCJpYXQiOjE0NTE5MTk4ODQsImV4cCI6MTQ1MTkxOTk0NH0kgmnrK86QC_vWRt0B_IShsIJHeYzLTQwRdwCFyvd-cw';
// verify a token symmetric - synchronous  
var decoded60mins = jwt.verify(token60mins, 'mysecret');
console.log('decoded60mins is: ' + JSON.stringify(decoded60mins));

```

###客户端
angularjs使用angular-jwt插件的jwt拦截器，在每次请求url是在header中写入token信息。




