# What is Addons ?

> ### Addons is a module that extends features to the hyron

Addons are still a feature that is experiment, if you have any ideas, please [let us know](../contribution.md), we will be happy to help you.

# Why we use Addons ?

1. It helps platform can be **customized** depending on context : Nothing is perfect, hyron will also have many shortcomings and limitations because it is still young. So hyron vibrates a level that allows you to build features to extend core features, helping better serve you and the community.

2. can be **easily installed** : Addons can also be plugged into your application just like other components like plugins and services. We can take advantage of help from the community with it

# How can I write addons ?

In order to write addons, you need to understand how it works, and how the hydrogen works

In addition, it also depends on what you want to build

You can refer to Hyron's [Source Code](https://github.com/hyron-group/hyron) and [Documentation](../api-reference/AddonsMeta.md) for more information

Here are the points you should keep in mind

- Addons can be installed via [json-build-file/../addons](../buildIn-features/appLoader.core.md#use-json-build-file)
- An addons has two states that are [Normal State](../buildIn-features/appLoader.core.md#use-json-build-file) and [Global State](../buildIn-features/appLoader.core.md#to-register-global-addons)
- **Normal State** only **runs in that instance scope**
- **Global State** can **run on all instances**
- The state of addons can be controlled by the user
- addons can inherit the resources that hyron manages through this scope, you can use it to modify the source code of the
- The classes you need to keep in mind when writing Addons
  - [ModuleManager](https://github.com/hyron-group/hyron/blob/master/core/ModulesManager.js) : used to manage modules (instance, services, addons, plugins) and run the server
  - [AddonsManager](https://github.com/hyron-group/hyron/blob/master/core/addonsManager.js) : used to manage and store addons
  - [RouterFactory](https://github.com/hyron-group/hyron/blob/master/core/ServicesManager/RouterFactory.js) : is the service core, used to manage routers
  - [MiddlewareManager](https://github.com/hyron-group/hyron/blob/master/core/pluginsManager/middlewareManager.js) : used to manage and store plugins