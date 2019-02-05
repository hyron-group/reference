# Build-service

# Concept

## What is service ?

> ### Service is a group of functions used to handle a specific business logic

## What is Micro-Service ?

> ### microservice is an application programming architecture that focuses on separating application features into the smallest processing services

## Why should I build on the micro-service architecture ?
Design your app used micro-service architecture gives you a lot of advantages compared to developing applications in monolithic architecture

We can mention the main advantages
- Easy to develop and expand
- Easy to reuse and control
- Easy testing and deployment



## Main handle flow

![](/res/router-life-circle.png)

## Declare config

To enable router. you need to declare it into **requestConfig()** method :

```javascript
static requestConfig(){
    return {
        method_name : meta
    }
}
```

The requestConfig method created to makes it easy for you to control the routers. It is a description of how hyron knows what it needs to do with the routers as specifying the main processing methods, plugins and their order of run, paths and more.

```javascript
static requestConfig(){
    return {
        method_name : method_type
    }
}
```

After declaring and turning it on enableServices() method. The router will be registered with the specified path. As mentioned above, if you do not specify a path, Hyron default will be based on the key name in the description to register the router path.

Example : /prefix/service\_name/method\_name

### **Config multi route**

If you have many of route with same config. You can used $all properties to setting global properties that router of this service used. Example

```javascript
static requestConfig(){
    return {
        $all : {
            fontware : ["stringer"]
        },
        sayHi : "get",
        sayBye : "get"
    }
}
```

The preference of the $all properties is less than meta. Therefore, you can also override the declared properties in $all normally

```javascript
static requestConfig(){
    return {
        $all : {
            fontware : ["stringer"]
        },
        ...
        sayNothing : {
            method : "post",
            fontware : ["!stringer"]
        }
    }
}
```

### **Style uri path**

The good news is that you can customize the type of path that suits your interests by adding a bit to the settings in app instance

```javascript
const hyron = require('hyron')

var yourApp = hyron.createInstance();

yourApp.setting({
    style : "lisp" // it will change path become : .../show-my-name
})

...
```

hyron support for 4 type of style, include :

* **camel** : like showMyName ( as default )
* **snake** : like show\_my\_name
* **lisp** : like show-my-name
* **lower** : like showmyname

## Declare method

Method contain business logic of your app, and just it

The hyron allows you to focus more on building processing logic with powerful of fontware param-parser. Now, you can turn a normal function into a router.

Hyron is friendly will [ECMAScript6](http://es6-features.org/). You should used them in your project because it has a fairly short syntax and is easy to use

```javascript
showMyName(firstName, lastName){
    return "Hello " + firstName + lastName;
}
```

Good new :D, you do not to care about how to dissection data from request (as query or body), you also do not need to care about the type of input data. It support dynamic for url-encoded, multi-part, file-upload, raw data.

Below are the rules you need to remember of param-parser plugins

* If method is **GET**, **HEAD** (query type) : param-parser will extract data from query
* If method is **POST**, **PUT**, **PATCH** (body type) : param-parser will extract data from body. It support for both of multipart and urlencoded, include upload file
* If you pass a file into body. It will wrapped by a "**ClientFile**" object, with properties is :
  * **name** : name of file
  * **content** : file data, in buffer
  * **encoding** : encoder algorithm of this file
  * **type** : file mime type
* If you pass **raw data** into body (with content-type is different with multipart and urlencoded), you need to add argument with name $body to receive data.
* If **params** option is set, then param-parser plugins will parse url and pass it as variable string is defined according to the syntax : /:arg1_name/:arg2_name
* param-parser also support for array or object input type for urlencoded and multipart. So, you can pass it in string format. Example : /search?sort=\[date,price\]&filter={local:vietnam}

### **Separate class into multi-file**

If your class too long (upto 200 line or more) You can separate your class into many of file. Example

```text
basic-auth
    |---- controller
              |---- login.js
              |---- signup.js
              |---- AccountManager.js
```

in this case, we separate handle function into 2 file js login and signup. and in AccountManager, we used properties handle to declare main-handler function

```javascript
static requestConfig(){
    return {
        login : {
            method : "post",
            handle : require('./login')
        }
        ...
    }
}
```

In addition, there is another way. That is you merge 2 class used 'hyron/type/route'

```javascript
// file login.js
class Login {
    static requestConfig(){
        return {
            login : "post"
        }
    }
    ...
}

//file signup.js
// class Signup as the same

//file AccountManager
const route = require('hyron/type/route');
module.exports = route.merge(
    require('./login'),
    require('./signup)
)
```

### **Service structure**

You can configure according to any model you want, which is not required. You can apply the model below. I am currently applying it to my project. It is based on the MVI model

```text
basicAuth
    |---- controller                           : that contain handler function
    |          |---- AccountManager.js         : is hyron AbstractRouter
    |
    |---- model
    |       |---- account.js                   : contain model object, mapping, in this case is mongodb model
    |
    |---- plugins                              : not required, if your service used own plugins, that is should be one-time plugins
    |---- router.js                            : export hyron AbstractRouter, that can be used to enableServices()
    |---- index.js                             : export instance of AbstractRouter. It can be used by another service
```

### **Base router**

If you want to have a router like

```text
http://localhost/
http://localhost/getting-started
```

don't worry, you can do it with hyron, it very easy. Has two way to do that

* used path properties in requestConfig
* change method name and key name to "".

Next step : [build unofficial service](build-unofficial-service.md)

