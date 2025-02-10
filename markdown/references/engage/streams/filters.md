---
stoplight-id: nek40wf32yiju
---

# Filter Streams

* [filterWillEnter$](#filterwillenter)
* [filterDidEnter$](#filterdidenter)
* [filterWillLeave$](#filterwillleave)
* [filterDidLeave$](#filterdidleave)
* [filterableRoutesWillEnter$](#filterablerouteswillenter)
* [filterableRoutesWillReenter$](#filterablerouteswillreenter)
* [filterableRoutesWillLeave$](#filterablerouteswillleave)
* [filtersDidUpdate$](#filtersdidupdate)

## filterWillEnter$

Triggers when the filter route prepares to enter.

### Usage

```javascript
import { filterWillEnter$ } from '@shopgate/engage/filter';

subscribe(filterWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterWillEnter$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterDidEnter$

Triggers when the filter route enters.

### Usage

```javascript
import { filterDidEnter$ } from '@shopgate/engage/filter';

subscribe(filterDidEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterDidEnter$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterWillLeave$

Triggers when the filter route prepares to leave.

### Usage

```javascript
import { filterWillLeave$ } from '@shopgate/engage/filter';

subscribe(filterWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterWillLeave$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterDidLeave$

Triggers when the filter route leaves.

### Usage

```javascript
import { filterDidLeave$ } from '@shopgate/engage/filter';

subscribe(filterDidLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterDidLeave$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterableRoutesWillEnter$

Triggers when either a category route or a search route will enter. You can filter these routes.

### Usage

```javascript
import { filterableRoutesWillEnter$ } from '@shopgate/engage/filter';

subscribe(filterableRoutesWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterableRoutesWillEnter$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterableRoutesWillReenter$

Triggers when either a category route or a search route re-enters on a `POP` history action.

### Usage

```javascript
import { filterableRoutesWillReenter$ } from '@shopgate/engage/filter';

subscribe(filterableRoutesWillReenter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterableRoutesWillReenter$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filterableRoutesWillLeave$

Triggers when either a category route or a search route leaves.

### Usage

```javascript
import { filterableRoutesWillLeave$ } from '@shopgate/engage/filter';

subscribe(filterableRoutesWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filterableRoutesWillLeave$ } from '@shopgate/pwa-common-commerce/filter'`

---

## filtersDidUpdate$

Triggers when filter data updates.

### Usage

```javascript
import { filtersDidUpdate$ } from '@shopgate/engage/filter';

subscribe(filtersDidUpdate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { filtersDidUpdate$ } from '@shopgate/pwa-common-commerce/filter'`