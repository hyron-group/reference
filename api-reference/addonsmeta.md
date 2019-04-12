---
description: Used to pack an addons used to extend hyron or to run a task
---

# AddonsMeta

#### interface **AddonsMeta**

* [**handle**](addonsmeta.md#function-handle) \( cfg \) : void

## Details

### interface **AddonsMeta**

Contains sections that define an addons. Addons help you to expand the Hyron platform, even making it more efficient, your way.

Addons have access to the resources that Hyron manages, such as instances, services, plugins, other addons, config, server, environment variables, ect

You can edit them by object inject through '**this**' variable, and make it stronger, handle your logic, or you can use addons to run scheduled tasks or run something at instance startup

### 

### function handle

A function contains custom logic for Hyron

#### ★ **Params**

```javascript
function handle(cfg) : void
```

| name | type | description |
| :--- | :--- | :--- |
| cfg | object | a function contains custom logic for hyron |
| **this** | object | variable this with scope in this instance |



