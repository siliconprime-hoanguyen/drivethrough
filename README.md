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

* **get shop list**
```javascript
get /shops/list/get?zipCode=12323
```

* **get default shop by country**
```javascript
get /shops/list/getdefault?defaultFor=USA
```

* **get default shop by location**
```javascript
get /shops/list/getdefault?longitude=xxxx&latitude=xxxx
```
