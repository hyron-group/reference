# Build-plugins

This topic will taling about how to build a plugins

## Table of contents

1. [Plugins structure](build-plugins.md##1.-Plugins-structure)
2. [Functions and features](build-plugins.md##2.-Functions-and-features)
3. [Recommendations](build-plugins.md##3.-Recommendations)

# Concept

Can be said, the hyron is a framework based on plugins. The main power of Hyron is actually largely based on external modules, such as plugins

First of all, let's learn a little bit about the concept, and why using plugins is essential.

## **Question** : What is plugins ?

### **Answer** :

> ### Plugins are a module that can be used to handle input and output for a router

## **Question** : Structure of a plugins ?

### **Answer** :

> ### A plugins based on 2 parts, fontware and backware

## **Question** : What is a fontware ?

### **Answer** :

> ### fontware is a middleware running in front of main-hander (is a function that processing business logic), used to process input for main-handler

## **Question** : What is a backware ?

### **Answer** :

> ### backware is a middleware running in back of main-hander, used to process output of main-handler

## **Question** : So, what a plugins look like ?

### **Answer** :

This is a diagram about a plugins

![](/res/plugins-struct.png)

Like you see, a plugins include at lest one part : fontware or backware or a both

Each middleware contains functions defined for itself as :
- **handle** ( req, res, prev ) : contain a function that can be called each time a request to target router have make
- **onCreate** () : a function that could be called for the first time to init values
- **checkout** ( done ) : a function that could be to used to revoke onCreate if have any change
- **typeFilter** : decide whether this middleware is executed by checking the type of prev
- **global** : decide whether the middleware is automatically called for each router or not

You can see [PluginsMeta reference](/api-reference/PluginsMeta.md) to find more about a plugins

## **Question** : Why we use plugins ?

### **Answer** :

- It's easy to reuse and share
- It helps separate the IO processing block from logic processing, makes it easy to reuse the logic block, test and fix errors, and your code becomes more concise.
- Can take advantage of help from the community through their push-up plugins

![](/res/router-struct.png)


## **Question** : How can i custom a plugins ?

### **Answer** :

In addition to modifying the code in the same way as the traditional way, hyron provides a solution that allows you to customize a plugins from 3rd parties through appcfg.yaml

appcfg is a special file that contains variables and settings for your modules and projects.
With override mechanism, lock field of appcfg.yaml. You can change the value of configuration properties to custom that plugins

But you should also note, you need to build a plugins so that they can be customized by other users. and the settings or processing should be cached and optimized to achieve the highest performance

You can use the following methods to access the config :
- args cfg at last argument of onCreate, checkout, handle
- Use hyron.**getConfig** ( pluginsName, defaultValue )

## **Questions** : How can i deploy my plugins ?

### **Answer** :

At the present time, we have not provided features to support deploying and sharing. We will try to release this feature as soon as possible to serve the community


## **Questions** : Do Hyron supports asynchronous plugins ?

### **Answer** :

Yes, so are all other ingredients


## **Questions** : I have many plugins, so how will the plugins run? ?

### **Answer** :

You can refer to the life of a router :

![](res/../../res/router-life-circle.png)

As you can see, the plugins will run sequentially, the value of the previous plugins will be used as the input value for the following plugins (via variables prev)

As you can see, the plugins will run sequentially, the value of the previous plugins will be used as the input value for the following plugins (via variables prev)

## **Questions** : Can I run my plugins without being declared ?

### **Answer** :

Yes, you can. By becoming a member of the Hyron organization, your package under @hyron scope if declared in appcfg will be able to be run automatically without requiring the user to declare it.

This is a great privilege. It allows your package to be much more convenient, and can be used as a third library

## **Questions** : Why is the package of the hyron organization preferred ?

### **Answer** :

Its package will be better moderated, so it is more reliable than other regular packages. In addition, you can also get help, and other benefits from the hyron developer community. See more at [developer policies]()


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

## Step 2 : create plugins structure

in plugins-name.fw.js & plugins-name.fw.js
```js

```


# Note

* You should name plugins handle with format : name.fw.js if it is fontware, or name\_bw.js if it is backware
* Plugins should be identical to the declared name
* The name of the plugins should be unique
* Development plugins should also adhere to the principles of application design and development, to facilitate maintenance and expansion for later.


Next step : [View example](example.md)

