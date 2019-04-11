# RouterMeta

#### interface **RouterMeta**

* [interface **RouterMeta**](routermeta.md#interface-routermeta-1)
* [var method](routermeta.md#var-method)
* [var fontware](routermeta.md#var-fontware)
* [var backware](routermeta.md#var-backware)
* [var plugins](routermeta.md#var-plugins)
* [var handle](routermeta.md#var-handle)
  * [**params**](routermeta.md#params)
  * [**return**](routermeta.md#return)
* [var path](routermeta.md#var-path)
* [var params](routermeta.md#var-params)
  * [Rule](routermeta.md#rule)

## interface **RouterMeta**

Is a metadata object contain information about routes

## var method

> ### **method** : string \| Array&lt; string &gt;

Specifies the methods that will be used to register the listener for this method. Include \( not case sensitive \) : GET, HEAD, POST, PUT, PATCH, ALL, PRIVATE

## var fontware

> ### **fontware** : Array&lt; string &gt;

Turn on registered fontware of a plugins by name, or turn off fontware of global plugins by marking with the character '!' in front of that name

## var backware

> ### **backware** : Array&lt; string &gt;

Turn on registered backware of a plugins by name, or turn off backware of global plugins by marking with the character '!' in front of that name

## var plugins

> ### **plugins** : Array&lt; string &gt;

Turn on registered a plugins by name, or turn off global plugins by marking with the character '!' in front of that name

## var handle

> ### **handle** : function

Specifies the main-handler for this router. If this function is not set, Hyron will select the function inside this class that have the name the same name declared for this RouterMeta. This attribute has a higher priority

#### **params**

* **argument** : The variables are input as a result of fontware plugins
* **this** : variable this with scope in this router

#### **return**

* any \| Promise &lt; any &gt; : result of logic block that could be used as input of backware plugins

## var path

> ### **path** : string

Customize the path for this router instead of the default path. Use this attribute only when absolutely necessary, to ensure consistency and ease of editing later

## var params

> ### **params** : string

An attribute used by param-parser plugins allows to parse parameters from url strings following the path of this router

Use it with syntax : /:param1/param2 ...

#### Rule

* var name start with ':' character
* params will be followed after the path
* The variable from the param should only have a depth of less than 5

