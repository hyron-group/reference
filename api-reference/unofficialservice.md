---
description: Used for packaging for a service that is not officially supported by hyron
---

# UnofficialService

function [handler](unofficialservice.md#function-handler)\(app, cfg\) : void

## Details

### function **handler**

The function is used to register a router in other cases that the hyron or addons from third parties do not yet support

#### ★ Params

```typescript
function handler(app, cfg) : void
```

| name | type | description |
| :--- | :--- | :--- |
| app | Server | server to handle client request and response. default is http.Server |
| cfg | object | The object containing the config on this service, described in appcfg |

