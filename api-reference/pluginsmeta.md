# PluginsMeta

#### interface **PluginsMeta**

* [interface **PluginsMeta**](pluginsmeta.md#interface-pluginsmeta-1)
* [var fontware](pluginsmeta.md#var-fontware)
* [var backware](pluginsmeta.md#var-backware)

## interface **PluginsMeta**

Contain parts of a plugins. It helps separate the layer and handle input and output separately from the logical processing layer, making it easy to reuse them for many different situations.

## var fontware

> ### **fontware** : [Middleware](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/Middleware.md)

This part will be called before main-handler for each time request has make. That could be used to handle input data such as prepare params for main-handler, handing connect, rate limited, decode, authenticate or something else

## var backware

> ### **backware** : [Middleware](https://github.com/hyron-group/reference/tree/40d0182386de8089e26b1cc05c3e887c4b505d69/api-reference/Middleware.md)

This part will be called after main-handler for each time request has make. That could be used to handle output data such as analysis, encode, authenticate or something else

