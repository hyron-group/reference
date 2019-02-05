## **Table of contents**

### interface **HyronService**

-   *static* **requestConfig** ( ) : Object < name, RouterMeta | method >

### interface **RouterMeta**

-   **method**: string | Array< string >
-   **fontware**: Array < string >
-   **backware**: Array < string >
-   **plugins**: Array < string >
-   **handle**: function
-   **path**: string
-   **params**: string

### interface **UnofficialService**
- **handle** ( Server, cfg ) : void

# **Details**

## inteface **HyronService**

Used to define a service that was controlled by Hyron. Create class that implement this, and declare it in hyron.enableServices to use

# function requestConfig

> ## *static* **requestConfig** ( ) :  Object < name, RouterMeta | method >

Used to declared information about method that could be used to register event listener

This function makes it possible to describe in a more centralized and synchronized manner, and can be implemented by many different languages

### **return**

 - Object < name, meta | method > : a object that contain descriptions about routes
    - **name** ( string ) : name of method declared bellow, that could be use to register a event. By default, hyron will take that name and register it as a child-path for this service
    - **meta** ( RouterMeta ) : a object that description detail about this router
    - **method** ( RouterMeta.method ) : a method or a list of method that could be used to register event for this method

---

## interface **RouterMeta**

Is a metadata object contain information about routes

# var method

> ## **method** : string | Array< string >

Specifies the methods that will be used to register the listener for this method. Include ( not case sensitive ) : GET, HEAD, POST, PUT, PATCH, ALL

# var fontware

> ## **fontware** : Array< string >

Turn on registered fontware of a plugins by name, or turn off fontware of global plugins by marking with the character '!' in front of that name

# var backware

> ## **backware** : Array< string >

Turn on registered backware of a plugins by name, or turn off backware of global plugins by marking with the character '!' in front of that name

# var plugins

> ## **plugins** : Array< string >

Turn on registered a plugins by name, or turn off global plugins by marking with the character '!' in front of that name

# var handle

> ## **handle** : function

Specifies the main-handler for this router. If this function is not set, the hyron will select the function inside this class that have the name the same name declared for this RouterMeta. This attribute has a higher priority

# var path

> ## **path** : string

Customize the path for this router instead of the default path. Use this attribute only when absolutely necessary, to ensure consistency and ease of editing later

# var params

An attribute used by param-parser plugins allows to parse parameters from url strings following the path of this router

Use it with syntax : /:param1/:param2