## **Table of contents**

### interface **PluginsMeta**

- fontware : Middleware
- backware : Middleware


### interface **Middleware**

-   **handle** ( req, res, prev, cfg ) : any | Promise< any >
-   **onCreate** ( cfg ) : any | Promise< any >
-   **checkout** ( done, cfg ) : boolean | Promise< boolean >
-   **typeFilter** : Array< any >
-   **global** : boolean


# **Details**

## *interface **PluginsMeta***

Contain parts of a plugins. It helps separate the layer and handle input and output separately from the logical processing layer, making it easy to reuse them for many different situations.

# var fontware

> ## **fontware** : Middleware
This part will be called before main-handler for each time request has make. That could be used to handle input data such as prepare params for main-handler, handing connect, rate limited, decode, authenticate or something else

# var backware

> ## **backware** : Middleware
This part will be called after main-handler for each time request has make. That could be used to handle output data such as analysis, encode, authenticate or something else

---

## *interface **Middleware***
It used to declare middleware that used to run before or after each services

# function handle

> ## **handle**( req, res, prev, cfg ) : any | Promise< any >

This is a heart of a plugins. It will be called when a request has make. Used to handle input or output data or something else

This function has the ability to access the 'this' variable of this route

### **params**
- **req** ( IncomingMessange ) : contain request data from client
- **res** ( ServerResponse ) : contain response from server
- **prev** ( any ) : preview result from abort plugins or main-handler if it is a first backware
- **cfg** ( any ) : config of this plugins

### **return**
any | Promise < any > : A result that could be used by bellow plugins, or as main-handler function if it is last fontware. It also support for async function or function return with a Promise

---

# function onCreate

> ## **onCreate** ( cfg ) : void | Promise< void >

This function called for the fist time request of this instance has make. Used to prepare value for later activities

This function has the ability to access the 'this' variable of this route

### **params**
- **cfg** ( any ) : config of this plugins


### **return**

void | Promise< void > : it not required, just notify in async case that it completed

---

# function checkout

> ## **checkout** ( done, cfg ) : boolean | Promise< boolean >

Used to check if some value has changed. If a change has make, onCreate will be revoke again

This function has the ability to access the 'this' variable of this route

### **params**

- **done** ( function ) : a function that break checkout life circle loops
- **cfg** ( any ) : config of this plugins


### **return**
boolean | Promise< boolean > : true if has change, or not

---

# var typeFilter
> ## **typeFilter** : Array< any >

It is used to filter which type of data from prev will be processed. if type of 'prev' don't contain in array. It will be skip

---

# var global
> ## **global** : boolean

Used to turn on global mode. Meanwhile, this middleware will be called automatically on each router. 

In addition, it can also be turned off in requestConfig -> fontware / backware / plugins by adding a '!' character before this plugins name