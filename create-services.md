---
description: >-
  Service is the smallest processing unit, used to handle a specific business
  logic
---

# Create Services

{% hint style="info" %}
Hyron encourages you to build [Microservice Architecture](https://microservices.io/) applications that bring great benefits to your application
{% endhint %}

## Why ?

* Easy to expand
* Easy to understand
* Easy to reuse

## Usage

### 1. Initialization service

{% code-tabs %}
{% code-tabs-item title="Using @hyron/cli" %}
```bash
hyron init services
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Structure" %}
```text
service-name
  ├── controller/     - contain processing logic for this service
  ├── model/          - contain contains data models, methods for communicating with the database
  ├── index.js        - contains interfaces for use by other services
  ├── router.js       - contains interfaces for use by Hyron to register to the service
  ├── appcfg.yaml     - contains the configuration used for this service
  ├── package.json    - contains the basic information of this service used for the npm registry
  └── readme.md       - contains descriptions for this service
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 2. Define controller

{% hint style="info" %}
Hyron allows turning from a **normal function to a router**. Allows you to **reuse** better, and allows **testing**, extremely friendly with beginner
{% endhint %}

This allows you to easily switch from a normal controller to a router. Example

{% code-tabs %}
{% code-tabs-item title="./controller/UserManager.js" %}
```javascript
const serModel = require('../model/UserModel'); // mongoose model

module.export = class UserManager {
    ...
    // create new user & save to mongo database
    async createUser(name, age, location){
        var newUser = await new UserModel({name, age, location});
        newUser.save((err)=>{
            if(err!=null){
                // this is a global Error object of hyron that used to break flow to return to client a message with a status code
                throw new HTTPMessage(
                    StatusCode.INTERNAL_SERVER_ERROR,
                    err.message
                )
            }
        });
        // return a object to response json data
        return newUser;
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="./model/userModel.js" %}
```javascript
const model = require('mongoose');

const UserModel = new model("user_info", {
    name : String,
    age : Number,
    location : String
});

module.export = UserModel;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Note

* The **processing functions** used to register a router are also called `executer`
* The **executer input and output** can be customized or processed before being transferred to the client using plugins
* **executer belongs to the logical layer**, should only contain processing logic for a business
* **executer** can share `this` variable with [plugins](create-plugins.md)

![sharing mechanism &apos;this&apos; variable allows communication between modules](.gitbook/assets/this-scope.png)

Here are some of the default properties of **`this`**, check out [HyronService](api-reference/hyronservice.md) for more info

| Properties | Type | Description |
| :--- | :--- | :--- |
| $executer | function | A function handler, which can be used for plugins to use in analysis |
| $eventName | string | The name of the event used to register the router |
| $requestConfig | string \| object | settings for this router, are declared in `requestConfig` |
| $config | object | contains settings for this module, declared in `appcfg.yaml` file |

### 3. Router definition

Hyron supports 2 types of services

* [**HyronService**](api-reference/hyronservice.md): used for normal HTTP connection, or supported by addons from 3rd parties
* [**UnofficialService**](api-reference/unofficialservice.md): used for other special situations, such as sockets, high-level customization, or for another protocol

#### HyronService

Let Hyron know that this is a service that can be supported by the http protocol, you need to **return an interface** specifically that the [`requestConfig`](api-reference/hyronservice.md#function-requestconfig) contains descriptive information about that router. Example

{% code-tabs %}
{% code-tabs-item title="./model/UserManager.js" %}
```javascript
const userModel = require('../model/UserModel'); // mongoose model

module.export = class UserManager {
    static requestConfig(){
        return {
            createUser : {
                method : "post"
            }
        }
    }
    ...
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Tips : If simple, you only need to declare the method directly instead of a description with an object. Example : `createUser : "post"`
{% endhint %}

The default [**param\_parser plugins**](ecosystem/plugins/param_parser.md) will help automate the process of passing variables from your request to your controller, saving you time and allowing you to package services more easily to be reused by other services.

Here are some of the attributes you should keep in mind of [`requestConfig`](api-reference/hyronservice.md#function-requestconfig)\`\`

| Attribute | Type | Description |
| :--- | :--- | :--- |
| method | string \| Array&lt;string&gt; | contains methods that can be used to register routers, including `get`, `head`, `delete`, `post`, `put`, `patch`, `all`, `private` . Default is `get` |
| frontware | Array&lt;string\|Function&gt; | Specifies which frontware plugins will be run or not for this method |
| backware | Array&lt;string\|Function&gt; | Specifies which backware plugins will be run or not for this method |
| plugins | Array&lt;string&gt; | Specifies which plugins will be run or not for this method. It should be used in most cases |
| path | string | Customizing the path for this router. default is `/prefix/module-name/method-name` |
| params | string | customize dynamic path, which can be used as input for method. Example : `/user/:name/age/:age` |
| handle | function | Specifying the function will be used to listen on this router. This method has a higher priority than mapping |

#### Unofficial Services

Hyron supports a path that allows support for unofficial supported services or by addons from 3rd parties

{% code-tabs %}
{% code-tabs-item title="./services/socket-demo/index.js" %}
```javascript
var socket = require('socket.io');

module.exports = function (app, cfg) {
    var io = socket(app);
    io.on('connection', function(socket){
        console.log('an user connected');
    });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 4. Declare & Routing

You should separate the interface from the hyron to a separate file, called router.js, containing the description of the router \(if complicated\).

In the simple case, just export the corresponding controller. Example

{% code-tabs %}
{% code-tabs-item title="./router.js" %}
```javascript
module.export = require('./controller/UserManager');
```
{% endcode-tabs-item %}

{% code-tabs-item title="index.js" %}
```javascript
// Create an interface that makes it easy for other services to interact
const UserManager = require('./controller/UserManager');
module.export = new UserManager();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

To use, you need to declare them in the JSON build file

```scheme
{
    "base_url" : "http://localhost:3000",
    "services" : {
        "user": "./services/user/router.js"
    }
}
```

By default, the hyron will automatically register the url based on the declared information

![](.gitbook/assets/url-struct.png)

* To **customize a path**, use the [path](api-reference/routermeta.md#var-path) attribute to [declare a router](create-services.md#3-router-definition)
* You can also design **rest-style** routers with a combination of [params](api-reference/routermeta.md#var-params)
* You can **change the style** of the url with [style config](api-reference/modulemanager.md#function-setting)
* The above action is **not recommended** because it can affect the ability to share and reuse

