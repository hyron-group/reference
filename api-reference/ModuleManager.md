## **Table of contents**

### class **ModuleManager** \(hyron\)

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
-   **host** : string
-   **port** : number
-   **prefix** : string
-   **protocol** : string
-   **app** : Server
-   **addons** : AddonsManager
-   **plugins** : PluginsManager
-   **services** : ServicesManager

# **Details**

## class **ModuleManager**

Used to register & management elements in project, like instance, service, plugins, addons. It is base of Hyron Framework

# function getInstance (+4 override)

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

> ## _static_ **getInstance** (serverConfig) : ModuleManager

Create a new instance from a description object

### **params**

-   **serverConfig** : object contain server config. include : protocol, host, port, prefix

---

# function getInstanceContainer

> ## _static_ **getInstanceContainer** \( \) : Array<ModuleManager>

Used to get all app instance created. This feature usually used by addons and expanded module to handle a central problems

### **return**

Array< ModuleManager > : A list of instances represent by baseUrl and instances

---

# function setting

> ### **setting** \( config \) : void

Used by modules from app, to make app more scalable & easy to management. setting will be overwrite onto setting value loaded by appcfg.yaml. Except lock field.

All default key :

-   **environment** \( string \) : dev or product. if it is dev, program should collect problem, else it should to optimized for performance
-   **timeout** \( number \) : expert timeout for router connection. default is 60s
-   **style** \( string \) : style of uri path. Hyron support for 4 style, include : **_camel_** \( likeThis \), **_snack_** \( like\*this \), \*\*\_lisp**\* \( like-this \), **_lower_\*\*\(likethis\).
-   **_secret_** : a private key that used to for encode a sensitive content

### **params**

-   **config** \( object \) : a description object contain config for this instance modules

---

# function getConfig

> ## _static_ **getConfig** \( name \) : any

Retrieve config value for a key by name

### **params**

-   **name** \( string \) : config value or null if config not found

---

# function enableAddons (+2 override)

> ## **enableAddons** \( addonsPaths \) : void

Used to register addons for this instance. A addons could have access to all the resources provided in this class via 'this' args. It used to bring more power for hyron to handle advanced problems

If you want to build your own addons, see this topic : [how to build a addons ? ](addons-development/overview.md)

### **params :**

-   **addonsPaths** \( Array< name, path > \) : list of linked addons referenced by path from root
    -   **name** ( string ) : name of addons. It used to load configs
    -   **path** ( string ) : link to addons handler. It should be start at root dir

---

> ## **enableAddons** \( addonsList \) : void

Used to register addons for this instance by addons handler function.

### **params :**

-   **addonsList** \( Array< name, handler > \) : list of addons called on this instance
    -   **name** (string) : name of addons. It used to import configs
    -   **handler** ( function (cfg) -> void ) : handler for addons

---

# function enablePlugins (+2 override)

> ## **enablePlugins** \( pluginsPaths \) : void

This method used to register plugins with name provided. After plugins declared, it can be used inside your app by name.

You should declare the names of the plugins that match the name provided by the manufacturer, unless the name is identical, or you want a more memorable name :\)\)

In addition to using plugins provided by third parties, you can also create plugins for yourself. See more in [How to create a plugins ?](./plugins-developent/README.md) topic

### **params**

-   **pluginsPaths** \( Object< name, path > \) : object declare plugins
    -   **name** ( string ) : name of this plugins. It used to load config
    -   **path** ( string ) : link to plugins metadata. It should be start at root dir

---

> ## **enablePlugins** \( pluginsList \) : void

Register plugins by directly by PluginsMeta. PluginsMeta is a object contain functions that will be called before (fontware) or after (backware) main-handler.

### **params**

-   **pluginsList** \( Object< name, PluginsMeta > \) : object declare plugins
    -   **name** ( string ) : name of this plugins. It used to load config
    -   **PluginsMeta** ( object ) : link to plugins metadata. It should be start at root dir. To find more about plugins structure, please visit : [PluginsMeta](./PluginsMeta)

---

# function enableServices (+2 override)

> ## **enableServices** \( servicePaths \) : void

Used to register routers for this instance. Service is a Object contain set of function that serve for a specific business purpose. To distinguish whether a package is a hyron service or not based on the requestConfig method. To know how to develop a service. Please visit topic : [how to build a service ?](./service-development/README.md)

#### **params**

-   **modulePaths** \( Object< name, path > \) : The set of functions is encapsulated to handle specific functions. Which will become the router
    -   **name** \( string \) : name o module
    -   **path** \( string \) : link to service metadata. It should be start at root dir

---

> ## **enableServices** \( serviceList \) : void

Used to register routers for this instance directly by hyron service

### **params**

-   **module** \( Object< name, path > \) : The set of functions is encapsulated to handle specific functions. Which will become the router
    -   **name** \( string \) : name o module
    -   **module** \( HyronService | UnofficialService \) : a packet of functions and it config

---

# function initServer

> ## **initServer** ( server ) : void

Used to custom server of this instance, and set it default listeners. By default, it called for the first time instance created with node http server.

### **params**

-   **server** ( Server ) : server to handle client request and response. default is http.Server

---

# function setServer

> ## *static* **setServer** ( host, port, server ) : void

This function could be used by addons to edit server for many instances

### **params**

- **host** ( string ) : host name of specified instance
- **port** ( number ) : port number of specified instance
- **server** ( Server ) : server to handle client request and response. default is http.Server

# function startServer

> ## startServer \( callback \) : void

Start this instance for listen client request

#### **params :**

-   **callback** \( function \) : event when server started
