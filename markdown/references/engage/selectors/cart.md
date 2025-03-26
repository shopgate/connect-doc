---
stoplight-id: v8z0hkt9ugytx
---

# Cart Selectors

* [getCartItems](#getcartitems)
* [getCartItemById](#getcartitembyid)
* [getCartProducts](#getcartproducts)
* [getCartCoupons](#getcartcoupons)
* [getCartProductCount](#getcartproductcount)
* [getProductPendingCount](#getproductpendingcount)
* [getCartProductDisplayCount](#getcartproductdisplaycount)
* [getOrderableStatus](#getorderablestatus)
* [getCurrency](#getcurrency)
* [getSubTotal](#getsubtotal)
* [getShippingCosts](#getshippingcosts)
* [getCartMessages](#getcartmessages)
* [getFlags](#getflags)
* [getAddToCartOptions](#getaddtocartoptions)
* [getAddToCartMetadata](#getaddtocartmetadata)
* [hasCouponSupport](#hascouponsupport)
* [getIsFetching](#getIsFetching)

## getCartItems

Retrieves all cart items from the cart data in the store.

### Usage

```javascript
import { getCartItems } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartItems } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: The cart items as an array. If no items are found, it returns an empty array.
> Cart items will match the `cartItems` from the [getCart](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.getCart.v1/post) pipeline response.

---

## getCartItemById

Retrieves a cart item from the cart data in the store by the item's ID.

### Usage

```javascript
import { getCartItemById } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartItemById } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `cartItemId` *(string)* __required__

### Returns

*(Object|null)*: The cart item. If no item is found for the provided ID, the selector returns `null`.
> The cart item will match the `cartItems` from the [getCart](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.getCart.v1/post) pipeline response.

---

## getCartProducts

Retrieves all cart items from the cart data in the store that are of type `product`.

### Usage

```javascript
import { getCartProducts } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartProducts } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: An array of the products in the cart data. If no products are found, it returns an empty array .
> Cart products will match the cartItems of `type` "product" from the [getCart](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.getCart.v1/post) pipeline response.

---

## getCartCoupons

Retrieves all cart items from the cart data in the store that are of the type `coupon`.

### Usage

```javascript
import { getCartCoupons } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartCoupons } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: An array of the coupons in the cart. If no coupons are found, it returns  an empty array.
> Cart coupons will match the cartItems of `type` "coupon" from the [getCart](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.getCart.v1/post) pipeline response.
---

## getCartProductCount

Retrieves the number of products from the cart data in the store. This number is synchronized with the backend and reflects the actual number of products in the cart.

### Usage

```javascript
import { getCartProductCount } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartProductCount } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number)*: The current amount of products in the cart. If there are no products, it returns `0`. __Important__: `getCartProductCount` does not include the coupons.

---

## getProductPendingCount

Retrieves the number of products from the cart data in the store that are only in the frontend and have not yet synchronized with the backend.

### Usage

```javascript
import { getProductPendingCount } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getProductPendingCount } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number)*: The current pending product count. It returns `0` by default.

---

## getCartProductDisplayCount

Retrieves the full number of products from the cart data in the store. It combines the product count and the pending product count. This number is equal to the product count when newly added products are synchronized with the backend.

### Usage

```javascript
import { getCartProductDisplayCount } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartProductDisplayCount } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number)*: The current number of products in the cart data of the store.

---

## getOrderableStatus

Retrieves the current `isOrderable` status from the cart data in the store.

### Usage

```javascript
import { getOrderableStatus } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getOrderableStatus } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the cart is orderable.

---

## getCurrency

The cart data that is received from the [getCart](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.getCart.v1/post) pipeline contains information about the currency used for the current cart. This selector retrieves the __currency code__ from that cart data in the store.

### Usage

```javascript
import { getOrderableStatus } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getOrderableStatus } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(string)*: The currency code. Examples include `USD` or `EUR`.

---

## getSubTotal

Retrieves the subtotal before shipping costs from the cart data in the store.

### Usage

```javascript
import { getSubTotal } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getSubTotal } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number)*: The subtotal as a float number.

---

## getShippingCosts

Retrieves the total shipping costs from the cart data in the store.

### Usage

```javascript
import { getShippingCosts } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getShippingCosts } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(number|null)*: The shipping costs as a float number. It returns `0` on free shipping, and `null` if no shipping costs are found.

---

## getCartMessages

Retrieves all messages that are present in the cart data in the store.

### Usage

```javascript
import { getCartMessages } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getCartMessages } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Array)*: An array of messages. If no messages are set, it returns an empty array.

---

## getFlags

Retrieves additional information about the cart from the cart data in the store.

### Usage

```javascript
import { getFlags } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getFlags } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Object)*: The cart flags.

* `taxIncluded` *(boolean)*: Whether the cart shows gross or net prices.
* `orderable` *(boolean)*: Whether the cart is orderable.
* `coupons` *(boolean)*: Whether the cart can have coupons.

---

## getAddToCartOptions

Builds the data for the `options` property in the [addProducts](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.addProducts.v1/post) pipeline request payload.

### Usage

```javascript
import { getAddToCartOptions } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getAddToCartOptions } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.
* `props` *(Object)* __required__: An object containing props.
  * `options` *(Object)* __required__: The product options.

### Returns

*(Object|null)*: The options for the pipeline request.

---

## getAddToCartMetadata

Builds the data for the `metadata` property in the [addProducts](../../../../static/pipelines/shopgate-cart-pipelines.oas2.yml/paths/~1shopgate.cart.addProducts.v1/post) pipeline request payload.

### Usage

```javascript
import { getAddToCartMetadata } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getAddToCartMetadata } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(Object|null)*: The metadata object for the pipeline request.

---

## hasCouponSupport

Checks if the cart supports redemption of coupons.

### Usage

```javascript
import { hasCouponSupport } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { hasCouponSupport } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the coupons feature is enabled.

---

## getIsFetching

Checks if the cart is currently fetching fresh data.

### Usage

```javascript
import { getIsFetching } from '@shopgate/engage/cart';
```

> **Attention**: The path to the old modules is deprecated and will be removed in *ENGAGE v7*: `import { getIsFetching } from '@shopgate/pwa-common-commerce/cart'`

### Parameters

* `state` *(Object)* __required__: The application state.

### Returns

*(boolean)*: Whether the cart is fetching.