---
stoplight-id: 64sdnlz6cm3qw
---

# Product Actions

* [fetchProduct](#fetchProduct)
* [fetchProductDescription](#fetchProductDescription)
* [fetchProductImages](#fetchProductImages)
* [fetchProductOptions](#fetchProductOptions)
* [fetchProductProperties](#fetchProductProperties)
* [fetchProductRelations](#fetchProductRelations)
* [fetchProductShipping](#fetchProductShipping)
* [fetchProductVariants](#fetchProductVariants)

## fetchProduct

Fetches a product from the server.

### Usage

```javascript
import { fetchProduct } from '@shopgate/engage/product';

const productId = 'abc123';
const forceFetch = false;

dispatch(fetchProduct(productId, forceFetch));
```


### Parameters

* `productId` *(string)* **required**: The ID of the product to fetch.
* `forceFetch` *(boolean)*: Default is `false`. Indicates if the product should be fetched, even if there is a still valid entry inside of Redux.

---

## fetchProductDescription

Fetches a product description from the server.

### Usage

```javascript
import { fetchProductDescription } from '@shopgate/engage/product';

const productId = 'abc123';

dispatch(fetchProductDescription(productId));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.

---

## fetchProductImages

Fetches product images from the server.

### Usage

```javascript
import { fetchProductImages } from '@shopgate/engage/product';

const productId = 'abc123';
const formats = [{
  width: 1024,
  height: 1024,
}];

dispatch(fetchProductImages(productId, formats));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.
* `formats` _(Array\<Object\>)_ **required**: The desired formats for the images.
  * `height` _(number)_ **required**: The height of the format.
  * `width` _(number)_ **required**: The width of the format.

---

## fetchProductOptions

Fetches product options from the server.

### Usage

```javascript
import { fetchProductOptions } from '@shopgate/engage/product';

const productId = 'abc123';

dispatch(fetchProductOptions(productId));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.

---

## fetchProductProperties

Fetches product properties from the server.

### Usage

```javascript
import { fetchProductProperties } from '@shopgate/engage/product';

const productId = 'abc123';

dispatch(fetchProductProperties(productId));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.

---

## fetchProductRelations

Fetches product relations from the server.

### Usage

```javascript
import {
  fetchProductRelations,
  PRODUCT_RELATIONS_TYPE_UPSELLING
} from '@shopgate/engage/product';

const productId = 'abc123';
const type = PRODUCT_RELATIONS_TYPE_UPSELLING;

dispatch(fetchProductRelations(productId, type));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.
* `type` *(string)* **required**: The desired type of the related products.
  * Possible Values: `crossSelling`, `upselling`, `bonus`, `boughtWith`, `custom`.  All of these values are prepared as constants. They can be imported like in the snippet below.
* `limit` _(number)_: The number of related products to request. Default is 20 items.

```javascript
import {
  PRODUCT_RELATIONS_TYPE_CROSS_SELLING,
  PRODUCT_RELATIONS_TYPE_UPSELLING,
  PRODUCT_RELATIONS_TYPE_BONUS,
  PRODUCT_RELATIONS_TYPE_BOUGHT_WITH,
  PRODUCT_RELATIONS_TYPE_CUSTOM
} from '@shopgate/engage/product';
```
`

---

## fetchProductShipping

Fetches shipping information for a product from the server.

### Usage

```javascript
import { fetchProductShipping } from '@shopgate/engage/product';

const productId = 'abc123';

dispatch(fetchProductShipping(productId));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.

---

## fetchProductVariants

Fetches product variants from the server.

### Usage

```javascript
import { fetchProductVariants } from '@shopgate/engage/product';

const productId = 'abc123';

dispatch(fetchProductVariants(productId));
```


### Parameters

* `productId` *(string)* **required**: The ID of the related product.