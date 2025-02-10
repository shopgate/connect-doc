---
stoplight-id: nu1k2rkm3o6ky
---

# Checkout Selectors

* [getCheckoutUrl](#getcheckouturl)

## getCheckoutUrl

Retrieves the current checkout URL from the store.

### Usage

```javascript
import { getCheckoutUrl } from '@shopgate/engage/checkout';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCheckoutUrl } from '@shopgate/pwa-common-commerce/checkout'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(string|null)* The checkout URL or `null` if no URL is found.