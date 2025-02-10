---
stoplight-id: 5v4pfviu08wb8
---

# Search Streams

* [searchRequesting$](#searchrequesting)
* [searchReceived$](#searchreceived)
* [searchWillEnter$](#searchwillenter)
* [searchDidEnter$](#searchdidenter)
* [searchWillLeave$](#searchwillleave)
* [searchWillUpdate$](#searchwillupdate)

## searchRequesting$

Triggers when the search requests results.

### Usage

```javascript
import { searchRequesting$ } from '@shopgate/engage/search';

subscribe(searchRequesting$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchRequesting$ } from '@shopgate/pwa-common-commerce/search'`

---

## searchReceived$

Triggers when the search receives results.

### Usage

```javascript
import { searchReceived$ } from '@shopgate/engage/search';

subscribe(searchReceived$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchReceived$ } from '@shopgate/pwa-common-commerce/search'`

---

## searchWillEnter$

Triggers when the search route prepares to enter.

### Usage

```javascript
import { searchWillEnter$ } from '@shopgate/engage/search';

subscribe(searchWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchWillEnter$ } from '@shopgate/pwa-common-commerce/search'`

---

## searchDidEnter$

Triggers when the search route enters.

### Usage

```javascript
import { searchDidEnter$ } from '@shopgate/engage/search';

subscribe(searchDidEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchDidEnter$ } from '@shopgate/pwa-common-commerce/search'`

---

## searchWillLeave$

Triggers when the search route prepares to leave.

### Usage

```javascript
import { searchWillLeave$ } from '@shopgate/engage/search';

subscribe(searchWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchWillLeave$ } from '@shopgate/pwa-common-commerce/search'`

---

## searchWillUpdate$

Triggers when the search route prepares to update.

### Usage

```javascript
import { searchWillUpdate$ } from '@shopgate/engage/search';

subscribe(searchWillUpdate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { searchWillUpdate$ } from '@shopgate/pwa-common-commerce/search'`