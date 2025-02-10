---
stoplight-id: i35dhhx2usw5f
---

# Page Actions

* [fetchPageConfig](#fetchpageconfig)

## fetchPageConfig

Retrieves the configuration for a page.

### Usage

```js
import { fetchPageConfig } from '@shopgate/engage/page';

dispatch(fetchPageConfig('page_id'));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import fetchPageConfig from '@shopgate/pwa-common/actions/page/fetchPageConfig'`

### Parameters

* `pageId` *(string)*: The ID of the requested page.