---
stoplight-id: yklsdrrmpyhop
---

# Category Route
Category route contains a list of shop categories and a product grid with infinite loading.

## How to customize content
### Portals
Main portals that can be found on category pages are:
- [Category](../portals/category.md)
- [Category List Item](../portals/category-list-item.md)
- [Product List Item](../portals/product-list-item.md)

## How to link
```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { CATEGORY_PATH } from '@shopgate/engage/category';

const Component = () => (
    <Link href={CATEGORY_PATH}>Open root category</Link>
);

export default Component;
```

You can also link to a specific category, if you know the category ID. **Please note** that the categoryId must be converted to a hex value in order to ensure URL-safe string usage.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { CATEGORY_PATH } from '@shopgate/engage/category';
import { bin2hex } from '@shopgate/engage/core';

/**
 * @param {string} categoryId Plain text category id
 **/
const Component = ({ categoryId }) => (
    <Link href={`${CATEGORY_PATH}/${bin2hex(categoryId}`}>Open root category</Link>
);

export default Component;
```