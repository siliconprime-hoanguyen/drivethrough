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
  "countryCode":"+84"
}
```
* **activate**
```javascript
post /accounts/activate/tokens
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

* **charge order**
```javascript
post /orders/charge/:orderId
```
```javascript
{
  "cardId":"12321321"
}
```

* **place order**
```javascript
post /orders/place/:orderId
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
* **get card list by account id**
```javascript
get /payments/methods/list?accountId=test
```

* **get public config for payment service (stripe)**

```javascript
get /payments/methods/config
```

