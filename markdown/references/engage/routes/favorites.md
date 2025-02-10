---
stoplight-id: a4a9n4f7w12w7
---

# Favorites
The Favorites page shows customer's favorites products. If there are none, it shows empty favorites view.

May not be available, depending on shop configuration.

## How to customize
### Portals
Main portals available on Favorites page are listed on [Favorites List portals reference page](/references/engage/portals/favorites-list).

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { FAVORITES_PATH } from '@shopgate/engage/favorites';

const Component = () => (
    <Link href={FAVORITES_PATH}>Open favorites page</Link>
);

export default Component;
```