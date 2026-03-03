---
stoplight-id: onb1jpm7vw8tj
---

# Category Actions

- [fetchCategory](#fetchcategory)
- [fetchCategoryChildren](#fetchcategorychildren)
- [fetchCategoryProducts](#fetchcategoryproducts)
- [fetchRootCategories](#fetchrootcategories)

## fetchCategory

Retrieves the data for a given category ID (including child categories).

### Usage

```javascript
import { fetchCategory } from '@shopgate/engage/category';

const categoryId = '25';

dispatch(fetchCategory(categoryId));
```

### Parameters

- `categoryId`_(string)_ **required**: The ID for the category to fetch.

---

## fetchCategoryChildren

Retrieves the child categories for a given category ID.

### Usage

```javascript
import { fetchCategoryChildren } from '@shopgate/engage/category';

const categoryId = '25';

dispatch(fetchCategoryChildren(categoryId));
```

### Parameters

- `categoryId`_(string)_ **required**: The ID for the category to fetch.

---

## fetchCategoryProducts

Retrieves category products by a category ID.

### Usage

```javascript
import { fetchCategoryProducts } from '@shopgate/engage/category';

const categoryId = '25';
const offset = 10;
const limit = 3;
const sort = 'priceAsc';
const filters = {
  display_amount: {
    minimum: 299,
    maximum: 4900
  },
  manufacturer: {
    values: ['Shopgate', 'ACME']
  }
}

dispatch(fetchCategoryProducts({categoryId, offset, limit, sort, filters}));
```

### Parameters

- `categoryId`_(string)_ **required**: The ID for the category to fetch.
- `offset`_(number)_: The offset for the products to request. Default is 0.
- `limit`_(number)_: The number of products to request. Default is 30 items.
- `filters` _(Object)_: Additional filters for the request.
- `sort`_(string)_: The sort scheme. Default is by relevance.
  - Possible Values: `relevance`, `priceAsc`, `priceDesc`.  All of these values are prepared as constants. They can be imported like this:

```javascript
import { SORT_RELEVANCE, SORT_PRICE_ASC, SORT_PRICE_DESC } from '@shopgate/engage/core';
```

---

## fetchRootCategories

Retrieves the root categories from the store.

### Usage

```javascript
import { fetchRootCategories } from '@shopgate/engage/category';

dispatch(fetchRootCategories());
```
