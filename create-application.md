---
description: >-
  Hyron helps you build applications faster and easier, meeting the development
  and expansion capabilities well
---

# Create Application

## Usage

### 1. Initialization application

{% code-tabs %}
{% code-tabs-item title="Using @hyron/cli" %}
```bash
hyron init app
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Structure" %}
```text
app-name
  ├── addons/         - contains the addons of your application
  ├── docs/           - contains project-related documents
  ├── lib/            - contains reusable libraries
  ├── plugins/        - contains the plugins of your application
  ├── public/         - contains resources that are publicly accessible
  ├── server/         - contains descriptions of instances that can be used by Hyron to run the application
  ├── services/       - contains the services of your application
  ├── strings/        - contains the string values in the application that can be used by @hyron/stringer plugins
  ├── test/           - contains test suites for the application
  ├── .gitignore      - contains the setting of git to ignore when synchronizing source code
  ├── appcfg.yaml     - contains application-level application configs
  ├── package.json    - contains descriptions of the application that can be used by npm
  └── readme.md       - contains descriptive information about the project
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 2. Create Modules

Hyron app based on 3 module units

1. **Services :** are the smallest processing units for a business logic. For more information, please see [Create Services](create-services.md) topic
2. **Plugins** : are the middleware from I/O layer, used to handle incoming, outgoing or interactive flows, and use it flexibly for many situations. For more information, please see [Create Plugins ](create-services.md)topic
3. **Addons** : are pluggable functions for customizing, or adding features to the hyron, interacting with resources that Hyron manages, and other situations. For more information, please see [Create Addons](create-addons.md) topic

{% hint style="info" %}
Tips : Hyron developed many features that allow you to reuse it to the maximum. Design your modules the most flexible way to use them for your later projects
{% endhint %}

### 3. Create instance

An **instance is a case of the application**. Hyron allows you to separate applications into separate instances, making it **easy to manage**

Instances should be declared in a [json build file](json-build-file.md) using json syntax

**Instances can overlap each other**, the hyron will pool them at runtime. It is used to group instances according to the corresponding addons or as required by the project

{% code-tabs %}
{% code-tabs-item title="server/app.js" %}
```scheme
{
    "base_url": "http://localhost:3000",
    "addons": {
        "db-setup" : "addons/database-setup",
        "multi-language": "@hyron/multi-pl",
        "java-driver" : "addons/java-driver",
        "python-driver" : "addons/python-driver"
    },
    "plugins": {
        "auth" : "plugins/simple-auth",
        "stringer": "@hyron/stringer",
        "validator": "@hyron/validator"
    },
    "services": {
        "account": "services/account/router.js",
        "user": "services/user/router.js",
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 4. Run your app

You can use @hyron/cli to run the application

```text
hyron start
```

