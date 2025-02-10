---
stoplight-id: e8kptbvqto9nl
---

# Page Selectors

* [getPageConfigById](#getpageconfigbyid)

## getPageConfigById

Retrieves the page configuration for a page ID from the store.

### Usage

```javascript
import { getPageConfigById } from '@shopgate/engage/page';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getPageConfigById } from '@shopgate/pwa-common/selectors/page'`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` _(Object)_ **required**: The component props.
  * `pageId` _(string)_ **required**: The page ID to retrieve the configuration for.

### Returns

_(Object|null)_: The page configuration for the given ID. If no configuration is found, it returns `null`.