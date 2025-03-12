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

> **Attention**: The path to the old modules is deprecated and will be removed in _ENGAGE v7_: `import { fetchCategory } from '@shopgate/pwa-common-commerce/category'`

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

> **Attention**: The path to the old modules is deprecated and will be removed in _ENGAGE v7_: `import { fetchCategoryChildren } from '@shopgate/pwa-common-commerce/category'`

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

> **Attention**: The path to the old modules is deprecated and will be removed in _ENGAGE v7_: `import { fetchCategoryProducts } from '@shopgate/pwa-common-commerce/category'`

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

> **Attention**: The path to the old modules is deprecated and will be removed in _ENGAGE v7_: `import { SORT_RELEVANCE, SORT_PRICE_ASC, SORT_PRICE_DESC } from '@shopgate/pwa-common/constants/DisplayOptions'`

---

## fetchRootCategories

Retrieves the root categories from the store.

### Usage

```javascript
import { fetchRootCategories } from '@shopgate/engage/category';

dispatch(fetchRootCategories());
```

> **Attention**: The path to the old modules is deprecated and will be removed in _ENGAGE v7_: `import { fetchRootCategories } from '@shopgate/pwa-common-commerce/category'`
