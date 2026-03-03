---
stoplight-id: 3qxk9zc905o3h
---

# Cart Actions

* [addCouponsToCart](#addcouponstocart)
* [addProductsToCart](#addproductstocart)
* [deleteCouponsFromCart](#deletecouponsfromcart)
* [deleteProductsFromCart](#deleteproductsfromcart)
* [fetchCart](#fetchcart)
* [updateProductsInCart](#updateproductsincart)

## addCouponsToCart

Adds coupons to the cart.

### Usage

```javascript
import { addCouponsToCart } from '@shopgate/engage/cart';

const couponIds = ['someCouponId', 'anotherCouponId'];

dispatch(addCouponsToCart(couponIds));
```

### Parameters

* `couponIds` _(Array\<string\>)_: The  IDs of the coupons to add to the cart.

---

## addProductsToCart

Adds products to the cart. For each product that is added, this action determines if the product is a product variant or a base product by the input `productId`.
Metadata is then updated appropriately based off of the `productId`.

### Usage

```javascript
import { addProductsToCart } from '@shopgate/engage/cart';

const productsData = [
  {
    productId: '1',
    quantity: 1,
  },
  {
    productId: '2',
    quantity: 5,
  }
];

dispatch(addProductsToCart(productsData));
```

### Parameters

* `data` _(Array\<Object\>)_ **required**: The data necessary for the products to be added to the cart.
  * `productId` _(string)_ **required**: can be a base product ID or variant product ID.
  * `quantity` _(number)_ **required**: any number greater than `0`.
  * `options` _(Array\<Object\>)_ Required when a product with options is added to the cart.
    * `type` _(string)_ **required**: Option type (`select` or `text`).
    * `id` _(string)_ **required**: Option ID.
    * `value` _(string)_ **required**: Option value (ID of an option value for `select` options, input value for `text` options.)

---

## deleteCouponsFromCart

Removes coupons from the cart.

### Usage

```javascript
import { deleteCouponsFromCart } from '@shopgate/engage/cart';

const couponIds = ['someCouponId', 'anotherCouponId'];

dispatch(deleteCouponsFromCart(couponIds));
```

### Parameters

* `couponIds` _(Array\<string\>)_ **required**: The IDs of the coupons to be removed from the cart.

---

## deleteProductsFromCart

Removes products from the cart.

### Usage

```javascript
import { deleteProductsFromCart } from '@shopgate/engage/cart';

const cartItemIds = ['1', '2', '5'];

dispatch(deleteProductsFromCart(cartItemIds));
```

### Parameters

* `cartItemIds` _(Array\<string\>)_ **required**: The IDs of the cart items to be removed from the cart.

---

## fetchCart

Retrieves the current cart for the user.

### Usage

```javascript
import { fetchCart } from '@shopgate/engage/cart';

dispatch(fetchCart());
```

---

## updateProductsInCart

Updates the quantity of a product in the cart.  The input can be an array of multiple products.

### Usage

```javascript
import { updateProductsInCart } from '@shopgate/engage/cart';

const updateData = [
  {
    cartItemId: '20',
    quantity: 2,
  },
  {
    cartItemId: '21',
    quantity: 4,
  }
]

dispatch(updateProductsInCart(updateData));
```


### Parameters

* `updateData` _(Array\<Object\>)_ **required**: The data required to update the products in the cart.
  * `cartItemId` _(string)_ **required**: The ID of the cart item to be updated.
  * `quantity` _(number)_ **required**: Any number greater than `0`.