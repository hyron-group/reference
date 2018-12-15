# app-example

This is simple hello-world app that help you have overview about hyron framework

```javascript
const hyron = require('hyron');

// init instance that listen on localhost, port 3000 by default
var instance = hyron.getInstance();

class DemoRouter {
    // return a object that description about routers
    static requestConfig(){
        return {
            // register event get on method sayHi
            sayHi: "get"
        }
    }

    // main handler that handle business logic
    sayHi(){
        return "hello world";
    }
}

instance.enableService({
    "":DemoRouter
})

instance.startServer();
```

## Result

A router registered on :

> ## GET : [http://localhost:3000/sayHi](http://localhost:3000/sayHi)

So, that really easy, right. You can do more with hyron framework :D check it out in next step

Next step : [getting started](geting-started.md)

See more :

* [Develop Plugins](https://github.com/hyron-group/reference/tree/3437eeb47ffad09baf95272f73ae3e71764436ce/plugins-developent/overview.md)
* [Develop Service](https://github.com/hyron-group/reference/tree/3437eeb47ffad09baf95272f73ae3e71764436ce/service-developent/overview.md)
* [Develop Addons](addons-development/overview.md)

