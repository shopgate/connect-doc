---
stoplight-id: 2sswr4re52zir
---

# Filter Selectors

* [getFiltersByHash](#getfiltersbyhash)
* [getActiveFilters](#getactivefilters)
* [hasActiveFilters](#hasactivefilters)

## getFiltersByHash

Retrieves a collection of set filters by a result hash.

### Usage

```javascript
import { getFiltersByHash } from '@shopgate/engage/filters';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFiltersByHash } from '@shopgate/pwa-common-commerce/filters'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `categoryId` *(string)*: The category ID for the hash.
  * `searchPhrase` *(string)*: The search phrase for the hash

### Returns

*(Array|null)*: A collection of set filters. If there are no filters, it returns `null`.
> Filters will match the filters from the [getFilters](/references/connect/shopgate-pipelines/search/shopgate.catalog.getfilters.v1) pipeline response.

---

## getActiveFilters

Retrieves the currently active filters.

### Usage

```javascript
import { getActiveFilters } from '@shopgate/engage/filters';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getActiveFilters } from '@shopgate/pwa-common-commerce/filters'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array|null)*: A collection of set filters. If there are no filters, it returns `null`.

---

## hasActiveFilters

Retrieves whether there are any active filters set.

### Usage

```javascript
import { hasActiveFilters } from '@shopgate/engage/filters';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasActiveFilters } from '@shopgate/pwa-common-commerce/filters'`


### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether there are any active filters set.