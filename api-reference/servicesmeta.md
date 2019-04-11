---
description: 'Used to describe information for a executer, used to register routers'
---

# ServiceMeta

#### interface **ServiceMeta**

* **$all** : RouterMeta \| RouterMeta.method
* \[ **method\_name**: string \] : RouterMeta \| RouterMeta.method

## Details

### interface **ServiceMeta**

Describe information for a mapping method. This information will be used by hyron to register the router and execute business logic along with plugins

### properties $all

Apply descriptions for all routers. It has a low priority, so you can override it at each router

#### Return

```typescript
$all : RouterMeta | RouterMeta.method
```

| type | description |
| :--- | :--- |
| RouterMeta | Contains descriptive information for this router |
| RouterMeta.method | The method will be used to register the router |

### 

### list \[method\_name\] 

List their mapping methods and descriptions, used by hyron to register the router

#### Result

```typescript
[ method_name: string ] : RouterMeta | RouterMeta.method
```

| type | description |
| :--- | :--- |
| method\_name | The corresponding method name is encapsulated in this class. it will be used as a child path url by default |
| RouterMeta | Contains descriptive information for this router |
| RouterMeta.method | The method will be used to register the router |

