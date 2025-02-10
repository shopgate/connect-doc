---
stoplight-id: fzzke8irde0my
---

# Favorites Actions

* [fetchFavorites](#fetchfavorites)
* [toggleFavorites](#togglefavorites)

## fetchFavorites

Retrieves favorites from the server.

### Usage

```javascript
import { fetchFavorites } from '@shopgate/engage/favorites';

dispatch(fetchFavorites());
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchFavorites } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `ignoreCache` *(boolean)*: Indicates whether to ignore the cache.

---

## toggleFavorites

Contains the `addFavorites` and `removeFavorites` functions. `addFavorites` is deprecated starting from Engage Theme version `6.7.0` and has been replaced with the `addFavorite` action.  

### Usage

```javascript
import { addFavorite, removeFavorites } from '@shopgate/engage/favorites';

const productId = '25';
const withRelatives = false;

dispatch(addFavorite(productId));
dispatch(removeFavorites(productId, withRelatives));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { addFavorites, removeFavorites } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `productId` *(string)* **required**: The ID of the product to add or remove from favorites.
* `withRelatives` *(boolean)*: Indicates whether relatives are also removed.