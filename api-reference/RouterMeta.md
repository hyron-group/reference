## **Table of contents**

### interface **RouterMeta**

-   **method**: string | Array< string >
-   **fontware**: Array < string >
-   **backware**: Array < string >
-   **plugins**: Array < string >
-   **handle**: function
-   **path**: string
-   **params**: string

# **Details**


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

Specifies the main-handler for this router. If this function is not set, Hyron will select the function inside this class that have the name the same name declared for this RouterMeta. This attribute has a higher priority

# var path

> ## **path** : string

Customize the path for this router instead of the default path. Use this attribute only when absolutely necessary, to ensure consistency and ease of editing later

# var params

> ## **params** : string

An attribute used by param-parser plugins allows to parse parameters from url strings following the path of this router

Use it with syntax : /:param1/:param2