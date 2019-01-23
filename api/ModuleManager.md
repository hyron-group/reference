# api-reference

## **Table of contents**

### class **ModuleManager** \(hyron\)

Used to register & management elements in project, like instance, service, plugins, addons. It is base of Hyron Framework

-   **build** \( path \) : void
-   _static_ **getInstance**\( ... \) : ModuleManager
-   **setting** \( config \) : void
-   _static_ **getConfig** \( name \) : any
-   _static_ **getInstanceContainer** \( \) : Array\<ModuleManager\>
-   **enableAddons** \( ... \) : void
-   **enablePlugins** \( ... \) : void
-   **enableServices** \( ... \) : void
-   **initServer** \( server \) : void
-   _static_ **setServer** ( host, port, server ) : void
-   **startServer** \( callback \) : void
-   _prototype_.**host** : string
-   _prototype_.**port** : number
-   _prototype_.**prefix** : string
-   _prototype_.**protocol** : string
-   _prototype_.**app** : Server
-   _prototype_.**addons** : AddonsManager
-   _prototype_.**plugins** : PluginsManager
-   _prototype_.**services** : ServicesManager

## **Details**

# function getInstance (+4)

> ## _static_ **getInstance** () : ModuleManager

Used to create a new instance, that can be used to create difference server. default server will listen on http://localhost:3000

---

> ## _static_ **getInstance** \( baseURL : string \) : ModuleManager

Create a new instance from specified port and current machine host

### **params**

-   **baseURL** (string) : specified url. example : https://localhost:1234

---

> ## _static_ **getInstance** ( port : number ) : ModuleManager

Create a new instance from specified port and current machine host

### **params**

-   **port** (number) : a free port. if port is 0, server will listen on random available port

---

> ## _static_ **getInstance**( port, host, prefix, protocol ): ModuleManager

Create a new instance with specified params

### **params**

-   **port** ( number ) : a free port. if port is 0, server will listen on random available port. default is '3000'
-   **host** ( string - option ) : host name or ip address of current machine. Default is 'localhost'
-   **prefix** ( string - option ) : a path to separate your routers, used to group routers into an instance. Default is empty
-   **protocol** ( string - option ) : a protocol for this instance. default is 'http'

---

> ### **setting** \( config \) : void

Used to config app and installed plugins. If appcfg.ini declared. all config will be append inside

All default key supported :

-   **isDevMode** \( boolean \) : true if hyron collect & show logs. default is **true**
-   **enableRESTFul** \( boolean \) : true if you want turn all route become rest. You also turn of it in each route. default is **false**
-   **secret** \( string \) : is special key from appcfg.ini or random key it it not set yet
-   **timeout** \( number \) : expert timeout for router connection. default is 60s
-   **poweredBy** \( string \) : provider name. default is "hyron"
-   **style** \( string \) : style of uri path. Hyron support for 4 style, include : camel \( likeThis \), snack \( like_this \), lisp \( like-this \), lower\(likethis\).

### **params :**

-   **config** \( object \) : config of app or it plugins

> #### _static_ **getConfig** \( name \) : string \| object&lt;?&gt;

Used to get config of app or installed plugins by name

**params :**

-   **name** \(string\) : config item name or plugin name

> #### **enableAddons** \(addonsList\) : void

Used to register addons for this instance. All addons have access to all the resources provided in this class.

If you want to build your own addons, see this topic : [how to build a addons ? ](addons-development/overview.md)

**params :**

-   addonsList \( Array \) : list of addons called on this instance

> #### _static_ **getInstanceContainer** \(\) : Object

Used to get all app instance created

> #### **enablePlugins** \( pluginsList \) : void

This method used to register plugins with name provided. After plugins declared, it can be used inside your app by name.

You should declare the names of the plugins that match the name provided by the manufacturer, unless the name is identical, or you want a more memorable name :\)\)

In addition to using plugins provided by third parties, you can also create plugins for yourself. See more in [How to create a plugins ?](https://github.com/hyron-group/reference/tree/3437eeb47ffad09baf95272f73ae3e71764436ce/plugins-developemt/overview/README.md) topic

**params**

-   **pluginsList** \( object { name : meta } \) : object declare plugins

#### **params :**

> #### **enableServices** \( moduleList \) : void

Register main handle \(logic of routers\)

#### **params :**

-   **module** \( object {**name** : **module**} \) : The set of functions is encapsulated to handle specific functions. Which will become the router
    -   name \( **string** \) : name o module
    -   module \( **string** \| **HyronClass** \) : a packet of functions and it config

> #### startServer \( callback \) : void

Start this instance for listen client request

#### **params :**

-   **callback** \( function \) : event when server started

### class **AbstractRouters**

Note : this class is only descriptive, you do not need to implement it to use it

This class is base element of hyron framework, to declare routers, setup plugins, etc

To used it, include it in \[_enableServices\(\)_\]\(\#\#\#-**enableServices**-\(-moduleList-\)-:-void\) method

> #### _static_ **requestConfig** \(\) : Object

Used to description about route that server will listen into.

#### **Return**

object { method_name : meta }

-   **method_name** \( string \) : name of handle method declared in this class
-   **meta** \( string \| object \| Array. \) : declare info about this router
    -   \( **string** \) : method name, include : get, head, post, put, delete, patch, all, private
    -   \(\*\*Array.\*\*\) : set of method name like about
    -   \(**object**\) : object description detail about route
        -   **method** \( string\|Array \) : like about
        -   **handle** \( function \) : handle function if handle method is not defined
        -   **fontware** \( Array. \) : list of enable or disable fontware by name
        -   **backware** \( Array. \) : list of enable or disable backware by name
        -   **plugins** \( Array. \) : list of enable or disable plugins by name. It is an acronym for fontware and backware
        -   **path** \( string \) : custom uri path for this router. If it not defined, a router with name _/method_name_ will be registered
        -   **enableREST** \( boolean \) : true if method is REST API, then handle function argument at index 0 will be pass path param.

### class **HTTPMessage**

**Parent : Error**

This class used to interrupt current flow and throw a http message to client

> #### **constructor** \( code, message \)

Used to create a Error instance description about your http error

#### **params :**

-   **code** \( Number \) : it can be a HTTP error code from 1XX - 5XX. You can used class StatusCode if you don't remember error code
-   **message** \( String \) : string description for this error

### class **StatusCode**

contain HTTP code from 1XX to 5XX with friendly name. Used it with class HTTPMessage to make your code more readable

### object **path**

used to get uri path of a route that hyron manages

> #### **build** \( baseURL, eventName, executer \)

Used to add a router into scope that used for future searches. Hyron will auto call this function when route loaded. So, you can search it route inside your functions

**params :**

-   **baseURL** \( string \) : base url of routes, like [http://example.com](http://example.com)
-   **eventName** \( string \) : is route path
-   **executer** \( function \) : is main handler

> #### **findURL** \( query \)

Used to get url of a router. It allow search by a part of string url, or by main handle function

**params :**

-   **query** \( string \| function \) : key used to search url path. After search for first time, it will be cache for future search
