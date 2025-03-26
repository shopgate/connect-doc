---
stoplight-id: pt6gdelhxek4l
---

# Router Selectors

* [getRouterStack](#getRouterStack)
* [getCurrentRoute](#getCurrentRoute)
* [getCurrentParams](#getCurrentParams)
* [getCurrentPathname](#getCurrentPathname)
* [getCurrentQuery](#getCurrentQuery)
* [getCurrentSearchQuery](#getCurrentSearchQuery)
* [getCurrentState](#getCurrentState)

## getRouterStack

Retrieves the router stack from the store.

### Usage

```javascript
import { getRouterStack } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getRouterStack } from '@shopgate/pwa-common/selectors/router';`

### Returns
_(Array|[])_: The current router stack. If the stack is empty, it returns `[]`.

### Example Result
```javascript
[{
  id: 'juicb',
  pattern: '/',
  pathname: '/',
  location: '/',
  params: {},
  query: {},
  hash: null,
  state: {},
  created: 1562587961638,
  updated: 1562588028967,
}, {
  id: 'sb5tk',
  pattern: '/category/:categoryId',
  pathname: '/category/3637',
  location: '/category/3637?sort=priceAsc#some-hash',
  params: {
    categoryId: '3637'
  },
  query: {
    sort: 'priceAsc'
  },
  state: {
    title: 'My Page Title'
  },
  hash: 'some-hash',
  created: 1562587961738,
  updated: 1562588029967,
}]
```

---

## getCurrentRoute

Retrieves the current visible route from the store.

### Usage

```javascript
import { getCurrentRoute } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentRoute } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(Object|null)_: The route object. If nothing was found, it returns `null`.

### Example Data
```javascript
{
  id: 'sb5tk',
  pattern: '/category/:categoryId',
  pathname: '/category/3637',
  location: '/category/3637?sort=priceAsc#some-hash',
  params: {
    categoryId: '3637'
  },
  query: {
    sort: 'priceAsc'
  },
  state: {
    title: 'My Page Title'
  },
  hash: 'some-hash',
  created: 1562587961738,
  updated: 1562588029967,
}
```

---

## getCurrentParams

Retrieves the params of the current visible route from the store.

### Usage

```javascript
import { getCurrentParams } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentParams } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(Object|null)_: The params object. If nothing was found, it returns `null`.

---

## getCurrentPathname

Retrieves the pathname of the current visible route from the store.

### Usage

```javascript
import { getCurrentPathname } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentPathname } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(string|null)_: The pathname. If nothing was found, it returns `null`.

---

## getCurrentQuery

Retrieves the query of the current visible route from the store.

### Usage

```javascript
import { getCurrentQuery } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentQuery } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(Object|null)_: The query. If nothing was found, it returns `null`.

---

## getCurrentSearchQuery

Retrieves the search query (query parameter "s") of the current visible route from the store.

### Usage

```javascript
import { getCurrentSearchQuery } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentSearchQuery } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(string|null)_: The search query. If nothing was found, it returns `null`.

---

## getCurrentState

Retrieves the state of the current visible route from the store. A route state can be set via the `update` helper which is provided by the [useNavigation](../hooks.md#usenavigation) hook.

### Usage

```javascript
import { getCurrentState } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCurrentState } from '@shopgate/pwa-common/selectors/router';`

### Parameters

* `state` _(Object)_ **required**: The application state.
* `props` *(Object)* : An object containing props.
  * `routeId` _(string)_: Can be passed to select a specific route from the stack.

### Returns
_(Object|null)_: The route state. If nothing was found, it returns `null`.