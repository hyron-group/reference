# Extension lib/path

Used to reference to a url

```
require('hyron/lib/path')
```

## Features

-   Find a router url by a part of it
-   Find a router url by main-handler
-   Allow to add other source
-   Get main-handler by a url

# Guide

## 1. Find a router url by path or function

Used to get complete url that was management by Hyron by a part of it (or full path if necessary). Example

```js
const {findURL} = require('hyron/lib/path');

...
// router with this path need to register first
var completePath = findURL('/api/say-hello');
console.log(completePath); // -> http://localhost:3000/demo/api/say-hello

// it also support for search by handler function
// you should use it for the most case for better support by your IDE
// don't worry about performance. it will cached for next call
var completePath = findURL(require('../api').sayHello);

```

## 2. Allow to add other source

By default, Hyron auto register url on runtime. You also register by you self used build function

Example

```js
var {build} = require('hyron/lib/path');


function doSomethingAction(val){
    // do something useful
    console.log(val);
}

// register path for abort url
build (
    "https://hyron.gitbook.io",
    "/reference",
    doSomethingAction);
```

## 3. Get main-handler by a url

You also could retrieve handler corresponding with a url used getHandleOfURL function

Example

```js
var {getHandleOfURL} = require('hyron/lib/path');

var doSomethingAction = getHandleOfURL("/reference");

doSomethingAction('hello world');

```

# API Reference

### interface path

-   **build** ( baseURL, eventName, executer ) : void
-   **findURL** ( query ) : string
-   **getHandleOfURL** ( path, baseUrl ) : function

# function build

> ## **build** ( baseURL, url, executer ) : void

Used to register a url scope, that can be use for another action

### **params**

-   **baseURL** ( string ) : base-url of your target website
-   **eventName** ( string ) : path of target site
-   **executer** ( function ) : a function to handle when retrieve this

# function findURL ( condition ) : string

> ## **findURL** ( condition ) : string

Used to retrieve a complete url by a part of url path or handle function

### **params**

-   **condition** ( string | function ) : condition for search. response will be cache for faster in the next call. You should to used function to search for better IDE support

### **return**

-   string : string url if exist or null if not

# function getHandleOfURL

> ## **getHandleOfURL** ( path, baseURL ) : function

Used to get handler of a url by url path

### **params**

-   **path** ( string ) : url or target site
-   **baseURL** ( string | null ) : base url of target website. If it null, it will refereence to first baseURL in scope

### **return**

-   function : a handler function correspond with base url have set before
