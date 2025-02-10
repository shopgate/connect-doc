---
stoplight-id: ykunvpstffjzl
---

# Search Actions

* [fetchSearchResults](#fetchsearchresults)
* [fetchSearchSuggestions](#fetchsearchsuggestions)

## fetchSearchResults

Retrieves products for a search query.

### Usage

```javascript
import { fetchSearchResults } from '@shopgate/engage/search';

const params = {
  offset: 0,
  searchPhrase: 'shoes',
  limit: 3,
  sort: 'priceAsc',
}
dispatch(fetchSearchResults(params));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchSearchResults } from '@shopgate/pwa-common-commerce/search'`

### Parameters

* `params` _(Object)_ **required**: The parameters for the products to request.
  * `searchPhrase` _(string)_ **required**: The search phrase.
  * `limit` _(number)_: The amount of items to get with a single request. Default is 30.
  * `offset` _(number)_: The offset for the request. Default is 0.
  * `sort` _(string)_: The sort scheme. Default is by relevance.
    * Possible Values: `relevance`, `priceAsc`, `priceDesc`, `random`.  All of these values are prepared as constants. Those can be imported like this:

```javascript
import { SORT_RELEVANCE, SORT_PRICE_ASC, SORT_PRICE_DESC, SORT_RANDOM } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { SORT_RELEVANCE, SORT_PRICE_ASC, SORT_PRICE_DESC, SORT_RANDOM } from '@shopgate/pwa-common/constants/DisplayOptions'`

---

## fetchSearchSuggestions

Retrieves suggestions for the currently ongoing search.

### Usage

```javascript
import { fetchSearchSuggestions } from '@shopgate/engage/search';

const searchPhrase = 'red';

dispatch(fetchSearchSuggestions(searchPhrase));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchSearchSuggestions } from '@shopgate/pwa-common-commerce/search'`

### Parameters

* `searchPhrase` _(string)_ **required**: The search phrase.