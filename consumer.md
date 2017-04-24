## consumer

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
get /products/search/query?term=1232&shopId=xxx&skip=0&limit=10
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

* **get category by id**
```javascript
get /categories/:categoryId
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
[example](https://github.com/siliconprime-hoanguyen/drivethrough/blob/master/examples/get_favourite_list.md)

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

* **get past order account id**

```javascript
get /orders/list/getpast?accountId=testId
```

* **charge order**

```javascript
post /orders/charge/:orderId
```
* **refund order**

```javascript
post /orders/refund/:orderId
```

```javascript
{

  details:[{
  	_id:'58d0a7c6826d4f21b890882a',
  	quantity: 4 //quantity to refund
  },
  {
  	_id:'58d0a7c6826d4f21b8908830',
  	quantity: 4 //quantity to refund
  }]
}
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

