---
stoplight-id: su9hh1e7spnqy
---

# Item reviews
The Item Reviews page shows product reviews and allows the customer to provide her/his own product reviews.

This page **SHOULD NOT** be linked from the outside except if you are adding a link to the reviews on a default Item page.

## How to customize
The Item Reviews page does not offer any page specific portals.

## How to link

You can link directly to a selected item reviews page using `productId` param. **Please note** that `productId` MUST be converted into a hex string in order to ensure URL-safe string usage.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { ITEM_PATH } from '@shopgate/engage/product';
import { bin2hex } from '@shopgate/engage/core';

/**
 * @param {string} productId Plain text product id.
 **/
const Component = ({ productId, slideNum }) => (
    <Link href={`${ITEM_PATH}/${bin2hex(productId}/reviews`}>Open product reviews list</Link>
);

export default Component;
```