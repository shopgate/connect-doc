---
stoplight-id: x29nnah5ktgu5
---

# Item Gallery
The Item Gallery page, just like the Category Filters page, is an internal route and **SHOULD NOT** be linked from the outside.

The only exception when you should link to the Item Gallery page is when you want to do it on [Item route](item.md). For example, by exchanging the entire `ProductImage` component rendered on the Item page. 

You can do that by using [`product.image`](../portals/product-details.md) portal. This way, you can decide if you want to implement your own Image Gallery or link to an existing one.

This route expects that [Item route](item.md) is right behind in the history stack. Linking to it from other pages might result in some unexpected problems with navigation.

## How to customize
The Item Gallery page does not offer any page specific portals.

## How to link
You can link directly to a selected item gallery using `productId` param. **Please note** that `productId` MUST be converted into a hex string in order to ensure URL-safe string usage.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { ITEM_PATH } from '@shopgate/engage/product';
import { bin2hex } from '@shopgate/engage/core';

/**
 * @param {string} productId Plain text product id.
 * @param {number} slideNum Slide index.
 **/
const Component = ({ productId, slideNum }) => (
    <Link href={`${ITEM_PATH}/${bin2hex(productId}/gallery/${slideNum}`}>Open product gallery</Link>
);

export default Component;
```