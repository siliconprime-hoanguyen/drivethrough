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

* **get default shop**
```javascript
get /shops/list/getdefault?defaultFor=usa&longitude=xxxx&latitdue=xxxx
```
