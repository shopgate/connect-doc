---
stoplight-id: ez6wemqy6yzqw
---

# Cart
The Cart page shows the customer's items that were added to the cart. If there are none, it shows empty cart view.

## How to customize
### Portals
Main portals that can be found on Cart page are listed on [Cart portals reference page](/references/engage/portals/cart).

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { CART_PATH } from '@shopgate/engage/cart';

const Component = () => (
    <Link href={CART_PATH}>Open cart</Link>
);

export default Component;
```