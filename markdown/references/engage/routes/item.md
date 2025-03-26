---
stoplight-id: zlexc3wccn8m7
---

# Item
The Item page contains all product information, with additional controls like `VariantSelect`, `AddToFavorites`, `AddToCart`.

## How to customize content
### Portals
Main portals that can be found on the Item page are listed on [Product Details portals reference page](../portals/product-details.md).

### How to link
You can link directly to a selected item using `productId` param. **Please note** that `productId` MUST be converted into a hex string in order to ensure URL-safe string usage.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { ITEM_PATH } from '@shopgate/engage/product';
import { bin2hex } from '@shopgate/engage/core';

/**
 * @param {string} productId Plain text product id.
 **/
const Component = ({ productId }) => (
    <Link href={`${ITEM_PATH}/${bin2hex(productId}`}>Open product</Link>
);

export default Component;
```