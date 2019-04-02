---
description: >-
  appcfg.yaml is a file containing the settings of the modules in the
  application
---

# Config File

![Setting is the sum of the config in the application](.gitbook/assets/appconfig.png)

## Why ?

* Easy to customize modules
* Flexible and versatile
* Easy to learn and easy to use
* Allow inheritance
* Support deep reference
* Support internal reference
* Support external reference
* Support value lock

## Classify

The config can be divided into two categories by level: `Module Level` and `Application Level`

### Module Level

#### 1. Services config

```text
service-name
  ├── controller/
  ├── model/
  ├── index.js
  ├── router.js
  └── appcfg.yaml
```

{% code-tabs %}
{% code-tabs-item title="appcfg.yaml" %}
```yaml
page_size: 20
filter:
  - age
  - location
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Service config can be accessed by the `this.$config` variable

{% code-tabs %}
{% code-tabs-item title="Normal services" %}
```javascript
getUsers(){
    var {page_size, filter} = this.$config;
    ...
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Unofficial service" %}
```javascript
function(app, cfg){
    var {page_size, filter} = this.$config;
    ...
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 2. Plugins config

```text
plugin-name
  ├── src/
  ├── lib/
  ├── index.js
  ├── hyron-plugin.js
  └── appcfg.yaml
```

{% code-tabs %}
{% code-tabs-item title="./plugins/demo/appcfg.yaml" %}
```yaml
private_key: 123456
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="./plugins/demo/hyron-plugin.js" %}
```javascript
function handler(req, res, prev, cfg){
    var {private_key} = cfg;
    ...
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 3. Addons config

```text
addon-name
  ├── src/
  ├── lib/
  ├── index.js
  ├── hyron-addon.js
  └── appcfg.yaml
```

{% code-tabs %}
{% code-tabs-item title="./addons/demo/appcfg.yaml" %}
```yaml
email: thangphung.work@gmail.com
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
function handler(cfg){
    var {private_key} = cfg;
    ...
}
```

### Application Level

```text
root
  ├── services/
  ├── addons/
  ├── plugins/
  ├── res/
  ├── server/
  ├── public/
  ├── index.js
  ├── package.json
  └── appcfg.yaml
```

{% code-tabs %}
{% code-tabs-item title="./appcfg.yaml" %}
```yaml
public_key: ahihi123
app_name: myApp
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Features

### 1. Lock field

To prevent inheriting a field, add '$' before the name of the field. For example

{% code-tabs %}
{% code-tabs-item title="./plugins/demo/appcfg.yaml" %}
```yaml
$private_key: 123456
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 2. Deep reference

To access a deep field in a parent field. For example

{% code-tabs %}
{% code-tabs-item title="./addons/crud/appcfg.yaml" %}
```yaml
schema:
  accounts:
    email: string
    password: string
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="./addons/crud/hyron-addons.js" %}
```javascript
const {getConfig} = require("hyron");

module.exports = function(cfg){
    var accountModel = getConfig("schema.accounts", {});
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 3. Internal reference

The value of a field in appcfg can be  **referenced**  to another field. For example

{% code-tabs %}
{% code-tabs-item title="appcfg.yaml" %}
```yaml
key1:
  child1: hello

key2: <#key1.child1> # hello
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 4. External reference

The value of a field in appcfg can be  **referenced externally**  by another `yaml` file

{% code-tabs %}
{% code-tabs-item title="./models/account.yaml" %}
```yaml
email: string
password: string
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="./addons/crud/appcfg.yaml" %}
```yaml
schema:
  account: <~models/account.yaml>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 5. Allow inheritance

`appcfg.yaml` in  **Application Level**  can override the config from the config in  **Module Level**  by identifying the module \(declared in the build file\)

{% code-tabs %}
{% code-tabs-item title="./appcfg.yaml" %}
```yaml
service_name:
  page_size: 50
  
addons_name:
  email: hyron.dev@gmail.com

plugins_name:
  private_key: abc123
```
{% endcode-tabs-item %}
{% endcode-tabs %}

