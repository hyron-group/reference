---
description: Used to pack routers that can be used by hyron to register routers
---

# HyronService

#### interface [**HyronService**](hyronservice.md#interface-HyronService)

* _static_ [**requestConfig**](hyronservice.md#function-requestconfig) \( \) : [ServiceMeta](servicesmeta.md)
* [**$config**](hyronservice.md) : object
* [**$requestConfig**](hyronservice.md#var-usdrequestconfig) : [RouterMeta](routermeta.md)
* [**$executer**](hyronservice.md#var-usdexecuter) : Function
* [**$eventName**](hyronservice.md#var-usdeventname) : string

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

```javascript
this.$config : object
```

return config of this service. It could be use inside every plugins & main-handler declared in this service

### var $requestConfig

```javascript
this.$requestConfig : RouterMeta
```

get to `requestConfig` **for this router**, or undefined if this executer has not been declared

### var $executer

```javascript
this.$executer : Function
```

get to `executer` **for this router**, or undefined if this executer has not been declared

### var $eventName

```javascript
this.$eventName : string
```

get to event name **for this router**, or undefined if this executer has not been declared

