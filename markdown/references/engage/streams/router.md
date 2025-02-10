---
stoplight-id: k5tzs9qbext37
---

# Router Streams

* [navigate$](#navigate)
* [routeWillEnter$](#routewillenter)
* [routeDidEnter$](#routedidenter)
* [routeWillLeave$](#routewillleave)
* [routeDidLeave$](#routedidleave)
* [routeDidChange$](#routedidchange)

## navigate$

Triggers on every routing action.

### Usage

```javascript
import { navigate$ } from '@shopgate/engage/core';

subscribe(navigate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { navigate$ } from '@shopgate/pwa-common/streams/router'`

---

## routeWillEnter$

Triggers before a route enters.

### Usage

```javascript
import { routeWillEnter$ } from '@shopgate/engage/core';

subscribe(routeWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { routeWillEnter$ } from '@shopgate/pwa-common/streams/router'`

---

## routeDidEnter$

Triggers when a route entered.

### Usage

```javascript
import { routeDidEnter$ } from '@shopgate/engage/core';

subscribe(routeDidEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { routeDidEnter$ } from '@shopgate/pwa-common/streams/router'`

---

## routeWillLeave$

Triggers before a route leaves.

### Usage

```javascript
import { routeWillLeave$ } from '@shopgate/engage/core';

subscribe(routeWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { routeWillLeave$ } from '@shopgate/pwa-common/streams/router'`

---

## routeDidLeave$

Triggers after the route leaves.

### Usage

```javascript
import { routeDidLeave$ } from '@shopgate/engage/core';

subscribe(routeDidLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { routeDidLeave$ } from '@shopgate/pwa-common/streams/router'`

---

## routeDidChange$

Triggers on any of the previous route changes.

> **Attention**: This stream is deprecated from *Engage v6.4.0*. Please use [`routeDidEnter$`](#routedidenter) instead.

### Usage

```javascript
import { routeDidChange$ } from '@shopgate/engage/core';

subscribe(routeDidChange$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { routeDidChange$ } from '@shopgate/pwa-common/streams/router'`