---
description: Used to describe the information for a router
---

# RouterMeta

#### interface **RouterMeta**

* [method](routermeta.md#var-method) : string \| array&lt;string&gt;
* [frontware](routermeta.md#var-frontware) : Array&lt;string \| [Middleware.handle](middleware.md#function-handle)&gt;
* [backware](routermeta.md#var-backware) : Array&lt;string \| [Middleware.handle](middleware.md#function-handle)&gt;
* [plugins](routermeta.md#var-plugins) : Array&lt;string&gt;
* [handle](routermeta.md#function-handle) : Function
* [path](routermeta.md#var-path) : string
* [params](routermeta.md#var-params) : string

## Details

### **interface RouterMeta**

Is a metadata object contain information about routes

### 

### var method

```typescript
method : string | Array<string>
```

Specifies the method or list of methods that will be used to register the listener for this method. Include \( not case sensitive \) :

* Query type : `get`, `head`
* Body type : `post`, `put`, `patch`
* Special type : `all`, `private`



### var frontware

```typescript
frontware : Array<string|Middleware.handle>
```

The list of plugins will be run on this router by name, or turn off global plugins by marking with the character '!' in front of that name

You can also register a simple plugins with it You can also register a simple plugins with it if you pass a function into it



### var backware

```typescript
backware : Array<string|Middleware.handle>
```

The list of b plugins will be run on this router by name, or turn off global plugins backware by marking with the character '!' in front of that name

You can also register a simple plugins with it You can also register a simple plugins with it if you pass a function into it



### var plugins

```typescript
plugins : Array<string|Middleware.handle>
```

The list of plugins will be run on this router by name, or turn off global plugins by marking with the character '!' in front of that name

You can also register a simple plugins with it You can also register a simple plugins with it if you pass a function into it



### function handle

Specifies the main-handler for this router. If this function is not set, Hyron will select the function inside this class that have the name the same name declared for this RouterMeta. This attribute has a higher priority

#### ★ **Params**

```typescript
handle : Function
```

| name | type | description |
| :--- | :--- | :--- |
| argument | Array&lt;any&gt; | The variables are input as a result of frontware plugins |
| this | object | variable this with scope in this router. Description in HyronService |

#### ★ **Return**

| type | description |
| :--- | :--- |
| any | result of logic block that could be used as input of backware plugins |
| Promise&lt;any&gt; | Async function  with result could be used as input of backware plugins |



### var path

```typescript
path : string
```

Customize the path for this router instead of the default path. Use this attribute only when absolutely necessary, to ensure consistency and ease of editing later



### var params

```typescript
params : string
```

An attribute used by param-parser plugins allows to parse parameters from url strings following the path of this router \(start with ':' character\). Example `/:param1/param2` 

