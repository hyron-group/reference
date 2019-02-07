Used to run server used json files

## Features

-   JSON with light syntax
-   Support for multi instance
-   Support load from multi file
-   Support download missing module (used yarn engine)

# Details

## 1. JSON with light syntax

Hyron now support to build a app with a JSON file. This allows you to easily manage your application even easier than that. with JSON syntax, which is already familiar to programmers, because of its friendliness, ease of learning, and can be read with people who don't know the code

You can use this json file to declare instances, addons, plugins, services, settings for the application (support for most basic functions in ModuleManager)

In the future, we plan to make it more powerful with CLI tools, allowing you to easily share and deploy your application with it.

### To use json build file

Used method [ModuleManager.build](../api-reference/ModuleManager.md#function_build) to reference to a json build file

index.js
```js
const hyron = require("hyron");

hyron.build(jsonBuildFile);
```

Below is some attributes you should to remember

```json
// this is single instance meta
{
    // like ModuleManager.getInstance
    "base_url" : "http://localhost:80/demo",
    "server" : {
        "host" : "localhost",
        "port" : 80,
        "prefix" : "demo",
        "protocol" : "http"
    },

    // like ModuleManager.setting
    "setting" : {
        ...
    },

    // like ModuleManager.enableAddons
    "addons" : {
        "name" : "path"
    },

    // like ModuleManager.enablePlugins
    "plugins" : {
        "name" : "path"
    },

    // like ModuleManager.enableServices
    "services" : {
        "api" : "path"
    }
}
```

to register global addons

```js
[
    {
        // a object only contain addons properties
        addons: {
            // global addons map
        }
    },

    {
        // instance meta
    }
];
```

## 2. Support for multi instance

You can declare multi instance in same a JSON file with follow syntax

```json
// start as a array of instance
[
    {
        // instance meta
        "base_url": "http://localhost:3000/docs",
        ...
    },
    {
        // instance meta
        "base_url": "http://localhost:3000/api",
        ...
    },
    ...
]
```

As you see, if JSON build file start as a object '{ ... }' it will create only instance. But, you wrap it with a aray '[ ... ]', then, you can declared multi instance inside

## 3. Support load from multi file

if you have multi instance, with great length, you could separate you instances to multi file under a directory

Example :

build/app.json

```json
[
    "./build/api-instance.json",
    "./build/docs-instance.json",
    ...
]
```

As you see, if you declare data type as string instead object, you could make it referenced corresponding path from root

## 4. Support download missing module

When build file loaded, Hyron will check if the modules you declared are installed by checking it in the package.json file

If the file has not yet existed, it will proceed to download it quickly, before building the application

Hyron uses the yarn engine to download, it is an extremely fast and stable engine (more than npm-install), you should also use them later.

If you are missing, you will automatically install ``yarn`` on your computer

For more information about sources you can install, please refer to https://yarnpkg.com/en/docs/cli/add