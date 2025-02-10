---
stoplight-id: 1onzpm2jid7hb
---

# Routes
Shopgate Engage supports many routes out of the box in order to provide a full e-commerce experience.

You can customize these routes using [Portals](/references/engage/portals).

You cannot [register your custom route](/guides/technical/engage/creating-custom-routes) under a default pattern or path name. This would result in duplicated content - default and custom.

However, you can customize most of the default content. You can find more information about possible customizations on route pages.

## Default routes list

- [Home page](/references/engage/routes/home)
- [Category](/references/engage/routes/category)
- [Search](/references/engage/routes/search)
- [Category and Search Filter](/references/engage/routes/category-search-filter)
- [Cart](/references/engage/routes/cart)
- [Browse](/references/engage/routes/browse)
- [Favorites](/references/engage/routes/favorites)
- [Item](/references/engage/routes/item)
- [Item Gallery](/references/engage/routes/item-gallery)
- [Item Reviews](/references/engage/routes/item-reviews)
- [Item Write Review](/references/engage/routes/item-write-review)
- [Login](/references/engage/routes/login)
- [More](/references/engage/routes/more)
- [Scanner](/references/engage/routes/scanner)

## All default routes pathname and patterns

```javascript
import {
    INDEX_PATH 
} from '@shopgate/engage/core';

import {
    ITEM_PATH,
    ITEM_PATTERN,
    ITEM_GALLERY_PATTERN,
    ITEM_REVIEWS_PATTERN,
    ITEM_WRITE_REVIEW_PATTERN,
} from '@shopgate/engage/product';

import {
    CART_PATH,
} from '@shopgate/engage/cart';

import {
    CATEGORY_PATH,
    ROOT_CATEGORY_PATTERN,
    CATEGORY_PATTERN,
    CATEGORY_FILTER_PATTERN,
} from '@shopgate/engage/category';

import {
    FAVORITES_PATH,
} from '@shopgate/engage/favorites';

import {
    PAGE_PATH,
} from '@shopgate/engage/page';

import {
    SEARCH_PATH,
    SEARCH_PATTERN,
} from '@shopgate/engage/search';
```

### How to use it?
All the `*_PATTERN` constants are useful when trying to check what the current page is. For example:

```javascript
const itemRouteDidEnter$ = routeDidEnter$.filter(({ action }) => (
    action.route.pattern === ITEM_PATTERN
  ));
```

Sometimes there is no `*_PATTERN` constant. This occurs when there is no need for a pattern because routes always have the same pathname. For example, `FAVORITES_PATH` which is `/favorites` (without params).