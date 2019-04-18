---
description: Used to package processing functions for a frontware or backware
---

# Middleware

#### interface **Middleware**

* [**handle**](middleware.md#function-handle)\( req, res, prev, cfg \) : any \| Promise&lt; any &gt;
* [**onCreate**](middleware.md#function-oncreate) \( cfg \) : any \| Promise&lt; any &gt;
* [**checkout**](middleware.md#function-checkout) \( done, cfg \) : boolean \| Promise&lt; boolean &gt;
* [**typeFilter**](middleware.md#var-typefilter) : Array&lt; any &gt;
* [**global**](middleware.md#var-global) : boolean



## Details

### interface **Middleware**

It used to declare middleware that used to run before or after each services



### function handle

This is a heart of a plugins. It will be called when a request has make. Used to handle input or output data or something else

This function has the ability to access the 'this' variable of this route

#### ★ **Params**

```typescript
handle( req, res, prev, cfg ) : any|Promise<any>
```

| name | type | description |
| :--- | :--- | :--- |
| req | IncomingMessange | contain request data from client |
| res | ServerResponse | contain response from server |
| prev | any | preview result from abort plugins or main-handler if it is a first backware |
| cfg | any | config of this plugins |
| **this** | object | variable this with scope in this router |

#### ★ **Return**

| type | description |
| :--- | :--- |
| any \| Promise&lt;any&gt;  | A result that could be used by bellow plugins, or as main-handler function if it is last frontware. It also support for async function or function return with a Promise |



### function onCreate

This function called for the fist time request of this instance has make. Used to prepare value for later activities

This function has the ability to access the 'this' variable of this route

#### ★ **Params**

```typescript
onCreate(cfg) : void | Promise<void>
```

| name | type | description |
| :--- | :--- | :--- |
| cfg | object | config of this plugins |
| **this** | object | variable this with scope in this router |

#### ★ **Return**

| type | description |
| :--- | :--- |
| void \| Promise&lt;void&gt;  | it not required, just notify in async case that it completed |



### function checkout

Used to check if some value has changed. If a change has make, onCreate will be revoke again

This function has the ability to access the 'this' variable of this route

#### ★ **Params**

```typescript
checkout(done, cfg) : boolean | Promise<boolean>
```

| name | type | description |
| :--- | :--- | :--- |
| done | Function | a function that used to break life circle loops |
| cfg | object | config of this plugins |
| **this** | this | variable this with scope in this router |

#### ★ **Return**

| type | description |
| :--- | :--- |
| boolean \| Promise&lt;boolean&gt; | true if has change, or not |



### var typeFilter

```typescript
typeFilter : Array<any>
```

It is used to filter which type of data from prev will be processed. if type of [`prev`](middleware.md#params) don't contain in array. It will be skip



### var global

```typescript
global : boolean
```

Used to turn on global mode. Meanwhile, this middleware will be called automatically on each router.

In addition, it can also be turned off in requestConfig -&gt; frontware / backware / plugins by adding a '!' character before this plugins name

