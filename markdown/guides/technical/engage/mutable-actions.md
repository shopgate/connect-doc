# What Are Mutable Actions

You can use actions to control your application and data flow. See [pre-defined Engage Actions](../../../references/engage/actions/overview.md).  

The pre-defined actions have mutable behavior.  
Using mutable behavior and/or mutable actions, you can:  

- [Change or replace pre-defined actions](#change-or-replace-pre-defined-actions) 
- [Change data passed into pre-defined actions](#change-data-passed-into-pre-defined-actions)
- [Conditionally change behavior of pre-defined actions](#conditionally-change-behavior-of-pre-defined-actions) 


#### Change or replace pre-defined actions

Pre-defined Engage actions with mutable behavior have internal functions to set / replace action execution flow. 

- `replace` (replace original action implementation)
- `restore` (restore original action)
- `reset` (reset action to original state, discarding attached mutations)
- `useBefore` (prepend data flow mutation)

All functions can be called with optional arguments, passed to the next mutation.

```jsx
import { mutableActions } from '@shopgate/engage/core';
import { addToCart } from '@shopgate/engage/cart';

// Replace addToCart implementation
addToCart.replace((data) => {
  // Custom logic
});

// Restore addToCart implementation
addToCart.restore();

// Reset addToCart implementation, discarding mutations attached with useBefore
addToCart.reset();

// Prepend data flow mutation
addToCart.useBefore((data) => {
  // Change data of action
  return mutableActions.next(data);
});
```

#### Change data passed into pre-defined actions

Mutable actions, available in `@shopgate/engage/core` package:

- `mutableActions`
    - `next` (call next mutation with changed data)

```jsx
import { mutableActions } from '@shopgate/engage/core';
import { addToCart } from '@shopgate/engage/cart';

addToCart.useBefore((data) => {
  // Call next with changed data
  return mutableActions.next(data);
});
```

#### Conditionally change behavior of pre-defined actions

Mutable actions, available in `@shopgate/engage/core` package:

- `mutableActions`
    - `skipRest` (immediately call original action with given arguments, skipping the rest of mutations)
    - `stop` (stop action execution)

```jsx
import { mutableActions } from '@shopgate/engage/core';
import { addToCart } from '@shopgate/engage/cart';

addToCart.useBefore((data) => {
  // Call original, skipping the rest
  return mutableActions.skipRest();

  // Stop action execution
  return mutableActions.stop();
});
```

##### List of Engage mutable actions 

- [Cart](../../../references/engage/actions/cart.md)
    - [addCouponsToCart](../../../references/engage/actions/cart.md#addCouponsToCart)
    - [addProductsToCart](../../../references/engage/actions/cart.md#addProductsToCart)
    - [deleteCouponsFromCart](../../../references/engage/actions/cart.md#deleteCouponsFromCart)
    - [deleteProductsFromCart](../../../references/engage/actions/cart.md#deleteProductsFromCart)
    - [fetchCart](../../../references/engage/actions/cart.md#fetchCart)
    - [updateProductsInCart](../../../references/engage/actions/cart.md#updateProductsInCart)
- [Category](../../../references/engage/actions/category.md)
    - [fetchCategory](../../../references/engage/actions/category.md#fetchCategory)
    - [fetchCategoryChildren](../../../references/engage/actions/category.md#fetchCategoryChildren)
    - [fetchCategoryProducts](../../../references/engage/actions/category.md#fetchCategoryProducts)
    - [fetchRootCategories](../../../references/engage/actions/category.md#fetchRootCategories)
- [Checkout](../../../references/engage/actions/checkout.md)
    - [fetchCheckoutUrl](../../../references/engage/actions/checkout.md#fetchCheckoutUrl)
- [Favorites](../../../references/engage/actions/favorites.md)
    - [fetchFavorites](../../../references/engage/actions/favorites.md#fetchFavorites)
- [Product](../../../references/engage/actions/product.md)
    - [fetchProduct](../../../references/engage/actions/product.md#fetchProduct)
    - [fetchProductDescription](../../../references/engage/actions/product.md#fetchProductDescription)
    - [fetchProductImages](../../../references/engage/actions/product.md#fetchProductImages)
    - [fetchProductMedia](../../../references/engage/actions/product.md#fetchProductMedia)
    - [fetchProductOptions](../../../references/engage/actions/product.md#fetchProductOptions)
    - [fetchProductProperties](../../../references/engage/actions/product.md#fetchProductProperties)
    - [fetchProductRelations](../../../references/engage/actions/product.md#fetchProductRelations)
    - [fetchProductShipping](../../../references/engage/actions/product.md#fetchProductShipping)
    - [fetchProductVariants](../../../references/engage/actions/product.md#fetchProductVariants)
- [Reviews](../../../references/engage/actions/reviews.md)
    - [fetchProductReviews](../../../references/engage/actions/reviews.md#fetchProductReviews)
    - [fetchReviews](../../../references/engage/actions/reviews.md#fetchReviews)
    - [fetchUserReview](../../../references/engage/actions/reviews.md#fetchUserReview)
    - [flushUserReview](../../../references/engage/actions/reviews.md#flushUserReview)
    - [submitReview](../../../references/engage/actions/reviews.md#submitReview)
- [Search](../../../references/engage/actions/search.md)
    - [fetchSearchResults](../../../references/engage/actions/search.md#fetchSearchResults)
    - [fetchSearchSuggestions](../../../references/engage/actions/search.md#fetchSearchSuggestions)
- [Modal](../../../references/engage/actions/modal.md)
    - [closeModal](../../../references/engage/actions/modal.md#closeModal)
    - [showModal](../../../references/engage/actions/modal.md#showModal)
- [Page](../../../references/engage/actions/page.md)
    - [fetchPageConfig](../../../references/engage/actions/page.md#fetchPageConfig)
- [User](../../../references/engage/actions/user.md)
    - [fetchRegisterUrl](../../../references/engage/actions/user.md#fetchRegisterUrl)
    - [fetchUser](../../../references/engage/actions/user.md#fetchUser)
    - [login](../../../references/engage/actions/user.md#login)
    - [logout](../../../references/engage/actions/user.md#logout)
