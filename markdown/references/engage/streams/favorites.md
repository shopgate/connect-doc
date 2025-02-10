---
stoplight-id: odkxm377rv6nq
---

# Favorites Streams

* [favoritesWillEnter$](#favoriteswillenter)
* [addProductToFavoritesDebounced$](#addProductToFavoritesDebounced)
* [removeProductFromFavoritesDebounced$](#removeProductFromFavoritesDebounced)
* [favoritesError$](#favoriteserror)
* [errorFavoritesLimit$](#errorFavoritesLimit)
* [shouldFetchFavorites$](#shouldfetchfavorites)
* [shouldFetchFreshFavorites$](#shouldfetchfreshfavorites)
* [favoritesDidUpdate$](#favoritesdidupdate)
* [favoritesWillAddItem$](#favoritesWillAddItem)
* [favoritesDidAddItem$](#favoritesDidAddItem)
* [favoritesWillRemoveItem$](#favoriteswillremoveitem)
* [favoritesDidRemoveItem$](#favoritesDidRemoveItem)
* [receiveFavorites$](#receiveFavorites)
* [favoritesSyncIdle$](#favoritessyncidle)
* [refreshFavorites$](#refreshFavorites)
* [didRequestFlushFavoritesBuffer$](#didRequestFlushFavoritesBuffer)
* [didReceiveFlushFavoritesBuffer$](#didReceiveFlushFavoritesBuffer)

## favoritesWillEnter$

Triggers when the favorites route prepares to enter.

### Usage

```javascript
import { favoritesWillEnter$ } from '@shopgate/engage/favorites';

subscribe(favoritesWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesWillEnter$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## addProductToFavoritesDebounced$

Triggers when the debounce time on adding favorites passes.

### Usage

```javascript
import { addProductToFavoritesDebounced$ } from '@shopgate/engage/favorites';

subscribe(addProductToFavoritesDebounced$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { addProductToFavoritesDebounced$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## removeProductFromFavoritesDebounced$

Triggers when the debounce time on removing favorites passes.

### Usage

```javascript
import { removeProductFromFavoritesDebounced$ } from '@shopgate/engage/favorites';

subscribe(removeProductFromFavoritesDebounced$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { removeProductFromFavoritesDebounced$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesError$

Triggers if there is an error when fetching the favorites.

### Usage

```javascript
import { favoritesError$ } from '@shopgate/engage/favorites';

subscribe(favoritesError$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesError$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## errorFavoritesLimit$

Triggers when errors related to the frontend part of the favorites list occur.

### Usage

```javascript
import { errorFavoritesLimit$ } from '@shopgate/engage/favorites';

subscribe(errorFavoritesLimit$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { errorFavoritesLimit$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## shouldFetchFavorites$

Triggers when Engage starts or the favorites route prepares to enter.

### Usage

```javascript
import { shouldFetchFavorites$ } from '@shopgate/engage/favorites';

subscribe(shouldFetchFavorites$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { shouldFetchFavorites$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## shouldFetchFreshFavorites$

Triggers when the user logs in or out or if there is an error when fetching the favorites.

### Usage

```javascript
import { shouldFetchFreshFavorites$ } from '@shopgate/engage/favorites';

subscribe(shouldFetchFreshFavorites$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { shouldFetchFreshFavorites$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesDidUpdate$

Triggers when the user updates the favorites or the favorites update as a result from the backend.

### Usage

```javascript
import { favoritesDidUpdate$ } from '@shopgate/engage/favorites';

subscribe(favoritesDidUpdate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesDidUpdate$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesWillAddItem$

Triggers when an "add to favorites" action is placed into the favorites buffer.

### Usage

```javascript
import { favoritesWillAddItem$ } from '@shopgate/engage/favorites';

subscribe(favoritesWillAddItem$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesWillAddItem$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesDidAddItem$

Triggers when a single product is successfully added to favorites.

### Usage

```javascript
import { favoritesDidAddItem$ } from '@shopgate/engage/favorites';

subscribe(favoritesDidAddItem$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesDidAddItem$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesWillRemoveItem$

Triggers when a "remove from favorites" action is placed into the favorites buffer.

### Usage

```javascript
import { favoritesWillRemoveItem$ } from '@shopgate/engage/favorites';

subscribe(favoritesWillRemoveItem$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesWillRemoveItem$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesDidRemoveItem$

Triggers when a single product is successfully removed from favorites.

### Usage

```javascript
import { favoritesDidRemoveItem$ } from '@shopgate/engage/favorites';

subscribe(favoritesDidRemoveItem$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesDidRemoveItem$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## receiveFavorites$

Triggers when the favorites are successfully received.

### Usage

```javascript
import { receiveFavorites$ } from '@shopgate/engage/favorites';

subscribe(receiveFavorites$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { receiveFavorites$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## favoritesSyncIdle$

Triggers when all favorites changes are successfully processed, or once any of the queued (or buffered) change requests fail.

### Usage

```javascript
import { favoritesSyncIdle$ } from '@shopgate/engage/favorites';

subscribe(favoritesSyncIdle$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { favoritesSyncIdle$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## refreshFavorites$

Triggers when the favorites should be refreshed to maintain data consistency.

### Usage

```javascript
import { refreshFavorites$ } from '@shopgate/engage/favorites';

subscribe(refreshFavorites$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { refreshFavorites$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## didRequestAddOrRemoveFavorites$

Triggers when a product is requested to be added to or removed from favorites.

### Usage

```javascript
import { didRequestAddOrRemoveFavorites$ } from '@shopgate/engage/favorites';

subscribe(didRequestAddOrRemoveFavorites$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { didRequestAddOrRemoveFavorites$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## didRequestFlushFavoritesBuffer$

Triggers when the favorites action buffer should be flushed immediately.

### Usage

```javascript
import { didRequestFlushFavoritesBuffer$ } from '@shopgate/engage/favorites';

subscribe(didRequestFlushFavoritesBuffer$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { didRequestFlushFavoritesBuffer$ } from '@shopgate/pwa-common-commerce/favorites'`

---

## didReceiveFlushFavoritesBuffer$

Triggers when the favorites action buffer should be flushed immediately.

### Usage

```javascript
import { didReceiveFlushFavoritesBuffer$ } from '@shopgate/engage/favorites';

subscribe(didReceiveFlushFavoritesBuffer$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { didReceiveFlushFavoritesBuffer$ } from '@shopgate/pwa-common-commerce/favorites'`