# Build-plugins

This topic will taling about how to build a plugins

## Table of contents

1. [Plugins structure](build-plugins.md##1.-Plugins-structure)
2. [Functions and features](build-plugins.md##2.-Functions-and-features)
3. [Recommendations](build-plugins.md##3.-Recommendations)

# Concept

Can be said, the hyron is a framework based on plugins. The main power of Hyron is actually largely based on external modules, such as plugins

First of all, let's learn a little bit about the concept, and why using plugins is essential.

## What is plugins ?

> ### Plugins are a module that can be used to handle input and output for a router

## Structure of a plugins ?

> ### A plugins based on 2 parts, fontware and backware

## What is a fontware ?

> ### fontware is a middleware running in front of main-hander (is a function that processing business logic), used to process input for main-handler

## What is a backware ?

> ### backware is a middleware running in back of main-hander, used to process output of main-handler

## So, what a plugins look like ?

This is a diagram about a plugins

![](/res/plugins-struct.png)

Like you see, a plugins include at lest one part : fontware or backware or a both

Each middleware contains functions defined for itself as :

-   **handle** ( req, res, prev, cfg ) : contain a function that can be called each time a request to target router have make
-   **onCreate** ( cfg ) : a function that could be called for the first time to init values
-   **checkout** ( done, cfg ) : a function that could be to used to revoke onCreate if have any change
-   **typeFilter** : decide whether this middleware is executed by checking the type of prev
-   **global** : decide whether the middleware is automatically called for each router or not

You can see [PluginsMeta reference](/api-reference/PluginsMeta.md) to find more about a plugins

## Why we use plugins ?

-   It's easy to reuse and share
-   It helps separate the IO processing block from logic processing, makes it easy to reuse the logic block, test and fix errors, and your code becomes more concise.
-   Can take advantage of help from the community through their push-up plugins

![](/res/router-struct.png)

## How can i custom a plugins ?

In addition to modifying the code in the same way as the traditional way, hyron provides a solution that allows you to customize a plugins from 3rd parties through appcfg.yaml

appcfg is a special file that contains variables and settings for your modules and projects.
With override mechanism, lock field of appcfg.yaml. You can change the value of configuration properties to custom that plugins

But you should also note, you need to build a plugins so that they can be customized by other users. and the settings or processing should be cached and optimized to achieve the highest performance

You can use the following methods to access the config :

-   args cfg at last argument of onCreate, checkout, handle
-   Use hyron.**getConfig** ( pluginsName, defaultValue )

## How to deploy my plugins ?

At the present time, we have not provided features to support deploying and sharing. We will try to release this feature as soon as possible to serve the community

You also use another service to resolve this problem like

-   [npm registry](https://www.npmjs.com/)
-   [github](https://github.com/)
-   [bitsrc](https://bitsrc.io/)

## Do Hyron supports asynchronous plugins ?

Yes, so are all other ingredients

## I have many plugins, how will the plugins run ?

You can refer to the life of a router :

![](res/../../res/router-life-circle.png)

As you can see, the plugins will run sequentially, the value of the previous plugins will be used as the input value for the following plugins (via variables prev)

As you can see, the plugins will run sequentially, the value of the previous plugins will be used as the input value for the following plugins (via variables prev)

## Can I run my plugins without being declared ?

Yes, you can. By becoming a member of the Hyron organization, your package under @hyron scope if declared in appcfg will be able to be run automatically without requiring the user to declare it.

This is a great privilege. It allows your package to be much more convenient, and can be used as a third library

## Why is the package of the hyron organization preferred ?

Its package will be better moderated, so it is more reliable than other regular packages. In addition, you can also register to become developer with benefits like get help, rewards and other benefits from the hyron developer community. See more at [developer policies]()

# Guide

Bellow is way to create a plugins

## Step 1 : Create a new plugins directory

create a new forder as bellow (or difference if you want - skip this step)

```
plugins
    `-- plugins-name
            |-- src
            |-- lib
            |-- index.js
            |-- appcfg.yaml
            |-- plugins-name.fw.js
            `-- plugins-bane.bw.js
```

## Step 2 : Create plugins structure

in plugins-name.fw.js & plugins-name.fw.js ( it's also called middleware )

```js
module.export = {
    handle(req, res, prev, cfg) {
        // do something useful when router is trigger
        return prev;
    },

    onCreate(cfg) {
        // prepare value and environment
    },

    checkout(done, cfg) {
        // check if have any change to revoke onCreate
        return false;
    },

    // filter typeof 'prev' that handle by this middleware
    typeFilter: ["object", "string"],

    // true if this middleware will be call on every router
    global: false
};
```

You don't need to implement all of method abort, you only need to implement the required methods. To see detail about Middleware, please see [API Reference](api-reference/PluginsMeta.md)

After that, you need to write logic for middleware. What do you want to do with this

## Step 3 : Wrap middleware in index.js

index.js

```js
module.exports = {
    fontware: require("./plugin-name.fw.js"),
    backware: require("./plugin-name.bw.js")
};
```

if you as a member of hyron organization, you could make your plugins register automatic when user install it by this way :

**Step 1 : change your package name into : @hyron/plugins-name**
or, simple is init your package with hyron organization from begin

package.json
```json
{
  "name": "@hyron/plugin-name",
  ...
}
```

**Step 2 : declare middleware in appcfg.yaml**

everything you need to make sure is plugins-name is a unique name

And as user, you also avoid named you modules with name is the same with this

```yaml
fontware:
    plugins-name: '@hyron/package-name/plugins-name.fw.js'

backware:
    plugins-name: '@hyron/package-name/plugins-name.bw.js'
```

## Step 4 : publish you plugins

In the future, we plan to build a separate hub so that users can share their modules, with stronger support for hyron and users.

But now, you can used follow way to deploy your plugins

npm : check it out at [npm document](https://docs.npmjs.com/cli/publish)

```
npm publish --access public
```

github : check it out at [github document](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/)

bitsrc : check it out at [bitsrc document](https://docs.bitsrc.io/docs/quick-start.html)

# Note

-   You should name plugins handle with format : name.fw.js if it is fontware, or name_bw.js if it is backware
-   Plugins should be identical to the declared name
-   The name of the plugins should be unique
-   Development plugins should also adhere to the principles of application design and development, to facilitate maintenance and expansion for later.

Next step : [View example](example.md)
