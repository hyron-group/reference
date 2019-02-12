# app-example

This is simple hello-world app that help you have overview about Hyron framework

```javascript
const hyron = require("hyron");

// init instance that listen on localhost, port 3000 by default
var instance = hyron.getInstance();

class DemoRouter {
    // return a object that description about routers
    static requestConfig() {
        return {
            // register event get on method sayHi
            sayHi: "get"
        };
    }

    // main handler that handle business logic
    sayHi() {
        return "hello world";
    }
}

instance.enableServices({
    "demo": DemoRouter
});

instance.startServer();
```

## Result

A router registered on :

> ## GET : [http://localhost:3000/demo/sayHi](http://localhost:3000/sayHi)

So, that really easy, right. You can do more with Hyron framework :D check it out in next step

Next step : [getting started](geting-started.md)

See more :

-   [Develop Plugins](plugins-development/README.md)
-   [Develop Service](service-development/README.md)
-   [Develop Addons](addons-development/README.md)
