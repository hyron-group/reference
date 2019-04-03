---
description: 'warning : CLI is comming soon !'
---

# Hello world

### Step 1 : Install Hyron CLI

{% code-tabs %}
{% code-tabs-item title="YARN" %}
```bash
yarn global add hyron-cli
```
{% endcode-tabs-item %}

{% code-tabs-item title="NPM" %}
```bash
npm i -g hyron-cli
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Step 2 : Add build file

{% code-tabs %}
{% code-tabs-item title="./app.json" %}
```scheme
{
    "base_url" : "http://localhost:3000",
    "services" : {
        "demo" : "./demo.js"
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Step 3 : Add controller file

{% code-tabs %}
{% code-tabs-item title="./demo.js" %}
```javascript
module.exports = class {
    static requestConfig(){
        return {
            sayHello : "get"
        }
    }
    
    sayHello(name){
        return "hello world !"+name;
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Step 4 : Run application

{% code-tabs %}
{% code-tabs-item title="Using hyron-cli" %}
```bash
hyron start app.json
```
{% endcode-tabs-item %}

{% code-tabs-item title="Using hyron" %}
```javascript
const hyron = require('hyron');

hyron.build("./app.json");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Result" %}
```http
GET http://localhost:3000/demo/say-hello?name=thangphung
```
{% endcode-tabs-item %}
{% endcode-tabs %}

