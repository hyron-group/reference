# param-parser

#### class **ModuleManager** \(Hyron\)

* [**build**](modulemanager.md#function-build) \( path \) : void
* _static_ [**getInstance**](modulemanager.md#function-getinstance-4-override)\( ... \) : [ModuleManager](modulemanager.md#class-modulemanager)
* [**setting**](modulemanager.md#function-setting) \( config \) : void
* _static_ [**getConfig**](modulemanager.md#function-getconfig) \( name, defaultValue \) : any
* _static_ [**getInstanceContainer**](modulemanager.md#function-getinstancecontainer) \( \) : Array&lt;[ModuleManager](modulemanager.md#class-modulemanager)&gt;
* [**enableAddons**](modulemanager.md#function-enableaddons-2-override) \( ... \) : void
* [**enableGlobalAddons**](modulemanager.md#function-enableglobaladdons-2-override) \( ... \) : void
* [**enablePlugins**](modulemanager.md#function-enableplugins-2-override) \( ... \) : void
* [**enableServices**](modulemanager.md#function-enableservices-2-override) \( ... \) : void
* [**initServer**](modulemanager.md#function-initserver) \( server \) : void
* _static_ [**setServer**](modulemanager.md#function-setserver) \( host, port, server \) : void
* [**startServer**](modulemanager.md#function-startserver) \( callback \) : void
* **host** : string
* **port** : number
* **prefix** : string
* **protocol** : string
* **app** : Server
* **addons** : AddonsManager
* **plugins** : PluginsManager
* **services** : ServicesManager

## class **ModuleManager**

Used to register & management elements in project, like instance, service, plugins, addons. It is base of Hyron Framework

## function build

> ### static **build** \( path \) : void

Used to build a Hyron app by that not through other javascript declaration. It supported by [AppLoader](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/buildIn-features/appLoader.core.md)

#### **params**

* **path** \( string \) : referenced to [JSON build file](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/buildIn-features/appLoader.core.md#Use-json-build-file) from root

## function getInstance \(+4 override\)

> ### _static_ **getInstance** \(\) : [ModuleManager](modulemanager.md#class-ModuleManager)

Used to create a new instance, that can be used to create difference server. default server will listen on [http://localhost:3000](http://localhost:3000)

#### **return**

* [ModuleManager](modulemanager.md#class-ModuleManager) : Current instance, that could be used to do something else

> ### _static_ **getInstance** \( baseURL : string \) : [ModuleManager](modulemanager.md#class-ModuleManager)

Create a new instance from specified port and current machine host

#### **params**

* **baseURL** \(string\) : specified url. example : [https://localhost:1234](https://localhost:1234)

#### **return**

* [ModuleManager](modulemanager.md#class-ModuleManager) : Current instance, that could be used to do something else

> ### _static_ **getInstance** \( port : number \) : [ModuleManager](modulemanager.md#class-ModuleManager)

[ModuleManager](modulemanager.md#class-ModuleManager) : Create a new instance from specified port and current machine host

#### **params**

* **port** \(number\) : a free port. if port is 0, server will listen on random available port

#### **return**

* Current instance, that could be used to do something else

> ### _static_ **getInstance**\( port, host, prefix, protocol \): [ModuleManager](modulemanager.md#class-ModuleManager)

[ModuleManager](modulemanager.md#class-ModuleManager) : Create a new instance with specified params

#### **params**

* **port** \( number \) : a free port. if port is 0, server will listen on random available port. default is '3000'
* **host** \( string - option \) : host name or ip address of current machine. Default is 'localhost'
* **prefix** \( string - option \) : a path to separate your routers, used to group routers into an instance. Default is empty
* **protocol** \( string - option \) : a protocol for this instance. default is 'http'

#### **return**

* [ModuleManager](modulemanager.md#class-ModuleManager) : Current instance, that could be used to do something else

> ### _static_ **getInstance** \(serverConfig\) : [ModuleManager](modulemanager.md#class-ModuleManager)

Create a new instance from a description object

#### **params**

* **serverConfig** : object contain server config. include : protocol, host, port, prefix

#### **return**

* [ModuleManager](modulemanager.md#class-ModuleManager) : Current instance, that could be used to do something else

## function getInstanceContainer

> ### _static_ **getInstanceContainer** \( \) : Array&lt;[ModuleManager](modulemanager.md#class-ModuleManager)&gt;

Used to get all app instance created. This feature usually used by addons and expanded module to handle a central problems

#### **return**

* Array &lt; [ModuleManager](modulemanager.md#class-ModuleManager) &gt; : A list of instances represent by baseUrl and instances

## function setting

> #### **setting** \( config \) : void

Used by modules from app, to make app more scalable & easy to management. setting will be overwrite onto setting value loaded by [appcfg.yaml](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/appcfg-file.md). Except lock field.

All default key :

* **environment** \( string \) : dev or product. if it is dev, program should collect problem, else it should to optimized for performance
* **timeout** \( number \) : expert timeout for router connection. default is 60s
* **style** \( string \) : style of uri path. Hyron support for 4 style, include : _camel_ \( likeThis \), _snake_ \( like\_this \), _lisp_ \( like-this \), _lower_ \( likethis \). default is lisp.
* **secret** : a private key that used to for encode a sensitive content

#### **params**

* **config** \( object \) : a description object contain config for this instance modules

## function getConfig

> ### _static_ **getConfig** \( name, defaultValue \) : any

Retrieve config value for a key by name

#### **params**

* **name** \( string \) : config value or null if config not found. It allow support to browse child values, separated by '.' character
* **defaultValue** \( any \) : value if do not found config by abort key

#### **return**

* any : config data

## function enableAddons \(+2 override\)

> ### **enableAddons** \( addonsPaths \) : void

Used to register addons for this instance. A addons could have access to all the resources provided in this class via `this` args. It used to bring more power for Hyron to handle advanced problems

If you want to build your own addons, see this topic : [how to build a addons ? ](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/api-reference/addons-development/README.md)

#### **params**

* **addonsPaths** \( Object &lt; name, path &gt; \) : list of linked addons referenced by path from root
  * **name** \( string \) : name of addons. It used to load configs
  * **path** \( string \) : link to addons handler. It should be start at root dir

> ### **enableAddons** \( addonsList \) : void

Used to register addons for this instance by addons handler function.

#### **params**

* **addonsList** \( Object &lt; name, [AddonsMeta](../../api-reference/addonsmeta.md#function-handle) &gt; \) : list of addons called on this instance
  * **name** \(string\) : name of addons. It used to import configs
  * **handler** \( [AddonsMeta](../../api-reference/addonsmeta.md#function-handle) \) : handler for addons

## function enableGlobalAddons \(+2 override\)

> ### **enableGlobalAddons** \( addonsPaths \) : void

Used to register global addons that have been called on each instance when it created

If you want to build your own addons, see this topic : [how to build a addons ? ](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/api-reference/addons-development/README.md)

#### **params**

* **addonsPaths** \( Object &lt; name, path &gt; \) : list of linked addons referenced by path from root
  * **name** \( string \) : name of addons. It used to load configs
  * **path** \( string \) : link to addons handler. It should be start at root dir

> ### **enableGlobalAddons** \( addonsList \) : void

Used to register global addons by addons handler function.

#### **params**

* **addonsList** \( Object &lt; name, [AddonsMeta](../../api-reference/addonsmeta.md#function-handle) &gt; \) : list of addons called on this instance
  * **name** \(string\) : name of addons. It used to import configs
  * **handler** \( [AddonsMeta](../../api-reference/addonsmeta.md#function-handle) \) : handler for addons

## function enablePlugins \(+2 override\)

> ### **enablePlugins** \( pluginsPaths \) : void

This method used to register plugins with name provided. After plugins declared, it can be used inside your app by name.

You should declare the names of the plugins that match the name provided by the manufacturer, unless the name is identical, or you want a more memorable name :\)\)

In addition to using plugins provided by third parties, you can also create plugins for yourself. See more in [How to create a plugins ?](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/api-reference/plugins-developent/README.md) topic

#### **params**

* **pluginsPaths** \( Object &lt; name, path &gt; \) : object declare plugins
  * **name** \( string \) : name of this plugins. It used to load config
  * **path** \( string \) : link to plugins metadata. It should be start at root dir

> ### **enablePlugins** \( pluginsList \) : void

Register plugins by directly by PluginsMeta. PluginsMeta is a object contain functions that will be called before \(fontware\) or after \(backware\) main-handler.

#### **params**

* **pluginsList** \( Object &lt; name, [PluginsMeta](../../api-reference/pluginsmeta.md) &gt; \) : object declare plugins
  * **name** \( string \) : name of this plugins. It used to load config
  * **PluginsMeta** \( object \) : link to plugins metadata. It should be start at root dir. To find more about plugins structure, please visit : [PluginsMeta](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/api-reference/PluginsMeta/README.md)

## function enableServices \(+2 override\)

> ### **enableServices** \( servicePaths \) : void

Used to register routers for this instance. Service is a Object contain set of function that serve for a specific business purpose. To distinguish whether a package is a Hyron service or not based on the requestConfig method. To know how to develop a service. Please visit topic : [how to build a service ?](https://github.com/hyron-group/reference/tree/94b6e23bec0221c1acba3e4016612b6849483786/api-reference/service-development/README.md)

**params**

* **modulePaths** \( Object &lt; name, path &gt; \) : The set of functions is encapsulated to handle specific functions. Which will become the router
  * **name** \( string \) : name o module
  * **path** \( string \) : link to service metadata. It should be start at root dir

> ### **enableServices** \( serviceList \) : void

Used to register routers for this instance directly by Hyron service

#### **params**

* **module** \( Object &lt; name, serviceMeta &gt; \) : The set of functions is encapsulated to handle specific functions. Which will become the router
  * **name** \( string \) : name o module
  * **serviceMeta** \( [HyronService](../../api-reference/hyronservice.md) \| [UnofficialService](../../api-reference/unofficialservice.md) \) : a packet of functions and it config

## function initServer

> ### **initServer** \( server \) : void

Used to custom server of this instance, and set it default listeners. By default, it called for the first time instance created with node http server.

#### **params**

* **server** \( [Server](https://nodejs.org/api/http.html) \) : server to handle client request and response. default is http.Server

## function setServer

> ### _static_ **setServer** \( host, port, server \) : void

This function could be used by addons to edit server for many instances

#### **params**

* **host** \( string \) : host name of specified instance
* **port** \( number \) : port number of specified instance
* **server** \( [Server](https://nodejs.org/api/http.html) \) : server to handle client request and response. default is http.Server

## function startServer

> ### startServer \( callback \) : void

Start this instance for listen client request

**params :**

* **callback** \( [function](https://nodejs.org/api/net.html#net_event_listening) \) : event when server started

