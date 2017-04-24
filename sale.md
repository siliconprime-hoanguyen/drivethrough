## sale

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

* **get default shop for sale** (protected)

```javascript
get /sale/shops/list/getdefault
```

* **get product list by shop id**
```javascript
get /sale/products/list/get?shopId=1234&skip=0&limit=10
```

* **create product**
```javascript
post /products
```

```javascript
{
    "name": "test product name 1",
    "description": "test product name 1",
    "originalPrice": 10,
    "currentPrice": 5,
    "shopId":"58cf5589354173d077b3e143",
    "categoryIds": "58cf4b6d8433d1c962522ee6,58cf4b6d8433d1c962522eda",
    "sku":"12321",
    "shelfNumber": "23",
    "lineNumber":"33",
    "published": true 
}
```

* **get product list by shop id and category ids**
```javascript
get /sale/products/list/get?shopId=1234&categoryIds=12,34,56&skip=0&limit=10 //get products from 3 category id 12, 34, 56
```
* **get product by id**
```javascript
get /sale/products/:productId
```

* **get category by id**
```javascript
get /sale/categories/:categoryId
```

* **get category list by shop id**
```javascript
get /sale/categories/list/get?shopId=1234&skip=0&limit=10
```

* **update category**
```javascript
post /categories/:categoryId
```
```javascript
{
  name: 'new category name',
  description: 'new category description',
  status: 'active' //or inactive
}
```


* **get signed url to upload image to category**
```javascript
post /categories/getSignedAssetUrl/:categoryId
```

* **assign a manager to shop** (protected)

```javascript
post /admin/shops/:shopId/addManager
```

```javascript
{
  accountId: 'sale account id'
}
```
## order
 **get upcoming order by shop id**

```javascript
get sale/orders/list/getupcoming/:shopId
```

**get past orders by shop id**

```javascript
get sale/orders/list/getpast/:shopId
```
