\[ experiment \]

# Summary

1. Write processing logic for [addons](../api-reference/AddonsMeta.md)
2. Declare addons to use in [json-build-file/~/addons](../buildIn-feature/appLoader.core.md) or [ModuleManager.enableAddons](../api-reference/ModuleManager.md#function-enableaddons-2-override) or [ModuleManager.enableGlobalAddons](../api-reference/ModuleManager.md#function-enableglobaladdons-2-override)

# Build in step-by-step

## 1. Write Processing Logic

Addons is a very simple and powerful feature. It allows you to customize and extend Hyron framework. By allowing access to resources that are managed from the ModuleManager class ( base of Hyron ) via this scope

### Declaration syntax

The simple addons are a function that is loaded into this variable from an initialized instance

```javascript
function handle(cfg){
    // show baseURI
    console.log(this.base_url);
}

module.exports = handle;
```

through this variable, you can optionally load what you want by using the following ways :

```javascript
// way 1 : used object.assign for multi value
Object.assign(this, args); // merge this var with args

// way 2 : used load var for single value
this.var_name = val;
```

You can also use the above method to override the default method. However, that is not recommended. If it's a bundle of Hyrons, we'd love to be able to contribute an edit from you.

To develop addons effectively, in addition to the documentation we have developed, you can study Hyron code to get a better view of the framework.

There is classes you need to keep in mind when writing Addons
  - [ModuleManager](https://github.com/hyron-group/hyron/blob/master/core/ModulesManager.js) : used to manage modules (instance, services, addons, plugins) and run the server
  - [AddonsManager](https://github.com/hyron-group/hyron/blob/master/core/addonsManager.js) : used to manage and store addons
  - [RouterFactory](https://github.com/hyron-group/hyron/blob/master/core/ServicesManager/RouterFactory.js) : is the service core, used to manage routers
  - [MiddlewareManager](https://github.com/hyron-group/hyron/blob/master/core/pluginsManager/middlewareManager.js) : used to manage and store plugins

## 2. Declare addons to use

You can control state of addons, make it as global and run on every instances, or by normal and run in assign instance

to make it become a global addons we can declare it in json build file as bellow :

server.json
```json
[
    // declare global addons
    {
        "addons":{
            "logger" : "./addons/logger",
            "debugger" : "./addons/debugger",
            "relation-analysis" : "./addons/rel-analysis",
            "document-general" : "document-general"
            ...
        }
    },
    // link to instances
    "./app/my-app1.json",
    "./app/my-app2.json"
]
```

or if you run addons only within the specified instance, you can declare in the ``addons`` attribute

my-app1.json
```json
{
    "base_url": "https://localhost:3000/app1",
    "addons" : {
        "server-setup" : "./addons/setup-server.js",
        "database-setup" : "./addons/database-setup.js",
        ""
        ...
    },
    "services" : {
        ...
    }
}
```
