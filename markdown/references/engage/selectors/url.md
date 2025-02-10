---
stoplight-id: 727jkb509orfl
---

# URL Selectors

* [getUrl](#geturl)

## getUrl

Retrieves the URL for a given type from the store.

### Usage

```javascript
import { getUrl } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getUrl } from '@shopgate/pwa-common/selectors/url';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `type` _(string)_ **required**: The URL type.
    * Possible Values: `checkout`, `register`.

### Returns
_(string|null)_: The requested URL. If no URL is found, it returns `null`.