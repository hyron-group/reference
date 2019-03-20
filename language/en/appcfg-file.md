**appcfg.yaml** is file contain all of config or variable in app, include your app, plugins, addons and services
separate config from modules will help you easy to management and custom it modules. Besides, it could help you and another user can plugs your module with minimum effort

If you never work with 'yaml' before, please visit tutorial : [Yaml tutorial](https://www.tutorialspoint.com/yaml/index.htm)
It very easy to learn and use. You don't need worry about how to learn it

## Feature

-   Allow **Inheritance**, auto load at runtime
-   Allow **Lock Field**, ignore inherit
-   Allow **Multi Data Type**, power from yaml
-   Allow **Internal Referenced**, import from another field
-   Allow **External Referenced**, import from external file

# Details

## **1. Allow inheritance**

appcfg could be inherit kind like parent-child type.
It mean you can declare appcfg from itself your module and it could be implement and overwrite by parent (appcfg at root)

Hyron only detect and load declared appcfg from declared module, except module that publish by Hyron organization ( module start with **@hyron** ).

Hyron will prefer to load the config files in the following preferred order :

![](res/appcfg-priority.png)

As you can see, the hyron will prefer the load config first in sequence

self-hyron appcfg -> hyron organization modules appcfg -> your app appcfg -> your appcfg inside each modules

## **2. Look field**

This feature helps freeze sensitive fields from overwrite. Meaning that its value will be fixed and cannot be changed. To used this feature, Please add dollar character ('\$') before key name like follow syntax :

> ## \$key = val

Example :

```yaml
# this is a looked key
$database:
    db-name: test-db
    connection: # mongo-connection
```

## **3. Multi data type**

This feature provided by **yaml**. This could help you used multi datatype as value from javascript primitive type, include : **_string_**, **_number_**, **_boolean_**, **_array_**, **_object_**

## **4. Internal referenced**

This feature used to reference to another field in current file. This feature could make you can reuse another declared config.
To used internal import. Please use follow syntax :

> ### <#field_path>

with **_field_path_** is path to referenced field separated by dot character ('.')

Internal referenced also used multi time in same value

This will be compiled and import by Hyron at runtime. and used like js object

Example :

```yaml
key1:
    field1: hello world

# Internal referenced
ref_field: <#key1.field1>
```

## 5. **External referenced**

This feature that allow you can import setting from another file into current field. To used external referenced, please use follow syntax :

> ### <~yaml_file_path>

with **_yaml_file_path_** is link to another yaml config file

Example :
account-info.yaml

```yaml
name: test-db
collection: account
schema:
    id: string
    access_token: string
    type: string
```

appcfg.yaml

```yaml
account-service: <~./database/account-info.yaml>
```

# How to used

Using appcfg is very simple. Just declare it by create **appcfg.yaml** file in root or your modules. Hyron will load it at runtime.

Depending on your project size you can use appcfg in many different ways.

-   **If you just want to build simple app.** You just need to declare appcfg in root dir
-   **If you want to build a large application**, with modules that can be separated and reused. We recommend that you write appcfg of modules into it self directory

Hyron also supports some special fields ( only valid in root-appcfg and hyron-organization appcfg ), allowing you to better control your application (Commonly used in modules)

-   **fontware** : enable a global fontware
-   **backware** : enable a global backware
-   **plugins** : enable a global plugins
-   **addons** : enable a global addons
