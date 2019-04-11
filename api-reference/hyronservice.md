# HyronService

#### interface [**HyronService**](hyronservice.md#interface-HyronService)

* _static_ [**requestConfig**](hyronservice.md#function-requestconfig) \( \) : Object &lt; name, [RouterMeta](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta/README.md) \| [RouterMeta.method](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta/README.md#var-method) &gt;
* [**$config**](hyronservice.md) : object

## inteface **HyronService**

Used to define a service that was controlled by Hyron. Create class that implement this, and declare it in Hyron.enableServices to use

## function requestConfig

> ### _static_ **requestConfig** \( \) :  Object &lt; name, [RouterMeta](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta/README.md) \| method &gt;

Used to declared information about method that could be used to register event listener

This function makes it possible to describe in a more centralized and synchronized manner, and can be implemented by many different languages. It also have special attribute for config all router is `$all` with properties inside like the same

#### **return**

* Object &lt; name, [RouterMeta](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta.md) \| [RouterMeta.method](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta/README.md#var-method) &gt; : a object that contain descriptions about routes
  * **name** \( string \) : name of method declared bellow, that could be use to register a event. By default, Hyron will take that name and register it as a child-path for this service
  * **meta** \( [RouterMeta](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta.md) \) : a object that description detail about this router
  * **method** \( [RouterMeta.method](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/RouterMeta/README.md#var-method) \) : a method or a list of method that could be used to register event for this method

## var $config

> ### this.**$config** : object

return config of this service. It could be use inside every plugins & main-handler declared in this service

