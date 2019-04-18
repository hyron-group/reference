---
description: >-
  Used to package a plugins that can be used by hyron such as the IO layer used
  to process input and output for requests
---

# PluginsMeta

#### interface **PluginsMeta**

* [var frontware](pluginsmeta.md#var-frontware)
* [var backware](pluginsmeta.md#var-backware)



## Details

### interface **PluginsMeta**

Contain parts of a plugins. It helps separate the layer and handle input and output separately from the logical processing layer, making it easy to reuse them for many different situations.



### var frontware

```javascript
frontware : Middleware
```

This part will be **called before executer** for each time request has make. That could be used to handle input data such as prepare params for executer, handing connect, rate limited, decode, authenticate or something else



### var backware

```javascript
backware : Middleware
```

This part will **be called after executer** for each time request has make. That could be used to handle output data such as analysis, encode, authenticate or something else

