---
stoplight-id: 2ds5vijjqiq96
---

# Search Selectors

* [getSuggestions](#getsuggestions)
* [getSuggestionsFetchingState](#getsuggestionsfetchingstate)

## getSuggestions

Retrieves the search suggestions for a passed search phrase.

### Usage

```javascript
import { getSuggestions } from '@shopgate/engage/search'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getSuggestions } from '@shopgate/pwa-common-commerce/search'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `searchPhrase` *(string)* __required__: The search phrase to use.

### Returns

*(Array|null)*: The found suggestions. If no phrase is passed or no suggestions are found, it returns `null`.

---

## getSuggestionsFetchingState

Retrieves whether suggestions for a passed search phrase are currently fetching.

### Usage

```javascript
import { getSuggestionsFetchingState } from '@shopgate/engage/search'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getSuggestionsFetchingState } from '@shopgate/pwa-common-commerce/search'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `searchPhrase` *(string)* __required__: The search phrase to use.

### Returns

*(boolean)*: Whether the suggestions are currently fetching.