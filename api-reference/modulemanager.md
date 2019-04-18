---
description: 'Represents the hyron, containing the basic methods for running the application'
---

# ModuleManager

{% hint style="warning" %}
Note: this class is no longer used, instead you should use the @hyron/cli package to work with hyron more easily, and better support later
{% endhint %}

class **ModuleManager**

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

## Details

### class **ModuleManager**

Used to register & management elements in project, like instance, service, plugins, addons. It is base of Hyron Framework

### 

### function build

Used to run the application with a json build file. It supported by AppLoader

#### ★ params

```javascript
static build(path) : void
```

| name | type | description |
| :--- | :---: | :--- |
| path | string | referenced to [JSON build file](../json-build-file.md) from root |

### 

### function getInstance

Used to create a new instance, that can be used to create difference server. default server will listen on [http://localhost:3000](http://localhost:3000)

#### ★ P**arams**

```javascript
static gtInstance() : ModuleManager
```

\(empty\)

```typescript
static getInstance(baseUrl) : ModuleManager
```

| name | type | description |
| :--- | :--- | :--- |
| baseUrl | string | a url specified where the server will run on |

```typescript
static getInstance(port, host?, prefix?, protocol?): ModuleManager
```

| name | type | description |
| :--- | :--- | :--- |
| post | number | a free port. if port is `0`, server will listen on random available port. default is `3000` |
| host | string | host name or IP address of current machine. Default is `localhost` |
| prefix | string | a path to separate your routers, used to group routers into an instance. Default is empty |
| protocol | string | a protocol for this instance. default is http |

```javascript
static getInstance (serverConfig) : ModuleManager
```

| name | type | description |
| :--- | :--- | :--- |
| serverConfig | object | object contain server config. include : `protocol`, `host`, `port`, `prefix` |

#### ★ **Return**

| type | description |
| :--- | :--- |
| [ModuleManager](modulemanager.md#class-ModuleManager) | Current instance, that could be used to do something else |



### function getInstanceContainer

Used to get all app instance created. This feature usually used by addons and expanded module to handle a central problems

#### ★ Params

```javascript
static getInstanceContainer() : Array<ModuleManager>
```

\(empty\)

#### ★ R**eturn**

| type | description |
| :--- | :--- |
| Array&lt;[ModuleManager](modulemanager.md#class-ModuleManager)&gt; | a list of instances represent by baseUrl and instances |



### function setting

Used by modules from app, to make app more scalable & easy to management. setting will be overwrite onto setting value loaded by [appcfg.yaml](https://github.com/hyron-group/reference/tree/12153991129d1d848d668cf895f35a0448237f02/appcfg-file.md). Except lock field.

#### ★ **Params**

```typescript
setting(config) : void
```

| name | type | description |
| :--- | :--- | :--- |
| config | object | a description object contain config for this instance modules |
| config.environment | string | dev or product. if it is dev, program should collect problem, else it should to optimized for performance |
| config.timeout | number | expert timeout for router connection. default is 60s |
| config.style | string | style of uri path. Hyron support for 4 style, include : `camel`, `snake`, `lisp`, `lower`. default is lisp |
| config.secret | string | a private key that used to for encode a sensitive content |



### function getConfig

Retrieve config value for a key by name

#### ★ **Params**

```javascript
static getConfig(name, defaultValue?) : any
```

| name | type | description |
| :--- | :--- | :--- |
| name | string | config value or null if config not found. It allow support to browse child values by. example  : `mailer.auth.email` |
| defaultValue | any | value if do not found config by abort key |

#### ★ **Return**

| type | description |
| :--- | :--- |
| any | config data. described in appcfg file |



### function enableAddons

Used to register addons for this instance. A addons could have access to all the resources provided in this class via `this` args. It used to bring more power for Hyron to handle advanced problems. se to expand hyron or run cron jobs

#### ★ **Params**

```javascript
enableAddons ( paths ) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">nam</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">paths</td>
      <td style="text-align:left">object&lt;name,path&gt;</td>
      <td style="text-align:left">
        <p>list of linked addons referenced by path from root</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>path</b> (string) : link to addons hander from root</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>```javascript
enableAddons(packs) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">packs</td>
      <td style="text-align:left">object&lt;name,pack&gt;</td>
      <td style="text-align:left">
        <p></p>
        <p>List of packaged a&#x111;ons</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>pack</b> (ServicesMeta | UnofficialService) : handle package that used
            by hyron to register router</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### function enableGlobalAddons

Used to register global addons that have been called on each instance when it created

#### ★ **Params**

```javascript
enableGlobalAddons(paths) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">paths</td>
      <td style="text-align:left">object&lt;name,path&gt;</td>
      <td style="text-align:left">
        <p>list of linked addons referenced by path from root</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>path</b> (string) : link to addons hander from root</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>```javascript
enableGlobalAddons(packs) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">packs</td>
      <td style="text-align:left">object&lt;name,pack&gt;</td>
      <td style="text-align:left">
        <p></p>
        <p>List of packaged plugins</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>pack</b> (AddonsMeta) : handle package that used by hyron to register
            addon</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### function enablePlugins

This method used to register plugins with name provided. After plugins declared, it can be used inside your app by name

The name of the plugins needs to be consistent and easy to remember, so that it can be used easily

#### ★ **Params**

```javascript
enablePlugins(paths) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">paths</td>
      <td style="text-align:left">object&lt;name,path&gt;</td>
      <td style="text-align:left">
        <p>list of linked plugins referenced by path from root</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>path</b> (string) : link to addons hander from root</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>```javascript
enablePlugins(packs) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">packs</td>
      <td style="text-align:left">object&lt;name,pack&gt;</td>
      <td style="text-align:left">
        <p>list of packaged plugins</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>pack</b> (PluginsMeta) : handle package that used by hyron to register
            plugin</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### function enableService

Used to register routers for this instance. Service is a Object contain set of function that serve for a specific business purpose. To distinguish whether a package is a Hyron service or not based on the `requestConfig` method

#### ★ Params

```javascript
enableServices(paths) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">paths</td>
      <td style="text-align:left">object&lt;name,path&gt;</td>
      <td style="text-align:left">
        <p>list of linked services referenced by path from root</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>path</b> (string) : link to services package from root</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>```javascript
enableServices(packs) : void
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">handles</td>
      <td style="text-align:left">object&lt;name,pack&gt;</td>
      <td style="text-align:left">
        <p>list of packaged services</p>
        <ul>
          <li><b>name</b> (string) : name of addons</li>
          <li><b>pack</b> (HyronService | UnofficialService) : handle package that used
            by hyron to register router</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### function initServer

Used to custom server of this instance, and set it default listeners. By default, it called for the first time instance created with node http server.

#### ★ **Params**

```javascript
initServer(server) : void
```

| name | type | description |
| :--- | :--- | :--- |
| server | Server | server to handle client request and response. default is http.Server |

\*\*\*\*

### function setServer

This function could be used by addons to edit server for many instances

#### ★ **Params**

```javascript
static setServer(host, port, server) : void
```

| name | type | description |
| :--- | :--- | :--- |
| host | string | host name of specified instance |
| port | number | port number of specified instance |
| server | [Server](https://nodejs.org/api/http.html#http_class_http_server) | server to handle client request and response. default is http.Server |



### function startServer

Start this instance for listen client request

★ **Params**

```javascript
static startServer(callback) : void
```

| name | type | description |
| :--- | :--- | :--- |
| callback | function | event that will be called when server started |



