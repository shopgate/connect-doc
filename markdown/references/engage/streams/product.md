---
stoplight-id: q0t646h0won28
---

# Product Streams

* [productWillEnter$](#productwillenter)
* [variantWillUpdate$](#variantwillupdate)
* [galleryWillEnter$](#gallerywillenter)
* [galleryWillLeave$](#gallerywillleave)
* [productReceived$](#productreceived)
* [cachedProductReceived$](#cachedproductreceived)
* [receivedVisibleProduct$](#receivedvisibleproduct)
* [variantDidChange$](#variantdidchange)
* [productRelationsReceived$](#productrelationsreceived)

## productWillEnter$

Triggers when the product route prepares to enter.

### Usage

```javascript
import { productWillEnter$ } from '@shopgate/engage/product';

subscribe(productWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { productWillEnter$ } from '@shopgate/pwa-common-commerce/product'`

---

## variantWillUpdate$

Triggers when a variant is chosen and the route prepares to update.

### Usage

```javascript
import { variantWillUpdate$ } from '@shopgate/engage/product';

subscribe(variantWillUpdate$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { variantWillUpdate$ } from '@shopgate/pwa-common-commerce/product'`

---

## galleryWillEnter$

Triggers when the product image gallery route prepares to enter.

### Usage

```javascript
import { galleryWillEnter$ } from '@shopgate/engage/product';

subscribe(galleryWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { galleryWillEnter$ } from '@shopgate/pwa-common-commerce/product'`

---

## galleryWillLeave$

Triggers when the product image gallery route prepares to leave.

### Usage

```javascript
import { galleryWillLeave$ } from '@shopgate/engage/product';

subscribe(galleryWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { galleryWillLeave$ } from '@shopgate/pwa-common-commerce/product'`

---

## productReceived$

Triggers when the product data is received.

### Usage

```javascript
import { productReceived$ } from '@shopgate/engage/product';

subscribe(productReceived$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { productReceived$ } from '@shopgate/pwa-common-commerce/product'`

---

## cachedProductReceived$

Triggers when the product data is retrieved from the store.

### Usage

```javascript
import { cachedProductReceived$ } from '@shopgate/engage/product';

subscribe(cachedProductReceived$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { cachedProductReceived$ } from '@shopgate/pwa-common-commerce/product'`

---

## receivedVisibleProduct$

Triggers when the data for the currently visible product is completely fetched.

### Usage

```javascript
import { receivedVisibleProduct$ } from '@shopgate/engage/product';

subscribe(receivedVisibleProduct$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { receivedVisibleProduct$ } from '@shopgate/pwa-common-commerce/product'`

---

## variantDidChange$

Triggers when a product variant changes.

### Usage

```javascript
import { variantDidChange$ } from '@shopgate/engage/product';

subscribe(variantDidChange$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { variantDidChange$ } from '@shopgate/pwa-common-commerce/product'`

---

## productRelationsReceived$

Triggers when the product relations are received.

### Usage

```javascript
import { productRelationsReceived$ } from '@shopgate/engage/product';

subscribe(productRelationsReceived$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { productRelationsReceived$ } from '@shopgate/pwa-common-commerce/product'`