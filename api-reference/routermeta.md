# RouterMeta

#### interface **RouterMeta**

* [method](routermeta.md#var-method) : string \| array&lt;string&gt;
* [fontware](routermeta.md#var-fontware) : Array&lt;string \| Middleware.handle&gt;
* [backware](routermeta.md#var-backware) : Array&lt;string \| Middleware.handle&gt;
* [plugins](routermeta.md#var-plugins) : Array&lt;string&gt;
* handle : Function
* [path](routermeta.md#var-path) : string
* [params](routermeta.md#var-params) : string

## Details

### **interface RouterMeta**

Is a metadata object contain information about routes

### 

### var method

Specifies the methods that will be used to register the listener for this method. Include \( not case sensitive \) :

* Query type : `get`, `head`
* Body type : `post`, `put`, `patch`
* Special type : `all`, `private`

#### ★ Return

```typescript
method : string | Array<string>
```

| type | description |
| :--- | :--- |
| string | The method is used to register the router |
| Array&lt;string&gt; | The array of basic methods will be registered on it |



### var fontware

Turn on registered fontware of a plugins by name, or turn off fontware of global plugins by marking with the character '!' in front of that name

#### ★ Return

```typescript
fontware : Array<string|Middleware.handle>
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Array&lt;string | Middleware.handle&gt;</td>
      <td style="text-align:left">
        <p>The list of fontware plugins is enabled for this router.</p>
        <p>You also can register a new fontware with it</p>
      </td>
    </tr>
  </tbody>
</table>

### var backware

Turn on registered backware of a plugins by name, or turn off backware of global plugins by marking with the character '!' in front of that name

#### ★ Return

```typescript
backware : Array<string|Middleware.handle>
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">t</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Array&lt;string | Middleware.handle&gt;</td>
      <td style="text-align:left">
        <p>The list of backware plugins is enabled for this router.</p>
        <p>You also can register a new backware with it</p>
      </td>
    </tr>
  </tbody>
</table>

### var plugins

Turn on registered plugins by name, or turn off global plugins by marking with the character '!' in front of that name

#### ★ Return

```typescript
plugins : Array<string|Middleware.handle>
```

| type | description |
| :--- | :--- |
| Array&lt;string \| Middleware.handle&gt; | The list of plugins is enabled for this router. |



### function handle

Specifies the main-handler for this router. If this function is not set, Hyron will select the function inside this class that have the name the same name declared for this RouterMeta. This attribute has a higher priority

#### **Params**

```typescript
handle : Function
```

| name | type | description |
| :--- | :--- | :--- |
| argument | Array&lt;any&gt; | The variables are input as a result of fontware plugins |
| this | object | variable this with scope in this router. Description in HyronService |

#### **Return**

| type | description |
| :--- | :--- |
| any | result of logic block that could be used as input of backware plugins |
| Promise&lt;any&gt; | It also supports for async function |

* any \| Promise &lt; any &gt; : result of logic block that could be used as input of backware plugins

## var path

> ### **path** : string

Customize the path for this router instead of the default path. Use this attribute only when absolutely necessary, to ensure consistency and ease of editing later

## var params

> ### **params** : string

An attribute used by param-parser plugins allows to parse parameters from url strings following the path of this router

Use it with syntax : /:param1/param2 ...

#### Rule

* var name start with ':' character
* params will be followed after the path
* The variable from the param should only have a depth of less than 5

