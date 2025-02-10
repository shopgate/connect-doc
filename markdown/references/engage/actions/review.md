---
stoplight-id: kv24fsxs2ubu8
---

# Reviews Actions

* [fetchProductReviews](#fetchproductreviews)
* [fetchReviews](#fetchreviews)
* [fetchUserReview](#fetchuserreview)
* [flushUserReview](#flushuserreview)
* [submitReview](#submitreview)

## fetchProductReviews

Requests product reviews from the server.

### Usage

```javascript
import { fetchProductReviews } from '@shopgate/engage/reviews';

const productId = '25',
const limit = 5,
const sort = 'priceAsc',

dispatch(fetchProductReviews(productId, limit, sort));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchProductReviews } from '@shopgate/pwa-common-commerce/reviews'`

### Parameters

* `productId` *(string)*: The product ID.
* `limit` *(number)*: The maximum number of reviews to fetch. Default is set to 2.
* `sort` *(string)*: The sort scheme. Default is by relevance.
  * Possible Values: `relevance`, `dateAsc`, `dateDesc`, `rateAsc`, and `rateDesc`.  All of these values are constants. They can be imported like this:

```javascript
import { SORT_RELEVANCE, SORT_DATE_ASC, SORT_DATA_DESC, SORT_RATE_ASC, SORT_RATE_DEC } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { SORT_RELEVANCE, SORT_DATE_ASC, SORT_DATA_DESC, SORT_RATE_ASC, SORT_RATE_DEC } from '@shopgate/pwa-common/constants/DisplayOptions'`

---

## fetchReviews

Requests product reviews by the given ID from the server.

### Usage

```javascript
import { fetchReviews } from '@shopgate/engage/reviews'

const productId = '25',
const limit = 5,
const offset = 2,
const sort = 'priceAsc',

dispatch(fetchReviews(productId, limit, offset, sort));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchReviews } from '@shopgate/pwa-common-commerce/reviews'`

### Parameters

* `productId` *(string)*: The product ID.
* `limit` *(number)*: The maximum number of reviews to fetch. Default is set to 2.
* `offset` *(number)*: The review list offset. Default is 0.
* `sort` *(string)*: The sort scheme. Default is by relevance.
  * Possible Values: `relevance`, `dateAsc`, `dateDesc`, `rateAsc`, and `rateDesc`.  All of these values are constants. They can be imported like this:

```javascript
import { SORT_RELEVANCE, SORT_DATE_ASC, SORT_DATA_DESC, SORT_RATE_ASC, SORT_RATE_DEC } from '@shopgate/engage/core';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { SORT_RELEVANCE, SORT_DATE_ASC, SORT_DATA_DESC, SORT_RATE_ASC, SORT_RATE_DEC } from '@shopgate/pwa-common/constants/DisplayOptions'`

---

## fetchUserReview

Requests a user review for a product from the server.

### Usage

```javascript
import { fetchUserReview } from '@shopgate/engage/reviews'

const productId = '25';

dispatch(fetchUserReview(productId))
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { fetchUserReview } from '@shopgate/pwa-common-commerce/reviews'`

### Parameters

* `productId` *(string)*: The product ID.

---

## flushUserReview

Removes the relation between the user and their reviews when a user is logged out.

### Usage

```javascript
import { flushUserReview } from '@shopgate/engage/reviews'

dispatch(flushUserReview());
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { flushUserReview } from '@shopgate/pwa-common-commerce/reviews'`

---

## submitReview

Submits a user review for a product to the server.

### Usage

```javascript
import { submitReview } from '@shopgate/engage/reviews'

const review = {
  'author': 'Bill Demapps',
  'productId': '25',
  'rate': 75,
  'review': 'Loved it!',
  'title': 'Works Great',
};

const update = true;

dispatch(submitReview(review, update));
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { submitReview } from '@shopgate/pwa-common-commerce/reviews'`

### Parameters

* `review` *(Object)*: The review data.
* The required fields are `rate`, `title`, `review`, `author`, and `productId`.
* `update` *(boolean)*: Indicates whether the update pipeline or the add pipeline is called.