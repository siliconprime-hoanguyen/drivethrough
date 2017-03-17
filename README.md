# drivethrough api

## protected api must be called with header

```javascript
{
	Authorization: Bearer xxxxxxx //xxxxxxx is the token received when calling login api successfully.
}
```

## shop 

* **get shop list**
```javascript
get /shops?uuid=12323
```
