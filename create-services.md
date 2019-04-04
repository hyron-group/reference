---
description: >-
  Service is the smallest processing unit, used to handle a specific business
  logic
---

# Create Services

{% hint style="info" %}
Hyron encourages you to build [Microservice Architecture](https://microservices.io/) applications that bring great benefits to your application
{% endhint %}

![Hyron can turn a controller into a router automatically with just a few lines](.gitbook/assets/overview-controller.png)

## Why ?

* Easy to expand
* Easy to understand
* Easy to reuse

## Usage

### Initialization service

{% code-tabs %}
{% code-tabs-item title="Using hyron-cli" %}
```bash
hyron init services
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Structure" %}
```text
service-name
  ├── controller/     - contain processing logic for this service
  ├── model/          - contain contains data models, methods for communicating with the database
  ├── index.js        - contains interfaces for use by other services
  ├── router.js       - contains interfaces for use by Hyron to register to the service
  ├── appcfg.yaml     - contains the configuration used for this service
  ├── package.json    - contains the basic information of this service used for the npm registry
  └── readme.md       - contains descriptions for this service
```
{% endcode-tabs-item %}
{% endcode-tabs %}



