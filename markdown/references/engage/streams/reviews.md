---
stoplight-id: p4k0ogj67m19s
---

# Reviews Streams

* [reviewsWillEnter$](#reviewswillenter)
* [reviewsWillLeave$](#reviewswillleave)
* [requestReviewSubmit$](#requestreviewsubmit)
* [responseReviewSubmit$](#responsereviewsubmit)
* [successReviewSubmit$](#successreviewsubmit)
* [errorReviewSubmit$](#errorreviewsubmit)
* [shouldFetchReviews$](#shouldfetchreviews)

## reviewsWillEnter$

Triggers when the reviews route prepares to enter.

### Usage

```javascript
import { reviewsWillEnter$ } from '@shopgate/engage/reviews';

subscribe(reviewsWillEnter$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { reviewsWillEnter$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## reviewsWillLeave$

Triggers when the reviews route prepares to leave.

### Usage

```javascript
import { reviewsWillLeave$ } from '@shopgate/engage/reviews';

subscribe(reviewsWillLeave$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { reviewsWillLeave$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## requestReviewSubmit$

Triggers when the user submits a review.

### Usage

```javascript
import { requestReviewSubmit$ } from '@shopgate/engage/reviews';

subscribe(requestReviewSubmit$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { requestReviewSubmit$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## responseReviewSubmit$

Triggers when a review submission receives a response.

### Usage

```javascript
import { responseReviewSubmit$ } from '@shopgate/engage/reviews';

subscribe(responseReviewSubmit$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { responseReviewSubmit$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## successReviewSubmit$

Triggers when a review is submitted successfully.

### Usage

```javascript
import { successReviewSubmit$ } from '@shopgate/engage/reviews';

subscribe(successReviewSubmit$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { successReviewSubmit$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## errorReviewSubmit$

Triggers when a review could not be submitted.

### Usage

```javascript
import { errorReviewSubmit$ } from '@shopgate/engage/reviews';

subscribe(errorReviewSubmit$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { errorReviewSubmit$ } from '@shopgate/pwa-common-commerce/reviews'`

---

## shouldFetchReviews$

Triggers when ever reviews should be fetched from the backend.

### Usage

```javascript
import { shouldFetchReviews$ } from '@shopgate/engage/reviews';

subscribe(shouldFetchReviews$, ({ action, dispatch, getState, prevState, events }) => {
  // The code you want to perform when the stream triggers.
})
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { shouldFetchReviews$ } from '@shopgate/pwa-common-commerce/reviews'`