# drivethrough api

## server
- intial dev: http://dtapi.codehub.io


## protected api must be called with header

```javascript
{
	Authorization: Bearer xxxxxxx //xxxxxxx is the token received when calling login api successfully.
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

* **create order**
```javascript
post /orders
```
```javascript
{
  accountId: 'testId', //generated random from app and must be unique per installation of the app.
  shopId:'58d0a754826d4f21b88fefae',
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
