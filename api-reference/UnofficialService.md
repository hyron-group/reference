## **Table of contents**


### interface **UnofficialService**
- **handle** ( app, cfg ) : void

# **Details**

## interface **UnofficialService**

Used to run modules that are not supported by hyron yet. With the UnofficialService, you have more freedom to run what you want. You should also note that it is not strictly managed by Hyron, so plugins and some of addons may not support this space.

However, there may be someone who has encountered the same situation as you, you can search for and install addons that match your needs. Or if you are the first one, we strongly encourage you to build a public addons to solve that problem

An addons have the ability to access and edit the resources that Hyron manages, you can use it to help expand the functionality for the hyron. You can refer to the following instructions for more information : [How to build a addons ?](addons-development/overview.md)

# function handle

> ## function **handle** ( app, cfg ) : void

Used to register handler for this router. It can be used to work with sockets, or write other advanced events

### **params**
- **app** ( Server | any ) : it as [http.Server](https://nodejs.org/api/http.html#http_class_http_server) by default. You also custom this with a addons
- **cfg** ( object ) : a object contain config of app, declared in appcfg.yaml file or hyron.setting method