---
stoplight-id: s6z0s7fg654e6
---

# Menu Selectors

* [getMenuById](#getmenubyid)

## getMenuById

Retrieves entries of a service menu by its ID from the menu data in the store.

### Usage

```javascript
import { getMenuById } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getMenuById } from '@shopgate/pwa-common/selectors/menu'`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` _(Object)_ **required**: The menu properties.
  * `id` _(string)_ **required**: The ID of the menu.

### Returns

_(Object)_: The service menu data. If no menu data is found, it returns an empty object -  `{}`.