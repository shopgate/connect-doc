# What Are Mutable Actions

You can use actions to control your application and data flow. See [pre-defined Engage Actions](/references/engage/actions).  

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

- [Cart](/references/engage/actions/cart)
    - [addCouponsToCart](/references/engage/actions/cart#addCouponsToCart)
    - [addProductsToCart](/references/engage/actions/cart#addProductsToCart)
    - [deleteCouponsFromCart](/references/engage/actions/cart#deleteCouponsFromCart)
    - [deleteProductsFromCart](/references/engage/actions/cart#deleteProductsFromCart)
    - [fetchCart](/references/engage/actions/cart#fetchCart)
    - [updateProductsInCart](/references/engage/actions/cart#updateProductsInCart)
- [Category](/references/engage/actions/category)
    - [fetchCategory](/references/engage/actions/category#fetchCategory)
    - [fetchCategoryChildren](/references/engage/actions/category#fetchCategoryChildren)
    - [fetchCategoryProducts](/references/engage/actions/category#fetchCategoryProducts)
    - [fetchRootCategories](/references/engage/actions/category#fetchRootCategories)
- [Checkout](/references/engage/actions/checkout)
    - [fetchCheckoutUrl](/references/engage/actions/checkout#fetchCheckoutUrl)
- [Favorites](/references/engage/actions/favorites)
    - [fetchFavorites](/references/engage/actions/favorites#fetchFavorites)
- [Product](/references/engage/actions/product)
    - [fetchProduct](/references/engage/actions/product#fetchProduct)
    - [fetchProductDescription](/references/engage/actions/product#fetchProductDescription)
    - [fetchProductImages](/references/engage/actions/product#fetchProductImages)
    - [fetchProductMedia](/references/engage/actions/product#fetchProductMedia)
    - [fetchProductOptions](/references/engage/actions/product#fetchProductOptions)
    - [fetchProductProperties](/references/engage/actions/product#fetchProductProperties)
    - [fetchProductRelations](/references/engage/actions/product#fetchProductRelations)
    - [fetchProductShipping](/references/engage/actions/product#fetchProductShipping)
    - [fetchProductVariants](/references/engage/actions/product#fetchProductVariants)
- [Reviews](/references/engage/actions/reviews)
    - [fetchProductReviews](/references/engage/actions/reviews#fetchProductReviews)
    - [fetchReviews](/references/engage/actions/reviews#fetchReviews)
    - [fetchUserReview](/references/engage/actions/reviews#fetchUserReview)
    - [flushUserReview](/references/engage/actions/reviews#flushUserReview)
    - [submitReview](/references/engage/actions/reviews#submitReview)
- [Search](/references/engage/actions/search)
    - [fetchSearchResults](/references/engage/actions/search#fetchSearchResults)
    - [fetchSearchSuggestions](/references/engage/actions/search#fetchSearchSuggestions)
- [Modal](/references/engage/actions/modal)
    - [closeModal](/references/engage/actions/modal#closeModal)
    - [showModal](/references/engage/actions/modal#showModal)
- [Page](/references/engage/actions/page)
    - [fetchPageConfig](/references/engage/actions/page#fetchPageConfig)
- [User](/references/engage/actions/user)
    - [fetchRegisterUrl](/references/engage/actions/user#fetchRegisterUrl)
    - [fetchUser](/references/engage/actions/user#fetchUser)
    - [login](/references/engage/actions/user#login)
    - [logout](/references/engage/actions/user#logout)
