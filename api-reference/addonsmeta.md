## **Table of contents**

### interface **AddonsMeta**

- [**handle**](#function-handle) ( cfg ) : void


# *interface **AddonsMeta***

Contains sections that define an addons. Addons help you to expand the Hyron's platform, even making it more efficient, your way.

Addons have access to the resources that Hyron manages, such as instances, services, plugins, other addons, config, server, environment variables, ect

You can edit them by object inject through '**this**' variable, and make it stronger, handle your logic. This requires you to have a background knowledge.
You can refer to the hyron's source code for more details, or join the hyron development community to get the instructions quickly.

You can refer to the following link for more information : [how to contribution](../contribution.md)

# function handle

> ## function **handle** ( cfg ) : void

A function contains custom logic for Hyron

### **params**

- **cfg** ( object ) : a function contains custom logic for hyron
- **this** : variable this with scope in this instance