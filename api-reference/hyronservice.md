---
description: Used to pack routers that can be used by hyron to register routers
---

# HyronService

#### interface [**HyronService**](hyronservice.md#interface-HyronService)

* _static_ [**requestConfig**](hyronservice.md#function-requestconfig) \( \) : [ServiceMeta](servicesmeta.md)
* [**$config**](hyronservice.md) : object
* \*\*\*\*[**$requestConfig**](hyronservice.md#var-usdrequestconfig) : [RouterMeta](routermeta.md)
* [**$executer**](hyronservice.md#var-usdexecuter) : Function
* \*\*\*\*[**$eventName**](hyronservice.md#var-usdeventname) : string

## Details

### inteface **HyronService**

Used to define a service that was controlled by Hyron. Create class that implement this, and declare it in hyron.enableServices to use



### function requestConfig

Used to declared information about method that could be used to register event listener

#### ★ Params

```javascript
static requestConfig() : ServicesMeta
```

\(empty\)

#### ★ **Return**

| type | description |
| :--- | :--- |
| [ServicesMeta](servicesmeta.md) | a object that contain descriptions about routes |



### var $config

return config of this service. It could be use inside every plugins & main-handler declared in this service

#### ★ Return

```javascript
this.$config : object
```

| t | description |
| :--- | :--- |
| object | An object contains settings for this service |



### var $requestConfig

get to `requestConfig` **for this router**, or undefined if this executer has not been declared

#### ★ Return

```javascript
this.$requestConfig : RouterMeta
```

| type | description |
| :--- | :--- |
| [RouterMeta](routermeta.md) | Descriptive information about this router, is declared in requestConfig |



### var $executer

get to `executer` **for this router**, or undefined if this executer has not been declared

#### ★ Return

```javascript
this.$executer : Function
```

| type | description |
| :--- | :--- |
| Function | The method will be used to register the router |



### var $eventName

get to event name **for this router**, or undefined if this executer has not been declared

#### ★ Return

```javascript
this.$eventName : string
```

| type | description |
| :--- | :--- |
| string | The event name is used to register this router. It corresponds to `eventName` displayed on the console |

