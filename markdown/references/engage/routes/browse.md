---
stoplight-id: c57gw897en79p
---

# Browse (iOS theme only)
The Browse page is a special iOS page that offers default search functionality (with barcode scanner) and category list.

## How to customize
### Portals
Main portals available on Browse page are listed on [Browse portals reference page](../portals/browse.md)

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';

const Component = () => (
    <Link href="/browse">Open browse page</Link>
);

export default Component;
```