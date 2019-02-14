## **Table of contents**

### interface [**HyronService**](#interface-HyronService)

-   *static* [**requestConfig**](#function-requestconfig) ( ) : Object < name, [RouterMeta](./RouterMeta) | [RouterMeta.method](./RouterMeta#var-method) >
-   [**$config**]() : object

# inteface **HyronService**

Used to define a service that was controlled by Hyron. Create class that implement this, and declare it in Hyron.enableServices to use

# function requestConfig

> ## *static* **requestConfig** ( ) :  Object < name, [RouterMeta](./RouterMeta) | method >

Used to declared information about method that could be used to register event listener

This function makes it possible to describe in a more centralized and synchronized manner, and can be implemented by many different languages. It also have special attribute for config all router is ``$all`` with properties inside like the same

### **return**

 - Object < name, [RouterMeta](./RouterMeta.md) | [RouterMeta.method](./RouterMeta#var-method) > : a object that contain descriptions about routes
    - **name** ( string ) : name of method declared bellow, that could be use to register a event. By default, Hyron will take that name and register it as a child-path for this service
    - **meta** ( [RouterMeta](./RouterMeta.md) ) : a object that description detail about this router
    - **method** ( [RouterMeta.method](./RouterMeta#var-method) ) : a method or a list of method that could be used to register event for this method

---

# var $config

> ## this.**$config** : object

return config of this service. It could be use inside every plugins & main-handler declared in this service