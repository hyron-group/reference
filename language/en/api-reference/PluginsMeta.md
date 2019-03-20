## **Table of contents**

### interface **PluginsMeta**

- [**fontware**](#var-fontware) : [Middleware](./Middleware.md)
- [**backware**](#var-backware) : [Middleware](./Middleware.md)


# interface **PluginsMeta**

Contain parts of a plugins. It helps separate the layer and handle input and output separately from the logical processing layer, making it easy to reuse them for many different situations.

# var fontware

> ## **fontware** : [Middleware](./Middleware.md)

This part will be called before main-handler for each time request has make. That could be used to handle input data such as prepare params for main-handler, handing connect, rate limited, decode, authenticate or something else

# var backware

> ## **backware** : [Middleware](./Middleware.md)

This part will be called after main-handler for each time request has make. That could be used to handle output data such as analysis, encode, authenticate or something else

