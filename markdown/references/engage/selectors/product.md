---
stoplight-id: 0cxnnkble9r0n
---

# Product Selectors

* [getProductById](#getproductbyid)
* [getProduct](#getproduct)
* [getProductName](#getproductname)
* [getProductRating](#getproductrating)
* [getProductManufacturer](#getproductmanufacturer)
* [getProductStock](#getproductstock)
* [getProductAvailability](#getproductavailability)
* [getProductFlags](#getproductflags)
* [getProductCurrency](#getproductcurrency)
* [getProductUnitPrice](#getproductunitprice)
* [hasProductVariants](#hasproductvariants)
* [isBaseProduct](#isbaseproduct)
* [getBaseProductId](#getbaseproductid)
* [getBaseProduct](#getbaseproduct)
* [hasBaseProductVariants](#hasbaseproductvariants)
* [getProductMetadata](#getproductmetadata)
* [getBaseProductMetadata](#getbaseproductmetadata)
* [getProductShipping](#getproductshipping)
* [getProductProperties](#getproductproperties)
* [getProductDescription](#getproductdescription)
* [getProductImages](#getproductimages)
* [getProductVariants](#getproductvariants)
* [isProductOrderable](#isproductorderable)
* [getVariantId](#getvariantid)
* [getVariantAvailabilityByCharacteristics](#getvariantavailabilitybycharacteristics)
* [getResultHash](#getresulthash)
* [getResultByHash](#getresultbyhash)
* [getProductsResult](#getproductsresult)
* [getProductOptions](#getproductoptions)
* [hasProductOptions](#hasproductoptions)
* [areProductOptionsSet](#areproductoptionsset)
* [isProductPageLoading](#isproductpageloading)
* [getProductPriceAddition](#getproductpriceaddition)
* [getProductTotalPrice](#getproducttotalprice)

## getProductById

Retrieves a specific product by its ID. It returns `null` if no product is found.

### Usage

```javascript
import { getProductById } from '@shopgate/engage/product';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductById } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)* __required__: The product ID to search for.

### Returns

*(Object|null)*: Returns the product data object from the store. If no product is found, it returns `null`.

> Products will have the shape of entities from the [getProduct](../../../../static/pipelines/shopgate-products.oas2.yml/paths/~1shopgate.catalog.getProductsByIds.v1) pipeline response.

---

## getProduct

Retrieves the product data for the passed productId from the store.

### Usage

```javascript
import { getProduct } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProduct } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product data. If no product is found, it returns `null`.
> Products will have the shape of entities from the [getProduct](../../../../static/pipelines/shopgate-products.oas2.yml/paths/~1shopgate.catalog.getProductsByIds.v1) pipeline response.

---

## getProductName

Retrieves the name of a product from the product data in the store.

### Usage

```javascript
import { getProductName } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductName } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The product name. If no product is found, it returns `null`.

---

## getProductRating

Retrieves product rating data from the product data in the store.

### Usage

```javascript
import { getProductRating } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductRating } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The rating data. If no product is found, it returns `null`.

---

## getProductManufacturer

Retrieves the product manufacturer from the product data in the store.

### Usage

```javascript
import { getProductManufacturer } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductManufacturer } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The manufacturer. If no product is found, it returns `null`.

---

## getProductStock

Retrieves the product stock information from the product data in the store.

### Usage

```javascript
import { getProductStock } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductStock } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The stock information. If no product is found, it returns `null`.

---

## getProductAvailability

Retrieves the availability information from the product data in the store.

### Usage

```javascript
import { getProductAvailability } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductAvailability } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The stock information. If no product is found, it returns `null`.

---

## getProductFlags

Retrieves the product flags from the product data in the store.

### Usage

```javascript
import { getProductFlags } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductFlags } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product flags. If no product is found, it returns `null`.

---

## getProductCurrency

Retrieves the currency code from the product data in the store.

### Usage

```javascript
import { getProductCurrency } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductCurrency } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The currency code (ISO 4217 alphabetic code). If no product is found, it returns `null`.

---

## getProductUnitPrice

Retrieves the unit price from the product data in the store.

### Usage

```javascript
import { getProductUnitPrice } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductUnitPrice } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(number|null)*: The unit price (float value). If no product is found, it returns `null`.

---

## hasProductVariants

Retrieves whether a product has variants from the product data in the store.

### Usage

```javascript
import { hasProductVariants } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasProductVariants } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether the product has variants.

---

## isBaseProduct

Retrieves whether a product is a base product (not a variant) from the product data in the store.

### Usage

```javascript
import { isBaseProduct } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isBaseProduct } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether the product is a base product.

---

## getBaseProductId

Retrieves a product ID of the base product from the product data in the store.

### Usage

```javascript
import { getBaseProductId } from '@shopgate/pwa-common-commerce/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isBaseProduct } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The current base product ID. If no ID is determined, it returns `null`.

---

## getBaseProduct

Retrieves the appropriate base product from the product data in the store - independent if the productId already references the base product.

### Usage

```javascript
import { getBaseProduct } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getBaseProduct } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.

### Returns

*(Object|null)*: The base product data. If no base product is found, it returns `null`.

---

## hasBaseProductVariants

Retrieves whether the base product has variants from the product data in the store.

### Usage

```javascript
import { hasBaseProductVariants } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasBaseProductVariants } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.

### Returns

*(boolean)*: Whether the base product has variants.

---

## getProductMetadata

Retrieves the product metadata from the product data in the store.

### Usage

```javascript
import { getProductMetadata } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductMetadata } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product metadata. If no product is found, it returns `null`.

---

## getBaseProductMetadata

Retrieves the base product metadata from the product data in the store.

### Usage

```javascript
import { getBaseProductMetadata } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getBaseProductMetadata } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product metadata. If no product is found, it returns `null`.

---

## getProductShipping

Retrieves the shipping data from the product data in the store.

### Usage

```javascript
import { getProductShipping } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductShipping } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product shipping data. If no product or shipping data is found, it returns `null`.

### Example Result
```javascript
{
  currency: 'EUR',
  price: 5.99
}
```
---

## getProductProperties

Retrieves the properties of a product from the product data in the store.

### Usage

```javascript
import { getProductProperties } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductProperties } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product properties. If no product or properties are found, it returns `null`.

### Example Result
```javascript
[{
  label: 'SKU',
  value: '0123456789012'
}, {
  label: 'Weight',
  value: '150g'
}]
```
---

## getProductDescription

Retrieves the product description from the product data in the store.

### Usage

```javascript
import { getProductDescription } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductDescription } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The product description (might contain HTML markup). If no product or description is found, it returns `null`.

---

## getProductImages

Retrieves the images for a product from the product data in the store. If the props contain a variant ID, and the related product does not have images, the selector attempts to choose images from its base product.

### Usage

```javascript
import { getProductImages } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductImages } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.
  * `formats` *(Array\<Object\>)*: The desired formats of the returned images (need the be requested via the [fetchProductImages](../actions/product.md#fetchProductImages) action).

### Returns

*(Array|null)*: The product images. If no product or images are found, it returns `null`.

### Example
```javascript
  const props = {
    productId: 'abc123',
    formats: [{
      width: 440, height: 440,
    }, {
      width: 1024, height: 1024,
    }]
  };

  const images = getProductImages(state, props);

  // Selector result
  [{
    width: 440,
    height: 440,
    sources: [
      'https://images.expample.com/image',
      'https://images.expample.com/image'
    ]
  }, {
    width: 1024,
    height: 1024,
    sources: [
      'https://images.expample.com/image',
      'https://images.expample.com/image'
    ]
  }]
```
---

## getProductVariants

Retrieves the product variant data from the product data in the store.

### Usage

```javascript
import { getProductVariants } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductVariants } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(Object|null)*: The product variant data. If no product or variants are found, it returns `null`.

---

## isProductOrderable

Retrieves whether a product is orderable from the product data in the store.

### Usage

```javascript
import { isProductOrderable } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isProductOrderable } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether the product is orderable.

---

## getVariantId

Retrieves the product ID of a variant product from the product data in the store. When none of the productIds from the props reference a variant product, the selector returns `null`.

### Usage

```javascript
import { getVariantId } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getVariantId } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(string|null)*: The product description. If no product or description is found, it returns `null`.

---

## getVariantAvailabilityByCharacteristics

Retrieves an availability object for a passed set of variant characteristics from the product data in the store.

### Usage

```javascript
import { getVariantAvailabilityByCharacteristics } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getVariantAvailabilityByCharacteristics } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `characteristics` *(Array)* __required__: The set characteristics.

### Returns

*(Object|null)*: The availability information. If no product is found, it returns `null`.

---

## getResultHash

Retrieves the generated result hash for a category ID or search phrase.

### Usage

```javascript
import { getResultHash } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getResultHash } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `categoryId` *(string)* : The category ID to use.
  * `searchPhrase` *(string)* : The search phrase to use.

### Returns

*(string|null)*: The result hash. If neither category ID nor search phrase is set, it returns `null`.

---

## getResultByHash

Retrieves a result set by a generated result hash from the product data in the store,

### Usage

```javascript
import { getResultByHash } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getResultByHash } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `categoryId` *(string)* : The category ID to use.
  * `searchPhrase` *(string)* : The search phrase to use.

### Returns

*(Object|null)*: The result set. If neither category ID nor search phrase is set or no results are found, it returns `null`.

---

## getProductsResult

Retrieves a collection of product data based on either a category ID or a search phrase from the product data in the store.

### Usage

```javascript
import { getProductsResult } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductsResult } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `categoryId` *(string)* : The category ID to use.
  * `searchPhrase` *(string)* : The search phrase to use.

### Returns

*(Object)*: The result set containing `products`, `totalProductCount`, `sort` and `hash`. If no products are found for the given category ID or search phrase, it returns the result set with an empty array of `products`.

---

## getProductOptions

Retrieves a product options from the product data in the store and transforms it to the correct data structure which can be used to render option pickers.

### Usage

```javascript
import { getProductOptions } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductOptions } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: A product ID to use.
  * `variantId` *(string)*: A variant ID to use. If variant ID is sent, the product ID will be ignored.
  * `currentOptions` *(Array)*: The currently set product options.

### Returns

*(Array)*: The product options.

### Example
```javascript
const props = {
  productId: 'abc123',
  currentOptions: {
    '1': '1', // {optionId}: {optionValueId}
    '6': '21'
  }
};

const options = getProductOptions(state, props)

// Selector result
[
  {
    id: '1',
    label: 'Option 1',
    type: 'select',
    value: '1', // Selected optionValueId of "Option 1"
    items: [
      {
        label: 'Option Value 1-1',
        currency: 'EUR',
        value: '1', // optionValueId
        price: 1.4, // Product price modifier of this option value
        priceDifference: 0.5 // Price difference compared to the currently visible price
      },
      {
        label: 'Option Value 1-2',
        currency: 'EUR',
        value: '2',
        price: 0,
        priceDifference: -1
      }
    ]
  },
  {
    id: '6',
    label: 'Option 2',
    type: 'select',
    value: '21',
    items: [
      {
        label: 'Option Value 2-1',
        currency: 'EUR',
        value: '21',
        price: 1,
        priceDifference: 0
      }
    ]
  }
]
```

---

## hasProductOptions

Retrieves whether a product has options from the product data in the store.

### Usage

```javascript
import { hasProductOptions } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasProductOptions } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether the product has options.

---

## areProductOptionsSet

Checks if all product options for a product are set.

### Usage

```javascript
import { areProductOptionsSet } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { areProductOptionsSet } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether all options are set.

---

## isProductPageLoading

Retrieves whether the products of the product page are loading. Depending on the configuration of the base product, it also checks if the loading process of a selected variant is currently ongoing.

### Usage

```javascript
import { isProductPageLoading } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { isProductPageLoading } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(boolean)*: Whether the products of the product page are loading.

---

## getProductPriceAddition

Retrieves the additional price for a product based on the selected options.

### Usage

```javascript
import { getProductPriceAddition } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductPriceAddition } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `options` *(Array)* __required__: The selected options.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(number)*: The additional product price.

---

## getProductTotalPrice

Retrieves the total product price by calculating all additional product option costs.

### Usage

```javascript
import { getProductTotalPrice } from '@shopgate/engage/product'
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductTotalPrice } from '@shopgate/pwa-common-commerce/product'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `options` *(Array)* __required__: The selected options.
  * `productId` *(string)*: The product ID to search for.
  * `variantId` *(string)*: The variant ID to search for.

### Returns

*(number)*: The calculated total product price.