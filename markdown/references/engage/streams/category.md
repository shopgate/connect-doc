---
stoplight-id: jbu9idz0sa39a
---

# Category Streams

* [categoryWillEnter$](#categorywillenter)
* [categoryDidEnter$](#categorydidenter)
* [categoryDidLeave$](#categorydidleave)
* [receivedRootCategories$](#receivedrootcategories)
* [categoryError$](#categoryerror)

## categoryWillEnter$

Triggers when a category route prepares to enter.

### Usage

```javascript
import { categoryWillEnter$ } from '@shopgate/engage/category';

subscribe(categoryWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { categoryWillEnter$ } from '@shopgate/pwa-common-commerce/category'`

---

## categoryDidEnter$

Triggers when a category route enters.

### Usage

```javascript
import { categoryDidEnter$ } from '@shopgate/engage/category';

subscribe(categoryDidEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { categoryDidEnter$ } from '@shopgate/pwa-common-commerce/category'`

---

## categoryDidLeave$

Triggers when a category route leaves.

### Usage

```javascript
import { categoryDidLeave$ } from '@shopgate/engage/category';

subscribe(categoryDidLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { categoryDidLeave$ } from '@shopgate/pwa-common-commerce/category'`

---

## receivedRootCategories$

Triggers when the root category data is received.

### Usage

```javascript
import { receivedRootCategories$ } from '@shopgate/engage/category';

subscribe(receivedRootCategories$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { receivedRootCategories$ } from '@shopgate/pwa-common-commerce/category'`

---

## categoryError$

Triggers if there is an error in any of the category data requests.

### Usage

```javascript
import { categoryError$ } from '@shopgate/engage/category';

subscribe(categoryError$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { categoryError$ } from '@shopgate/pwa-common-commerce/category'`