# drivethrough api

## server
- intial dev: http://dtapi.codehub.io

## test
http://test.codehub.io


## protected api must be called with header

```javascript
{
   Authorization: Bearer xxxxxxx //xxxxxxx is the token received when calling login api successfully.
}
```

### registration & authentication

* **registration**
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
post /asset/markuploaded/58eaf2b00989830044484950
````

## shop 

* **get shop list by zip code**
```javascript
get /shops/list/get?zipCode=12323&skip=0&limit=10
```

* **get shop list by location**
```javascript
get /shops/list/get?longitude=xxxx&latitude=xxxx&skip=0&limit=10
```

* **get default shop by country**
```javascript
get /shops/list/getdefault?defaultFor=USA
```

* **get default shop by location**
```javascript
get /shops/list/getdefault?longitude=xxxx&latitude=xxxx
```
## category

* **get category list by shop id**
```javascript
get /categories/list/get?shopId=1234&skip=0&limit=10
```
## product

* **term suggestion for searching product**
```javascript
get /products/search/suggest?term=1232
```

* **full text search for product**
```javascript
get /products/search/query?term=1232&skip=0&limit=10
```

* **get popular keywords (sort by hit count)**
```javascript
get /products/search/keywords?skip=0&limit=10
```

* **get product list by shop id**
```javascript
get /products/list/get?shopId=1234&skip=0&limit=10
```

* **get product list by shop id and category ids**
```javascript
get /products/list/get?shopId=1234&categoryIds=12,34,56&skip=0&limit=10 //get products from 3 category id 12, 34, 56
```
* **get product by id**
```javascript
get /products/:productId
```

* **add product to favourite list**
```javascript
post /products/addtofavourite/:productId
```
```javascript
{
  accountId: 'testId', //generated random from app and must be unique per installation of the app.  
}
```
* **remove product frome favourite list**
```javascript
post /products/removefromfavourite/:productId
```
```javascript
{
  accountId: 'testId', //generated random from app and must be unique per installation of the app.  
}
```

* **get favourite list by account id**
```javascript
get /products/getFavourites/:accountId?skip=0&limit=3&limitProduct=10
```
* **get favourite list by account id and shop id**
```javascript
get /products/getfavouritesbyshopid/:accountId/:shopId?skip=0&limit=3
```

* **get favourite list by account id and product id**
```javascript
get /products/getfavouritebyproductid/:accountId/:productId
```


## order

* **create order (or initially add products to cart) for anonymous user** 

**please note that one accountId can only have one active cart for each shop at a moment**
```javascript
post /orders
```
```javascript
{
  accountId: 'testId', //generated random from app and must be unique per installation of the app.
  shopId:'58d0a754826d4f21b88fefae',
  description: 'lorem ipsum',
  details:[{
  	_id:'58d0a7c6826d4f21b890882a',
  	quantity: 4
  },
  {
  	_id:'58d0a7c6826d4f21b8908830',
  	quantity: 4
  }]
}
```

* **adjust quantity for anonymous user**
```javascript
post /orders/adjustQuantity/:orderId
```
```javascript
{
  productId: '12321',
  quantity: 23
}
```

* **get active cart for account id and shop id**
```javascript
get /orders/list/getactivecart?shopId=12312321&accountId=testId
```

* **get upcoming order account id**
```javascript
get /orders/list/getupcoming?accountId=testId
```

* **charge order**
```javascript
post /orders/charge/:orderId
```
```javascript
{
  cardId:"12321321",
  pickupOn: "2017-01-20T08:35:30.231Z"
}
```

* **place order**
```javascript
post /orders/place/:orderId
```
```javascript
{
   pickupOn: "2017-01-20T08:35:30.231Z"
}
```



## payment


* **add stripe card token**
```javascript
post /payments/methods/add
```
```javascript
{
  tokenId: 'stripetoken',
  accountId: 'auniqueid'
}
```

* **remove stripe card from account**
```javascript
delete /payments/methods/remove
```
```javascript
{
  cardId: 'stripecardid',
  accountId: 'auniqueid'
}
```

* **get card list by account id**
```javascript
get /payments/methods/list?accountId=test
```

* **get public config for payment service (stripe)**

```javascript
get /payments/methods/config
```

