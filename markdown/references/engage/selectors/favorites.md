---
stoplight-id: gnxeoqfg11gbl
---

# Favorites Selectors

* [getFavoritesProducts](#getfavoritesproducts)
* [getFavoritesProductsIds](#getfavoritesproductsids)
* [getFavorites](#getfavorites)
* [isInitialLoading](#isinitialloading)
* [getFavoritesCount](#getfavoritescount)
* [hasFavorites](#hasfavorites)
* [isFetching](#isfetching)
* [isCurrentProductOnFavoriteList](#iscurrentproductonfavoritelist)

## getFavoritesProducts

Retrieves the current product stack from the favorites data in the store.

### Usage

```javascript
import { getFavoritesProducts } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFavoritesProducts } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Object|null)*: Returns the current products stack. If the product stack is not set yet, it returns `null`.

---

## getFavoritesProductsIds

Retrieves a collection of product IDs for the current products in the favorite list from the favorites data in the store.

### Usage

```javascript
import { getFavoritesProductsIds } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFavoritesProductsIds } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: A collection of product IDs. It returns an empty array as a default.

---

## getFavorites

Retrieves a collection of product data with all products that are in the favorite list from the favorites data in the store.

### Usage

```javascript
import { getFavorites } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFavorites } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: A collection of product data.

---

## isInitialLoading

Retrieves whether the favorite list is loading the very first time.

### Usage

```javascript
import { isInitialLoading } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isInitialLoading } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the favorite list loads for the first time.

---

## getFavoritesCount

Retrieves the number of products in the favorite list from the favorites data in the store.

### Usage

```javascript
import { getFavoritesCount } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFavoritesCount } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number)*: The number of products in the favorite list.

---

## hasFavorites
Retrieves whether the favorite list has any products.

### Usage

```javascript
import { hasFavorites } from '@shopgate/pwa-common-commerce/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasFavorites } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* *`state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the favorite list has products.

---

## isFetching

Retrieves whether the favorite list is currently fetching data.

### Usage

```javascript
import { isFetching } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isFetching } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the favorite list is fetching data.

---

## isCurrentProductOnFavoriteList

Retrieves whether the currently viewed product (inside a product list or on a product detail page) is already inside the favorite list.

### Usage

```javascript
import { isCurrentProductOnFavoriteList } from '@shopgate/engage/favorites';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isCurrentProductOnFavoriteList } from '@shopgate/pwa-common-commerce/favorites'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing properties.
  * `productId` *(string)* __required__: The product ID to check for.

### Returns

*(boolean)*: Whether the product is in the favorite list.