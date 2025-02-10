---
stoplight-id: 4223kaw1ca1ei
---

# Item write review (review composer)
The Item Write Review page allows the user to write new reviews for a product. This page **SHOULD NOT** be linked from the outside, except if you are adding a link to the reviews composer on a default Item page.

## How to customize
The Item Write Review page does not offer any page specific portals.

## How to link
You can link directly to a selected item review composer `productId` param. **Please note** that `productId` MUST be converted into a hex string in order to ensure URL-safe string usage.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { ITEM_PATH } from '@shopgate/engage/product';
import { bin2hex } from '@shopgate/engage/core';

/**
 * @param {string} productId Plain text product id.
 **/
const Component = ({ productId, slideNum }) => (
    <Link href={`${ITEM_PATH}/${bin2hex(productId}/write_review`}>Open product review composer</Link>
);

export default Component;
```