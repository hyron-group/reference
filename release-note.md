# Release note

### 2.4.0 - 2018-1-22

* **Switch from appcfg.ini to appcfg.yaml**
  * light syntax
  * allow deep value config and multi type provided by yaml. Includes : number, string, boolean, array, object
  * easy to learn & implement

* **More powerful for config file(appcfg)**
  * lock key with '$' character at start of key. that ignore inherited on this field  
  * internal referenced with syntax : <#key.field>
  * external referenced with syntax : <~path>
  * allow implement inside modules include : addons, plugins, services, organization, self your app


* **Build app with json file**
  * auto download necessary modules (used yarn)
  * light & clear syntax
  * easy to management
  
*  **More powerful for addons**
   *  more access onto core base

* **Support for REST API**
  * separate request path into separate requestConfig properties : params with syntax : /:param1/:param2
  * removed app setting -> enableRestFul, requestConfig -> enableREST. Replace by requestConfig -> params
  * High performance index

* **Support for multi instance on port**
* **Support random port if port = 0**
* **Support for another tcp protocols include : https, http2**
* **Optimize & refactor codebase**
* **Add override for some methods**
* **Better document**
* **Fix bug**


## 2.0.0 - 2018-12-12

* Replace enableFontware\(\) and enableBackware\(\) with enablePlugins\(\)
* Increased independence for plugins
* Optimize & Restructure the source code
* Increase performance by 10% \(~ 83-90% compared with raw-node\)
* Remove the default plugins to use less
* Styling URL \(camel, snake, lisp, lower\)
* Addons that help to custom Hyron framework
* Support for async function
* Introduced animals into the world, we believe they're going to be a neat addition.
* Fix bug
