# PluginsMeta

#### interface **PluginsMeta**

* [**fontware**](pluginsmeta.md#var-fontware) : [Middleware](middleware.md)
* [**backware**](pluginsmeta.md#var-backware) : [Middleware](middleware.md)

## interface **PluginsMeta**

Contain parts of a plugins. It helps separate the layer and handle input and output separately from the logical processing layer, making it easy to reuse them for many different situations.

## var fontware

> ### **fontware** : [Middleware](middleware.md)

This part will be called before main-handler for each time request has make. That could be used to handle input data such as prepare params for main-handler, handing connect, rate limited, decode, authenticate or something else

## var backware

> ### **backware** : [Middleware](middleware.md)

This part will be called after main-handler for each time request has make. That could be used to handle output data such as analysis, encode, authenticate or something else

