---
description: 'Use to extend features for hyron, or run other scheduled, initialized tasks'
---

# Create Addons

{% hint style="warning" %}
This feature is in the process of developing and improving, to increase the flexibility of the hyron
{% endhint %}

## Why ?

* More **flexible** with high **customization capabilities**
* help **minimize the core**, improve speed and ease of **expansion**
* Serves easily **scheduled** and **initialized** **tasks**

## **Usage**

### **1.** Initialization addons

{% code-tabs %}
{% code-tabs-item title="Using hyron-cli" %}
```bash
hyron init addons
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
addon-name
  ├── lib/              - contains reusable code sections
  ├── src/              - contains the main processing code
  ├── index.js          - contains interfaces for use like a library
  ├── hyron-addon.js   - contains interfaces for use by Hyron to register to the addons
  ├── appcfg.yaml       - contains the configuration used for this addons
  ├── package.json      - contains the basic information of this addons used for the npm registry
  └── readme.md         - contains descriptions for this addons
```

### 2. Create addons handler

An addons is simply a function that is run when starting an instance

{% code-tabs %}
{% code-tabs-item title="./addons/database-setup/index.js" %}
```javascript
const mongo = require("mongoose");

module.exports = function(app, cfg){
    mongo.connect(cfg.mongo_url);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**addons share this variable with an instance**, so you can customize the functions in it or add new features if needed

For more information on addons, and using them, refer to the [source code](https://github.com/hyron-group/hyron/blob/master/core/ModulesManager.js) of hyron

### 3. Declare Addons

Like other modules, you also need to declare addons to use

{% code-tabs %}
{% code-tabs-item title="./server/app.json" %}
```scheme
{
    "base_url": "http://localhost:3000",
    "addons" : {
        "db-setup" : "./addons/database-setup"
    },
    "services": {...}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

A global addons can be run on all instances

```scheme
[
{
    "addons" : {
        "db-setup" : "./addons/database-setup"
    }
},
{
    "base_url": "http://localhost:3000",
    "services": {...}
},
{
    "base_url": "http://localhost:3001",
    "services": {...}
}
]
```

