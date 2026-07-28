---
stoplight-id: 12vhrdt8jxe3j
---

# Emarsys Module

The Emarsys module integrates Predict recommendations and commerce tracking with the native Emarsys SDK.

```jsx
import { Emarsys } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { Emarsys } from '@shopgate/native-modules';

export function ProductRecommendations() {
  const [products, setProducts] = useState([]);
  useEffect(() => {
    const loadProducts = async () => {
      const result = await Emarsys.recommendProducts({
        logic: 'POPULAR',
        logicOptions: { variants: ['default'] },
        recommendationOptions: { limit: 10 },
      });
      setProducts(result);
    };
    loadProducts();
  }, []);
  return <p>Recommendations: {products.length}</p>;
}
```

## recommendProducts(params)

```js
const products = await Emarsys.recommendProducts({
  logic: 'POPULAR',
  logicOptions: { variants: ['default'] },
  recommendationOptions: { limit: 10 },
});
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `logic` | `string` | yes | Recommendation algorithm. |
| `logicOptions` | `object` | yes | Logic-specific options such as `query`, `cartItems`, or `variants`. |
| `recommendationOptions` | `object` | yes | Optional limit, availability zone, and filters. |

Returns a product array. Recommendation logic includes `SEARCH`, `CART`, `RELATED`, `CATEGORY`, `ALSO_BOUGHT`, `POPULAR`, `PERSONAL`, and `HOME`.

## Tracking methods

The module also supports `setContact`, `clearContact`, `trackRecommendationClick`, `trackCategoryView`, `trackCart`, and `trackPurchase`. Each method accepts the parameter object described by its native module contract and returns a promise.
