# drivethrough api

## useful links
- authentication config: [link](configuration-authentication)
- main config: [link](configuration-main)
- shop config: [link](configuration-shop)
- service config: [link](service-config)
- setup: [link](setup)

## server
- intial dev: http://dtapi.codehub.io

## test
http://test.codehub.io


## sale documentation

https://github.com/siliconprime-hoanguyen/drivethrough/blob/master/sale.md

## consumer documentation

https://github.com/siliconprime-hoanguyen/drivethrough/blob/master/consumer.md


## protected api must be called with header

```javascript
{
   Authorization: Bearer xxxxxxx //xxxxxxx is the token received when calling login api successfully.
}
```

### registration & authentication

* **registration consumer account**

```javascript
post /accounts
```

```javascript
{
  "email":"codehubio@gmail.com",
  "password":"12345678", // must be more than 6
  "firstName":"hoa",
  "lastName":"nguyen",
  "phone": "123123",
  "countryCode":"+84",
  "consumerAccountId": "testConsummerAccountId"
  "type": "consumer"
}
```

 * **registration sale account**

```javascript
post /accounts
```

```javascript
{
  "email":"codehubio@gmail.com",
  "password":"12345678", // must be more than 6
  "firstName":"hoa",
  "lastName":"nguyen",
  "type": "sale"
}
```

* **activate**

```javascript
post /accounts/activate/tokens?autoLogin=1 //autoLogin=1 means login token will be returned automatically without calling login api
````

```javascript
{
	"token":"12345678"
}

```
[example](https://github.com/siliconprime-hoanguyen/drivethrough/blob/master/examples/resgistration-autologin-1.md)

* **resend activate email**

```javascript
post /accounts/activate/sendemail
````

```javascript
{
	"email":"ancsd@fdsfds.com"
}
```

* **resend activate sms**

```javascript
post /accounts/activate/sendsms
````

```javascript
{
 "phone":"12345"
}
```

* **send reset password token via email or sms**

```javascript
post /auth/forgotpassword
````

```javascript
{
  "email":"ancsd@fdsfds.com", //if email provided, send via email
  "phone":"+8412321321" //if phone provided, send via sms
}
```


* **reset password with token**

```javascript
post /auth/resetpassword
````

```javascript
{
  "token":"79892047",
  "newPassword": "1234566"
}
```



* **login**

```javascript
post /auth/login
```

```javascript
{
  "password":"12345678",
  "uid":"+8412323232"
}
```

* **get account by account id (protected)**

```javascript
get /accounts/:accountId 
```

* **update account by account id (protected)**

```javascript
post /accounts/:accountId 
```
```javascript
{
  "firstName":"hoa",
  "lastName":"nguyen",
  "countryCode":"12",
  "phone":"4343"
  "status": "active", // ['active', 'inactive', 'banned']
  "userStatus": "online", // ['online', 'offline'],
  "serviceSettings": 
  {
     "pushMode": true, //or false, default true
     "smsMode": false // or true, default true
  }
}
```

```javascript
this api is for update general info of account so important fields like email, password, id will be **ignored**. to change those fields, please call other specific apis
```

* **change password (protected)**

```javascript
put /accounts/:accountId/password
```

```javascript
{
  "currentPassword":"xxxx",
  "newPassword": "xxxxx"
}
```

* **get link for upload profile picture**
```javascript
post /accounts/profile/getsignedasseturl
````

* **sample upload**

```javascript
http://dtapi-uploader.codehub.io/images/edf81ec0-1d11-11e7-9f71-b59ac7bddaa
````

***content-type: multipart/form-data***

```javascript
  file: 'Attach file content'
```

* **mark link as uploaded**

```javascript
post /asset/markuploaded/xxxxx
````

* **get public config for payment service (stripe)**

```javascript
get /payments/methods/config
```

