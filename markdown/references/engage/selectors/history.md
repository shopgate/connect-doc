---
stoplight-id: 29kc6wwkkshz8
---

# History Selectors

* [getQueryParam](#getqueryparam)
* [getSortOrder](#getsortorder)
* [getSearchPhrase](#getsearchphrase)
* [getHistoryPathname](#gethistorypathname)
* [getHistoryLength](#gethistorylength)
* [getQueryParamsAsString](#getqueryparamsasstring)
* [getHistoryLocation](#gethistorylocation)
* [getRedirectLocation](#getredirectlocation)

## getQueryParam

Retrieves a single URL parameter from the query parameters object.

### Usage

```javascript
import { getQueryParam } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getQueryParam } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `param` _(String)_ **required**: The dedicated URL parameter.

### Returns

_(Array|null)_: The URL parameter value. If no parameter value is found, it returns `null`.

---

## getSortOrder

Retrieves the sort order from the URL query parameters.

### Usage

```javascript
import { getSortOrder } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getSortOrder } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The current sort order. If no sort order is found, it returns `null`.

---

## getSearchPhrase

Retrieves the search phrase from the URL query parameters.

### Usage

```javascript
import { getSearchPhrase } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getSearchPhrase } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The current search phrase. If no search phrase is found, it returns `null`.

---

## getHistoryPathname

Retrieves the current history path name.

### Usage

```javascript
import { getHistoryPathname } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getHistoryPathname } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string |null)_: The history path name. If no value is returned, the selector returns `null`.

---

## getHistoryLength

Retrieves the length of the current history stack.

### Usage

```javascript
import { getHistoryLength } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getHistoryLength } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(number|null)_: The current length of the history stack.

---

## getQueryParamsAsString

Retrieves the query parameters from the history state as a pre-formatted string.

### Usage

```javascript
import { getQueryParamsAsString } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getQueryParamsAsString } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The current query parameters.

---

## getHistoryLocation

Retrieves the history location from the history state.

### Usage

```javascript
import { getHistoryLocation } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getHistoryLocation } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The current history location. If no value is found, it returns `null`.

---

## getRedirectLocation

Retrieves the current redirect location from the history state.

### Usage

```javascript
import { getRedirectLocation } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getRedirectLocation } from '@shopgate/pwa-common/selectors/history'`

### Parameters

* `state` _(Object)_ **required**: The application state.

### Returns

_(string|null)_: The current redirect location. If no value is found, it returns `null`.